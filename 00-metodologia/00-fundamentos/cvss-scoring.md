# Guía de scoring CVSS

Cómo puntuar un hallazgo de forma **consistente y defendible**. CVSS (Common Vulnerability Scoring System, de FIRST) traduce las características de una vuln a un número 0.0–10.0 y una severidad. Lo importante no es el número, es que puedas **justificar cada métrica** ante el cliente.

- **v3.1** — el estándar de facto en la industria; es el que usa `../05-informe/plantilla-finding.md`.
- **v4.0** — la versión actual (FIRST, nov 2023). Adopción creciente. Al final se explica qué cambia.

## Severidad (igual en 3.1 y 4.0)

| Rango | Severidad |
|---|---|
| 0.0 | None |
| 0.1 – 3.9 | Low |
| 4.0 – 6.9 | Medium |
| 7.0 – 8.9 | High |
| 9.0 – 10.0 | Critical |

---

## CVSS 3.1 — métricas Base

El vector se escribe: `CVSS:3.1/AV:_/AC:_/PR:_/UI:_/S:_/C:_/I:_/A:_`

**Explotabilidad**

- **AV — Attack Vector:** ¿desde dónde se explota?
  - `N` Network (remoto por red) · `A` Adjacent (misma subred) · `L` Local · `P` Physical
  - *Web: casi siempre `N`.*
- **AC — Attack Complexity:** ¿hacen falta condiciones especiales?
  - `L` Low (repetible siempre) · `H` High (depende de algo fuera del control del atacante)
- **PR — Privileges Required:** ¿qué privilegios necesita el atacante antes?
  - `N` None (sin login) · `L` Low (usuario normal) · `H` High (admin)
- **UI — User Interaction:** ¿necesita que la víctima haga algo?
  - `N` None · `R` Required (ej. que haga clic → típico en XSS reflejado, CSRF)

**Alcance e impacto**

- **S — Scope:** ¿el impacto salta a otro componente de seguridad?
  - `U` Unchanged · `C` Changed (ej. XSS que compromete el navegador/otra app → `C`)
- **C / I / A — Confidentiality / Integrity / Availability:**
  - Cada una: `H` High · `L` Low · `N` None

### Ejemplos rápidos (web)

| Vuln típica | Vector orientativo | Score aprox. |
|---|---|---|
| SQLi no autenticada con volcado de BD | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` | 9.8 Critical |
| XSS reflejado | `AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N` | 6.1 Medium |
| IDOR que expone datos de otro usuario | `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N` | 6.5 Medium |
| SSRF a metadata del cloud | `AV:N/AC:L/PR:L/UI:N/S:C/C:H/I:L/A:N` | 8.5 High |
| Cabecera de seguridad ausente | `AV:N/AC:H/PR:N/UI:R/S:U/C:L/I:N/A:N` | 3.1 Low |

> Son orientativos: ajusta según el caso real. Lo que te evaluarán es el **razonamiento**, no que copies estos.

---

## Consejos para puntuar consistente

- **Puntúa el caso realista, no el peor teórico.** Si el IDOR solo expone el email, C:L, no C:H.
- **PR según lo que hace falta de verdad.** Si necesitas estar logueado, es `PR:L`, no `PR:N`.
- **Scope `C` con cuidado:** solo cuando el impacto cruza a otro componente/autoridad de seguridad. Es lo que más infla el score y lo que más te van a cuestionar.
- **Sé coherente entre findings.** Dos vulns iguales, mismo vector. Un catálogo de vectores reutilizables ayuda (guárdalos en `../05-informe/`).
- **El número no manda sobre el contexto.** Puedes subir/bajar la severidad final con las métricas Environmental si el contexto del cliente lo justifica, y explicándolo.

---

## CVSS 4.0 — qué cambia

Misma escala y bandas, pero más granular y con nueva nomenclatura:

- **Nomenclatura:** el score ya no es solo "Base". Ahora: **CVSS-B** (Base), **CVSS-BT** (+Threat), **CVSS-BE** (+Environmental), **CVSS-BTE** (todo). Di siempre cuál reportas.
- **Fuera `Scope`**, entra **AT — Attack Requirements** (`N`/`P`): condiciones del entorno que deben darse.
- **UI más granular:** `N` None · `P` Passive · `A` Active.
- **Impacto separado en dos:** sistema vulnerable (**VC/VI/VA**) y sistema posterior/subsecuente (**SC/SI/SA**) — sustituye la idea de Scope.
- **Threat metric:** **E — Exploit Maturity** (si hay exploit público/activo).
- **Supplemental (informativas, no puntúan):** Safety, Automatable, Recovery, Value Density… dan contexto extra.

**¿Cuál uso?** El que pida el cliente/tu plantilla de informe. Hoy 3.1 sigue siendo lo más habitual; si el cliente ya trabaja en 4.0, úsalo. Lo importante: **indica siempre la versión y el vector completo**, para que el score sea reproducible.

## Calculadoras

- CVSS 3.1: https://www.first.org/cvss/calculator/3.1
- CVSS 4.0: https://www.first.org/cvss/calculator/4.0
- Especificación: https://www.first.org/cvss/
