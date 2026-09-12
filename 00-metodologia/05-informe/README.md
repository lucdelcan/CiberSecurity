# 05 · Informe

Todo lo relacionado con el reporte al cliente. Cada vez que redactas un buen finding, abstráelo y guárdalo aquí para reutilizar.

## Contenido

- `plantilla-finding.md` — estructura estándar de un hallazgo.
- `estructura-informe.md` — secciones del informe y a quién va dirigida cada una.
- `catalogo-redacciones.md` — descripciones, impactos y remediaciones reutilizables por tipo de vuln.
- Scoring CVSS → vive en `../00-fundamentos/cvss-scoring.md`.

## Buenas prácticas de redacción

- **Doble audiencia:** el resumen ejecutivo es para negocio (sin tecnicismos); los hallazgos detallados, para el equipo técnico.
- Separa **hallazgo técnico** de **riesgo de negocio**.
- La remediación debe ser **accionable y concreta**, no genérica.
- **Evidencia mínima suficiente:** que se entienda, sin exponer datos sensibles reales.
- **Coherencia:** mismo tipo de vuln → misma redacción base y mismo vector CVSS. Este catálogo es lo que te lo garantiza.
