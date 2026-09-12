# 00 · Metodología

El **proceso** de un pentest, reutilizable en cualquier engagement. Aquí va el *cómo procedo*, no el *cómo exploto X* (eso vive en `01-web/`).

Regla: si sirve para cualquier target → aquí. Si sirve para un tipo de vuln concreto → `01-web/`.

Las subcarpetas van numeradas porque hay una **secuencia** real. (En catálogos como `01-web/` no se numera: son fichas sueltas.)

## Flujo

0. **00-fundamentos/** — lo que hay que saber *antes* de empezar: estándares y metodologías (WSTG, ASVS…), glosario, scoring CVSS, modelado de amenazas.
1. **01-recon/** — descubrimiento externo (OSINT, subdominios, hosts, fingerprinting).
2. **02-enumeration/** — mapeo de la aplicación por dentro (endpoints, parámetros, APIs).
3. **03-explotacion/** — criterio y estrategia de explotación (priorización, encadenado, impacto).
4. **04-post-explotacion/** — qué hacer una vez dentro, dentro del alcance.
5. **05-informe/** — plantillas de report, scoring CVSS, catálogo de findings.
6. **06-checklists/** — listas accionables (WSTG + propias). Transversal: se usa durante todo el proceso.
