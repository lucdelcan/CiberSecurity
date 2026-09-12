# Ataques a OAuth 2.0 / SSO

- **WSTG:** `WSTG-AUTHN-*` · Ver hub: [broken-authentication.md](broken-authentication.md)
- **OWASP Top 10:** `A07:2021`
- **Alias:** OAuth, OpenID Connect, inicio de sesión social

## Qué es

OAuth delega la autenticación en un proveedor (Google, etc.). Las vulnerabilidades suelen estar en la **implementación del cliente** (la app que integra el login), no en el protocolo, y permiten robar cuentas.

## Conceptos

Flujo típico (authorization code): la app redirige al proveedor con `client_id`, `redirect_uri`, `scope`, `state`; el proveedor devuelve un `code` a `redirect_uri`; la app lo canjea por un token.

## Vectores

- **`redirect_uri` laxo:** si el proveedor/app aceptan un `redirect_uri` no exacto, rediriges el `code`/token a un dominio tuyo → robo del código y toma de cuenta. (Ver también `../open-redirect/`.)
- **Falta de `state`:** sin `state` impredecible → **CSRF en el login** (vincular la cuenta de la víctima a la del atacante o viceversa).
- **`code` reutilizable o sin atar al cliente:** reusar/robar el código.
- **Robo de token por referer/historial** si viaja en la URL.
- **Account takeover por email no verificado:** si la app confía en el email del proveedor sin verificar y hace *account linking* por email.
- **Scopes excesivos** concedidos.

## Cómo probarlo

1. Mapea todo el flujo con el proxy (parámetros y redirecciones).
2. Manipula `redirect_uri` (subdominios, sufijos, `//`, `@`, path extra).
3. Quita/repite `state` y `code`; prueba `code` en otra sesión.
4. Revisa cómo se hace el *linking* de cuentas por email.

## Impacto

Toma de cuentas en la aplicación cliente. Alto/crítico.

## Remediación

- `redirect_uri` con **coincidencia exacta** y lista blanca.
- `state` obligatorio, aleatorio y validado; PKCE en clientes públicos.
- No confiar en emails no verificados para vincular cuentas.
- Códigos de un solo uso, atados al cliente y de vida corta.

## Referencias

- PortSwigger — OAuth 2.0 authentication vulnerabilities · RFC 6749/6819
