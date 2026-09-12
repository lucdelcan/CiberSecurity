# WSTG-SESS · Session Management

- [ ] `WSTG-SESS-01` **Session Management Schema** — Analizar cómo se gestionan las sesiones (aleatoriedad y robustez del token).
- [ ] `WSTG-SESS-02` **Cookies Attributes** — Revisar flags de cookies: `HttpOnly`, `Secure`, `SameSite`.
- [ ] `WSTG-SESS-03` **Session Fixation** — Que el ID de sesión cambie tras autenticarse.
- [ ] `WSTG-SESS-04` **Exposed Session Variables** — Que el token no viaje en la URL ni en campos visibles.
- [ ] `WSTG-SESS-05` **CSRF** — Forzar acciones en nombre del usuario por falta de token anti-CSRF.
- [ ] `WSTG-SESS-06` **Logout Functionality** — Que el logout invalide la sesión de verdad en servidor.
- [ ] `WSTG-SESS-07` **Session Timeout** — Que la sesión expire tras inactividad.
- [ ] `WSTG-SESS-08` **Session Puzzling** — Uso incorrecto de variables de sesión que permita saltarse pasos.
- [ ] `WSTG-SESS-09` **Session Hijacking** — Robo o reutilización de la sesión de otro usuario.
