# Estándares y metodologías

Antes de "cómo hago recon" conviene tener claro **con qué mapa** trabajas. En web sec hay varios estándares y se confunden mucho porque suenan parecido, pero cada uno responde a una pregunta distinta.

## La idea clave

- **Metodología de testing** → *¿cómo pruebo?* (qué casos ejecuto, en qué orden). → **WSTG**, PTES, OSSTMM.
- **Estándar de verificación** → *¿qué requisitos debe cumplir la app?* (checklist de seguridad a validar). → **ASVS**.
- **Lista de riesgos / concienciación** → *¿qué es lo más peligroso hoy?* (no es una metodología). → **OWASP Top 10**.

En un pentest web tú ejecutas con **WSTG** y, si el cliente lo pide, mides el nivel de cumplimiento contra **ASVS**.

## WSTG — Web Security Testing Guide (OWASP)

- **Qué es:** la guía de referencia de *cómo* testear la seguridad de una app web. Es una metodología de ejecución: te dice qué probar y cómo, categoría por categoría.
- **Versión:** estable **v4.2** (2020-12-03). La **v5.0** está en desarrollo (bleeding-edge en GitHub).
- **Estructura (v4.2):** cada test tiene un ID `WSTG-<CAT>-<nn>`. Categorías:
  - `INFO` Information Gathering (recon) — **esta fase**
  - `CONF` Configuration & Deployment Management
  - `IDNT` Identity Management
  - `ATHN` Authentication
  - `ATHZ` Authorization
  - `SESS` Session Management
  - `INPV` Input Validation (inyecciones, XSS…)
  - `ERR`  Error Handling
  - `CRYP` Cryptography
  - `BUSL` Business Logic
  - `CLNT` Client-side
  - `APIT` API Testing
- **Cómo lo uso:** es la espina dorsal de `06-checklists/`. Cada categoría → una checklist propia.

## ASVS — Application Security Verification Standard (OWASP)

- **Qué es:** un catálogo de **requisitos** de seguridad verificables. No te dice cómo atacar, te dice qué debe cumplirse. Sirve para (1) medir el nivel de seguridad de una app y (2) definir el alcance de un test como "verificar que cumple X requisitos".
- **Versión:** **5.0.0** (30 mayo 2025).
- **Niveles:**
  - **L1** — básico/oportunista. Verificable de forma mayormente black-box. Mínimo para cualquier app.
  - **L2** — estándar. El nivel recomendado para la mayoría de apps que manejan datos sensibles. Requiere algo de acceso (docs, a veces código).
  - **L3** — avanzado. Apps críticas (salud, finanzas, vidas). Verificación exhaustiva.
- **Cómo lo uso:** cuando el cliente quiere "certificar" un nivel, o para dar estructura a la remediación ("esto incumple ASVS V-x.y").

## OWASP Top 10

- **Qué es:** los 10 riesgos más críticos, orientado a **concienciación y priorización**, no a testing exhaustivo. Muy útil para hablar con negocio y clasificar findings, pero **no es una metodología**: no cubre toda la superficie.
- **Uso:** mapear findings a una categoría reconocible en el informe. No sustituye a WSTG.

## Otros que conviene conocer

- **PTES** (Penetration Testing Execution Standard): metodología de pentest **de extremo a extremo** (pre-engagement, intel, threat modeling, análisis de vulns, explotación, post-explotación, reporte). Más amplia que WSTG (no solo web). Buen marco para estructurar todo el engagement.
- **OSSTMM**: metodología de testing de seguridad muy formal y orientada a métricas. Densa; se ve más en entornos que exigen rigor científico/auditoría.
- **NIST SP 800-115**: guía técnica de testing de seguridad del NIST. Referencia habitual en entornos US/compliance.
- **MITRE ATT&CK**: no es una metodología de pentest, es una **base de conocimiento de TTPs** (tácticas y técnicas de adversarios). Útil en post-explotación y para red team / mapear lo que haces a técnicas reales.
- **OWASP MASVS/MASTG**: los equivalentes a ASVS/WSTG pero para **móvil**. Si algún día tocas apps móviles.
- **PCI DSS**: no es metodología de test, es un requisito de compliance (pagos) que a veces obliga a hacer pentest.

## Cómo los combino en la práctica

1. **PTES** como marco general del engagement (las fases de esta carpeta siguen esa idea).
2. **WSTG** para la ejecución técnica web (qué casos pruebo en cada fase).
3. **ASVS** como referencia de requisitos y para dar estructura a la remediación.
4. **OWASP Top 10** para clasificar y comunicar el riesgo en el informe.
5. **MITRE ATT&CK** si hay componente de post-explotación / simulación de adversario.
