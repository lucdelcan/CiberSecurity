# Broken Authentication

- **WSTG:** `WSTG-AUTHN-*`
- **OWASP Top 10:** `A07:2021 – Identification and Authentication Failures`
- **Alias:** autenticación rota

## Qué es

Fallos en el diseño o implementación de la autenticación que permiten suplantar a otros usuarios: desde saltarse el login hasta abusar del reset de contraseña o de tokens mal generados.

## Vectores frecuentes

- **Bypass del esquema:** acceso directo a rutas protegidas, forzado de parámetros (`admin=true`), respuestas manipulables.
- **Credenciales por defecto** y contraseñas débiles.
- **Reset de contraseña inseguro:** tokens predecibles, sin caducidad, host header injection en el enlace, respuesta que filtra el token.
- **JWT mal implementado:** `alg:none`, firma no verificada, secreto débil/forzable, `kid` inyectable.
- **MFA débil:** se puede omitir, códigos sin rate limit, backup codes filtrados.
- **Gestión de sesión débil** (ver `../session-management/`).

## Cómo detectarla

- Mapea todo el flujo: registro, login, logout, "recuérdame", reset, MFA.
- Prueba acceso a funciones sin autenticar y con rol insuficiente.
- Analiza los tokens (JWT) y el proceso de reset paso a paso.

## Impacto

Toma de cuentas (incluidas de administrador) y acceso no autorizado. Suele ser alto/crítico.

## Cómo remediar

- Framework de autenticación probado; no reinventar.
- MFA, política de contraseñas robusta y rate limiting.
- Tokens de reset aleatorios, de un solo uso y con caducidad; no filtrarlos.
- JWT: verificar firma y algoritmo, secretos fuertes, expiración.

## Referencias

- OWASP WSTG `WSTG-AUTHN-*` · CWE-287
- OWASP Authentication Cheat Sheet

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/04-authentication.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
