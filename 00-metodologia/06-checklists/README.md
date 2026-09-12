# 06 · Checklists

La **OWASP WSTG v4.2** troceada por categoría, un fichero por cada una. Marca `- [x]` conforme avanzas en un engagement.

Cómo usarlas: cópiate estos ficheros (o duplícalos por cliente) y ve marcando. Cada test lleva su **ID oficial** (`WSTG-XXX-NN`) para citarlo en el informe y una **explicación en español** de qué hacer, para que de una lectura sepas por dónde tirar sin abrir la guía.

## Categorías

| # | Categoría | Fichero |
|---|---|---|
| 01 | Information Gathering | [01-info-gathering.md](01-info-gathering.md) |
| 02 | Configuration & Deployment | [02-config-deploy.md](02-config-deploy.md) |
| 03 | Identity Management | [03-identity.md](03-identity.md) |
| 04 | Authentication | [04-authentication.md](04-authentication.md) |
| 05 | Authorization | [05-authorization.md](05-authorization.md) |
| 06 | Session Management | [06-session.md](06-session.md) |
| 07 | Input Validation | [07-input-validation.md](07-input-validation.md) |
| 08 | Error Handling | [08-error-handling.md](08-error-handling.md) |
| 09 | Weak Cryptography | [09-cryptography.md](09-cryptography.md) |
| 10 | Business Logic | [10-business-logic.md](10-business-logic.md) |
| 11 | Client-side | [11-client-side.md](11-client-side.md) |
| 12 | API Testing | [12-api.md](12-api.md) |

## Notas

- Basado en WSTG **v4.2** (estable). La v5.0 está en desarrollo → revisar cuando salga.
- El *proceso* de cada fase está en `../01-recon/` … `../05-informe/`; esto son las listas de verificación.
- El *cómo* técnico de cada vuln vivirá en `../../01-web/`; los comandos, en `../../04-cheatsheets/`.

## Antes de cerrar un engagement

- [ ] Todas las categorías aplicables revisadas.
- [ ] Cada hallazgo con PoC y severidad (CVSS) asignada.
- [ ] Evidencias recogidas y anonimizadas.
- [ ] Informe redactado con resumen ejecutivo.
