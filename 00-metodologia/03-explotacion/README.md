# 03 · Explotación — Estrategia

**No dupliques `01-web/`.** Aquí no va "cómo exploto un SSRF" (eso es una ficha de vuln). Aquí va el *criterio*: qué atacas primero, cómo combinas hallazgos y cómo demuestras impacto real sin romper nada.

Punto de partida: el **mapa de superficie de ataque** que salió de `02-enumeration/` (endpoints, parámetros, roles, candidatos jugosos).

---

## 1. Priorización — ¿qué ataco primero?

No pruebes todo a lo loco. Ordena por **impacto × probabilidad**, buscando quick wins:

- **Impacto alto primero:** lo que lleva a RCE, acceso a datos sensibles, bypass de autenticación o toma de cuentas.
- **Quick wins:** cosas rápidas de confirmar (default creds, ficheros expuestos, `.git/`, endpoints admin sin auth).
- **Sigue el dato:** los puntos de entrada que tocan la BD, el sistema de ficheros o llaman a otros servicios son los más rentables.
- **Aparca lo de bajo impacto** (cabeceras faltantes, autocomplete) para el barrido final; no gastes el tiempo bueno ahí.

---

## 2. Encadenado de vulnerabilidades

El impacto real casi nunca es un bug suelto, es la **cadena**. Piensa siempre "¿esto a dónde me lleva?":

- Info leak (IDs, tokens en JS) **+** IDOR → **account takeover**.
- SSRF → metadata del cloud (169.254.169.254) → **credenciales** → acceso a infra.
- LFI **+** log poisoning → **RCE**.
- XSS almacenado en panel admin → robo de sesión de admin → **escalada**.
- Subida de fichero + path predecible → **webshell**.

Documenta la cadena entera: es lo que convierte un "medio" en un "crítico" en el informe.

---

## 3. Demostrar impacto real (no solo el bug técnico)

Un finding vale por lo que **significa para el negocio**, no por el payload:

- Traduce "hay SQLi" → "se puede volcar la tabla de usuarios con credenciales".
- Consigue una prueba concreta pero **mínima suficiente** (un registro, no toda la BD; `id` del usuario víctima, no sus datos reales).
- Si demuestras RCE, ejecuta algo inocuo (`id`, `whoami`, `hostname`), no toques nada más.

---

## 4. PoC segura en cliente real ⚠️

Esto separa a un profesional de alguien que rompe producción:

- **No DoS** ni pruebas destructivas sin permiso explícito por escrito.
- **No borres, modifiques ni cifres** datos. Nada de payloads destructivos.
- **No exfiltres datos reales** de usuarios/clientes. Para demostrar acceso basta una muestra acotada o metadatos.
- **Acciones intrusivas** (explotar RCE, pivotar) → confirma que están en alcance antes.
- **Registra todo lo que haces** con marca de tiempo, para poder revertir y para el informe.
- Ante la duda, **para y pregunta** al contacto del cliente.

---

## 5. Entregable de la fase

Hallazgos listos para `05-informe/`:

- Cada vuln confirmada con su **PoC reproducible** (pasos + request/response).
- La **cadena** documentada cuando aplique.
- **Impacto de negocio** redactado.
- Evidencias mínimas y anonimizadas.
- Severidad preliminar (afinas el CVSS en informe → ver `00-fundamentos/`).

---

## Herramientas (referencia)

El "cómo" de cada vuln va en `01-web/`; los payloads por tipo en `04-cheatsheets/por-vuln/`. Utilidades genéricas (listeners, generación de payloads, transferencia de ficheros) en `04-cheatsheets/por-fase/03-explotacion.md`.

## Referencias

- OWASP WSTG (categorías de explotación: `INPV`, `ATHN`, `ATHZ`, `SESS`, `BUSL`…).
- Ver `../00-fundamentos/estandares-y-metodologias.md`.
