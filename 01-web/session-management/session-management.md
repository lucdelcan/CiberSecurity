# Session Management

- **WSTG:** `WSTG-SESS-*`
- **OWASP Top 10:** `A07:2021 – Identification and Authentication Failures`
- **Alias:** gestión de sesión

## Qué es

Fallos en cómo se crean, transmiten, almacenan y expiran las sesiones, que permiten robar o suplantar la sesión de otro usuario.

## Vectores frecuentes

- **Tokens débiles:** IDs de sesión predecibles o con poca entropía.
- **Atributos de cookie:** falta de `HttpOnly`, `Secure`, `SameSite`.
- **Session fixation:** el ID no cambia tras el login (el atacante fija uno conocido).
- **Exposición del token:** en la URL, logs o campos visibles.
- **Logout/timeout:** la sesión no se invalida al salir o no expira por inactividad.
- **Session hijacking:** robo del token (XSS, red insegura) y reutilización.

## Cómo detectarla

- Analiza la aleatoriedad del token y sus atributos.
- Comprueba si el ID cambia tras autenticar (fixation).
- Verifica que logout y timeout invalidan la sesión en **servidor**, no solo borran la cookie.

## Impacto

Suplantación de usuarios y toma de cuentas.

## Cómo remediar

- Tokens aleatorios y robustos generados por el framework.
- Cookies `HttpOnly`, `Secure`, `SameSite`.
- Regenerar el ID tras login; invalidar en servidor al hacer logout y por timeout.
- No exponer el token en URL ni logs.

## Referencias

- OWASP WSTG `WSTG-SESS-*` · CWE-384 / CWE-613
- OWASP Session Management Cheat Sheet

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/06-session.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
