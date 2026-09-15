# Server-Side Template Injection (SSTI)

Inyección en plantillas de servidor; suele llevar a RCE.

> Cada ficha: qué es · cómo detectarla · cómo explotarla · impacto · remediación · referencias.

## Fichas

- [ssti.md](ssti.md) — **SSTI** — índice (detección + por motor)
- [jinja2.md](jinja2.md) — Jinja2 / Flask (Python)
- [twig.md](twig.md) — Twig (PHP)
- [freemarker.md](freemarker.md) — Freemarker (Java)

## Relación con el resto del repo

- **Checklist:** `../../00-metodologia/06-checklists/07-input-validation.md`
- **Payloads:** `../../04-cheatsheets/por-vuln/`
- **Redacción para informe:** `../../00-metodologia/05-informe/catalogo-redacciones.md`
- **Nueva ficha:** copia `../_plantilla-vuln.md` en este cajón.
