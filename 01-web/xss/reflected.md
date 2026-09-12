# XSS Reflejado (Reflected)

- **WSTG:** `WSTG-INPV-01`
- **OWASP Top 10:** `A03:2021 – Injection`
- Ver índice: [xss.md](xss.md)

## Qué es

El payload viaja en la petición (parámetro de URL, campo de formulario, cabecera) y la aplicación lo **devuelve sin codificar en la respuesta inmediata**. No se almacena: solo afecta a quien envía esa petición, por lo que se explota engañando a la víctima para que abra un enlace/formulario preparado.

## Cómo detectarla

1. Inyecta un marcador único e inocuo (`cl4ude123`) en cada parámetro y búscalo en la respuesta.
2. Si aparece **sin codificar**, analiza en qué **contexto** cae (ver más abajo).
3. Prueba caracteres clave según contexto: `< > " ' / =` y observa cuáles llegan literales.
4. Confirma con un payload no destructivo: `<script>alert(document.domain)</script>` o un vector adaptado al contexto/filtro.

Revisa **todos** los puntos de entrada reflejados: parámetros GET/POST, fragmentos de URL, cabeceras reflejadas (User-Agent, Referer), y mensajes de error.

## Contextos de inyección (clave del reflected)

El payload correcto depende de dónde caiga tu entrada:

- **Entre etiquetas HTML** (`<div>AQUÍ</div>`): inyecta una etiqueta nueva → `<script>…</script>`, `<img src=x onerror=…>`.
- **Dentro de un atributo** (`value="AQUÍ"`): cierra la comilla y añade un handler → `" autofocus onfocus=alert(1) x="`.
- **Dentro de `<script>`** (string JS): rompe el string → `';alert(1)//` o cierra la etiqueta → `</script><script>alert(1)</script>`.
- **En una URL/href**: `javascript:alert(1)`.

## Cómo explotarla

1. Identifica el contexto y construye el payload que **escapa** de él.
2. Empaqueta la petición en un enlace o formulario auto-enviado que la víctima abra.
3. Impacto real: robar cookie de sesión (si no `HttpOnly`), token CSRF, o ejecutar acciones autenticadas. PoC de exfiltración en `../../04-cheatsheets/por-vuln/xss.md`.

## Impacto

Compromiso de la sesión de la víctima que abre el enlace. Requiere interacción (clic), por eso suele puntuar algo menos que el stored, salvo que afecte a usuarios privilegiados.

## Cómo remediar

- Codificar la salida según el contexto donde se refleje la entrada.
- CSP y `HttpOnly`.
- No reflejar entrada innecesaria (cabeceras, mensajes de error).

## Referencias

- OWASP WSTG `WSTG-INPV-01` · CWE-79 · PortSwigger — Reflected XSS
