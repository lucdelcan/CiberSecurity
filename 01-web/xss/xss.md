# Cross-Site Scripting (XSS) — Índice

- **WSTG:** `WSTG-INPV-01` (reflected), `WSTG-INPV-02` (stored), `WSTG-CLNT-01` (DOM)
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** XSS

## Qué es

La aplicación incorpora entrada del usuario en una página sin codificarla según el contexto, de modo que el navegador la interpreta como código y ejecuta **JavaScript** en el contexto de la víctima (su origen, su sesión). Con eso un atacante actúa como si fuera la víctima dentro de la aplicación.

## Los tres tipos (fichas a fondo)

| Tipo | Dónde ocurre | Ficha |
|---|---|---|
| **Reflected** | El payload viaja en la petición y se refleja en la respuesta inmediata | [reflected.md](reflected.md) |
| **Stored** | El payload se guarda en el servidor y se sirve a otros usuarios | [stored.md](stored.md) |
| **DOM-based** | La inyección ocurre en el propio JavaScript del cliente | [dom.md](dom.md) |

Y transversal a los tres:

- **Evasión de filtros / WAF:** [bypass.md](bypass.md)

## Impacto (común a los tres)

Ejecución de código en la sesión de la víctima: robo de sesión/cookies, acciones en su nombre, keylogging, phishing en contexto, y — si cae en un panel de administración — escalada hacia compromiso total.

## Remediación (común)

- **Codificar la salida según el contexto** (HTML, atributo, JS, URL) — defensa principal.
- **Content Security Policy (CSP)** como defensa en profundidad.
- Cookies de sesión `HttpOnly`.
- En cliente: evitar sinks peligrosos, usar `textContent` en vez de `innerHTML`, sanitizar con DOMPurify.
- Validación de entrada como capa adicional (no sustituye a la codificación de salida).

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/xss.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: OWASP XSS Prevention Cheat Sheet · PortSwigger — Cross-site scripting · CWE-79
