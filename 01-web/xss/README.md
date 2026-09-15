# Cross-Site Scripting (XSS)

Ejecución de JS en el navegador de la víctima por falta de codificación de salida.

> Cada ficha: qué es · cómo detectarla · cómo explotarla · impacto · remediación · referencias.

## Fichas

- [xss.md](xss.md) — **XSS** — índice (los tres tipos + remediación)
- [reflected.md](reflected.md) — Reflected XSS (contextos de inyección)
- [stored.md](stored.md) — Stored XSS (incluye blind)
- [dom.md](dom.md) — DOM-based XSS (sources/sinks)
- [bypass.md](bypass.md) — Evasión de filtros / WAF

## Relación con el resto del repo

- **Checklist:** `../../00-metodologia/06-checklists/07-input-validation.md`
- **Payloads:** `../../04-cheatsheets/por-vuln/`
- **Redacción para informe:** `../../00-metodologia/05-informe/catalogo-redacciones.md`
- **Nueva ficha:** copia `../_plantilla-vuln.md` en este cajón.
