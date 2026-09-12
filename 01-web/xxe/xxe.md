# XML External Entity (XXE) — Índice

- **WSTG:** `WSTG-INPV-07`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** XXE, inyección de entidades externas XML

## Qué es

Un parser XML procesa entrada con entidades externas habilitadas. El atacante define entidades que hacen al parser leer ficheros locales, hacer peticiones de red (SSRF) o provocar DoS.

## Dónde aparece

Cualquier endpoint que acepte XML: SOAP, APIs XML, y ficheros que **son XML por dentro** (`.docx`, `.xlsx`, `.svg`, `.xml`).

## Fichas a fondo

| Tema | Ficha |
|---|---|
| XXE clásico (in-band) | [basic.md](basic.md) |
| XXE ciego / OOB (DTD externa) | [blind-oob.md](blind-oob.md) |
| Variantes (SVG, OOXML, SOAP, XInclude) | [variants.md](variants.md) |

## Impacto

Lectura de ficheros sensibles, SSRF a la red interna, DoS; en casos concretos escala a RCE.

## Remediación (común)

- Deshabilitar DTD y entidades externas en el parser (config segura por defecto).
- Usar formatos menos complejos (JSON) donde sea posible.
- Parsers actualizados con resolución de entidades externas desactivada.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/xxe.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-INPV-07` · CWE-611 · OWASP XXE Prevention Cheat Sheet
