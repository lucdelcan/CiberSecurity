# Login Brute Forcing

- **WSTG:** `WSTG-AUTHN-03` (lock out), `WSTG-IDNT-04` (enumeración)
- **OWASP Top 10:** `A07:2021 – Identification and Authentication Failures`
- **Alias:** fuerza bruta, credential stuffing, password spraying

## Qué es

La ausencia de protección contra intentos automatizados permite probar grandes volúmenes de credenciales hasta acertar (fuerza bruta), reutilizar credenciales filtradas (credential stuffing) o probar una contraseña común contra muchos usuarios (password spraying).

## Cómo detectarla

- ¿Hay rate limiting, bloqueo o CAPTCHA tras varios fallos?
- **Enumeración de usuarios:** mensajes o tiempos distintos entre "usuario no existe" y "contraseña incorrecta" → permite acotar el ataque.
- Revisa también endpoints secundarios (API, app móvil) que quizá no apliquen el mismo control.

## Cómo explotarla

1. Primero enumera usuarios válidos si es posible.
2. Ataca con diccionarios adaptados (contraseñas comunes, patrones de la organización).
3. Password spraying para evitar bloqueos por cuenta.
4. Reutiliza brechas conocidas (credential stuffing).

## Impacto

Toma de cuentas, especialmente con contraseñas débiles o reutilizadas.

## Cómo remediar

- Rate limiting y bloqueo temporal progresivo; CAPTCHA tras varios fallos.
- MFA (mitiga la mayoría de estos ataques).
- Mensajes de error genéricos y tiempos constantes (evitar enumeración).
- Detección de credenciales filtradas y monitorización de accesos anómalos.

## Referencias

- OWASP WSTG `WSTG-AUTHN-03`, `WSTG-IDNT-04` · CWE-307

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/04-authentication.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
