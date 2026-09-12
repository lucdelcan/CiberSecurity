# Estructura del informe

Un buen informe tiene **doble audiencia**: dirección (que decide y paga) y el equipo técnico (que corrige). Cada sección apunta a una de las dos. Este es el esqueleto estándar.

## Secciones

### 1. Resumen ejecutivo  — *audiencia: negocio/dirección*
- Sin tecnicismos. En 1 página.
- Qué se evaluó, en qué estado de seguridad está, y el **riesgo de negocio** en lenguaje llano.
- Nº de hallazgos por severidad (idealmente un gráfico) y las 3–5 conclusiones clave.
- Recomendación de alto nivel (prioridades).

### 2. Alcance y objetivos  — *técnico + negocio*
- Qué entró en scope (URLs, IPs, apps, roles) y qué **no**.
- Tipo de test (black/grey/white box), autenticado o no, ventanas y limitaciones.
- Fechas y personas de contacto.

### 3. Metodología  — *técnico*
- Marco seguido (WSTG, PTES…) → ver `../00-fundamentos/`.
- Herramientas principales.
- Cómo se calcula la severidad (CVSS y versión) → `../00-fundamentos/cvss-scoring.md`.

### 4. Resumen de hallazgos  — *ambas*
- Tabla: ID · título · severidad · estado.
- Vista rápida de todo lo encontrado antes del detalle.

### 5. Hallazgos detallados  — *técnico*
- Uno por finding, con la `plantilla-finding.md` (descripción, impacto, PoC, remediación, referencias, CVSS).
- Ordenados por severidad, de mayor a menor.

### 6. Conclusiones y recomendaciones  — *negocio*
- Estado general y patrones detectados (ej. "falta validación de entrada de forma sistemática").
- Recomendaciones priorizadas y, si aplica, plan de remediación por fases.

### 7. Anexos  — *técnico*
- Evidencias extendidas, listados de herramientas, glosario, referencias.

## Tono y estilo

- **Ejecutivo:** claro, orientado a riesgo e impacto, cero jerga.
- **Técnico:** preciso y reproducible; que el dev pueda replicar y corregir.
- **Constructivo:** el informe señala problemas y **cómo arreglarlos**, no culpa.
- **Consistente:** mismos términos, misma estructura de finding, mismo criterio de severidad en todo el documento.

> Formato de salida: el detalle de generar el `.docx` es cosa de tu herramienta de reporting; aquí vive el *contenido y la estructura*.
