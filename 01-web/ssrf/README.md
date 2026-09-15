# Server-Side Request Forgery (SSRF)

Forzar al servidor a hacer peticiones a destinos que elige el atacante.

> Cada ficha: qué es · cómo detectarla · cómo explotarla · impacto · remediación · referencias.

## Fichas

- [ssrf.md](ssrf.md) — **SSRF** — índice
- [blind-oob.md](blind-oob.md) — SSRF ciego y exfiltración OOB
- [cloud-metadata.md](cloud-metadata.md) — Metadatos cloud (AWS/GCP/Azure)
- [filter-bypass.md](filter-bypass.md) — Evasión de filtros anti-SSRF

## Relación con el resto del repo

- **Checklist:** `../../00-metodologia/06-checklists/07-input-validation.md`
- **Payloads:** `../../04-cheatsheets/por-vuln/`
- **Redacción para informe:** `../../00-metodologia/05-informe/catalogo-redacciones.md`
- **Nueva ficha:** copia `../_plantilla-vuln.md` en este cajón.
