# 00 · Metodología

El **proceso** de un pentest, reutilizable en cualquier engagement. Aquí va el *cómo procedo*, no el *cómo exploto X* (eso vive en `01-web/`).

Regla: si sirve para cualquier target → aquí. Si sirve para un tipo de vuln concreto → `01-web/`.

## Flujo

1. **recon/** — descubrimiento externo (OSINT, subdominios, hosts, fingerprinting).
2. **enumeration/** — mapeo de la aplicación por dentro (endpoints, parámetros, APIs).
3. **explotacion/** — criterio y estrategia de explotación (priorización, encadenado, impacto).
4. **post-explotacion/** — qué hacer una vez dentro, dentro del alcance.
5. **informe/** — plantillas de report, scoring CVSS, catálogo de findings.
6. **checklists/** — listas accionables (WSTG + propias) para no dejarse nada.
