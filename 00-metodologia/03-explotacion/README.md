# Explotación

**No dupliques `01-web/`.** Aquí no va "cómo exploto un SSRF", va la *estrategia*.

## Qué guardo aquí

- **Priorización**: cómo decido qué atacar primero (impacto vs. esfuerzo, acceso a datos, RCE potencial).
- **Encadenado**: cómo combino hallazgos menores en algo con impacto real (p.ej. IDOR + info leak → takeover).
- **Impacto real**: cómo demuestro el impacto de negocio, no solo el bug técnico.
- **Explotación segura en cliente real**: qué es aceptable, cómo hacer PoC sin romper producción ni tocar datos reales.

> El "cómo" técnico de cada vuln vive en `01-web/`. Esto es el "cuándo, en qué orden y hasta dónde".
