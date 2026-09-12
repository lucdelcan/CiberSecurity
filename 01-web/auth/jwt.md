# Ataques a JWT

- **WSTG:** `WSTG-AUTHN-*` · Ver hub: [broken-authentication.md](broken-authentication.md)
- **OWASP Top 10:** `A07:2021`
- **Alias:** JSON Web Token

## Qué es

Un JWT es `header.payload.signature` en base64url. El servidor confía en su contenido si la firma es válida. Los ataques explotan verificaciones de firma mal implementadas o secretos débiles para **forjar** tokens (p. ej. subir de usuario a admin).

## Reconocimiento

- Decodifica header y payload (base64url). Mira `alg`, `kid`, y claims como `role`, `admin`, `user`.
- Identifica el algoritmo: `HS256` (simétrico, secreto) vs `RS256` (asimétrico, clave privada/pública).

## Vectores

- **`alg: none`:** cambiar el algoritmo a `none` y quitar la firma; si el servidor lo acepta, forjas cualquier token.
- **Firma no verificada:** el servidor decodifica pero no valida la firma → cambia el payload libremente.
- **Secreto débil (HS256):** crackea el secreto por diccionario y firma tokens propios.
- **Confusión de algoritmo RS256→HS256:** si el server usa la **clave pública** como secreto HMAC, firmas un HS256 con esa clave pública (que conoces).
- **`kid` inyectable:** path traversal o SQLi en `kid` para forzar una clave conocida (p. ej. `/dev/null`).
- **`jku`/`x5u` controlables:** apuntar la URL de claves a un JWKS tuyo.
- **Claims:** `exp` no validado (tokens eternos), falta de `aud`/`iss`.

## Herramientas

```
jwt_tool <token>                 # análisis y ataques
hashcat -m 16500 jwt.txt wl.txt  # crackear HS256
```

## Impacto

Forjar tokens = suplantar a cualquier usuario, incluido admin → toma de cuentas / bypass total. Crítico.

## Remediación

- Verificar **siempre** la firma y **fijar** el algoritmo esperado en servidor (no confiar en el `alg` del token).
- Secretos HMAC largos y aleatorios; claves gestionadas.
- Validar `exp`, `aud`, `iss`. No aceptar `none`.
- No cargar claves desde URLs controlables por el usuario.

## Referencias

- PortSwigger — JWT attacks · CWE-347
