# XSS — Evasión de filtros y WAF

Transversal a reflected/stored/DOM. Cuando la entrada se refleja pero un filtro/WAF bloquea el payload básico. Ver índice: [xss.md](xss.md). Payloads en `../../04-cheatsheets/por-vuln/xss.md`. **Solo sobre objetivos autorizados.**

## Metodología de bypass

1. **Averigua qué filtra:** manda cada carácter/palabra por separado (`<`, `>`, `"`, `script`, `onerror`, `alert`) y observa cuáles pasan y cuáles se bloquean/codifican.
2. **Adáptate a lo que sí pasa.** El bypass consiste en construir un vector con los caracteres/etiquetas permitidos.

## Técnicas frecuentes

- **Etiquetas alternativas** si `<script>` está bloqueado: `<img>`, `<svg>`, `<body>`, `<details>`, `<iframe>`.
- **Event handlers** en vez de `<script>`: `onerror`, `onload`, `onfocus`, `onpointerover`, `ontoggle`.
- **Mayúsculas/mezcla** si el filtro es case-sensitive: `<sCrIpT>`, `oNeRrOr`.
- **Sin paréntesis** si filtran `()`: `alert\`1\``, o `onerror=alert` con throw.
- **Sin comillas** si filtran `"`/`'`: usar entidades o backticks.
- **Codificación:** HTML entities (`&#x61;`), URL/doble URL, unicode; útil según dónde se decodifique.
- **Ofuscación de JS:** `eval(atob('...'))`, `top['al'+'ert'](1)`, notación con corchetes.
- **Romper palabras clave** que el filtro busca literalmente: comentarios, caracteres nulos, etc.

## Contexto manda

Un bypass solo funciona si encaja en el **contexto** de salida (etiqueta, atributo, JS, URL). Combina la técnica de evasión con el escape del contexto correspondiente (ver [reflected.md](reflected.md)).

## Frente a CSP

- Revisa la política: ¿permite inline? ¿`unsafe-eval`? ¿orígenes laxos o `data:`?
- Busca endpoints permitidos por la CSP que sirvan JS (JSONP, librerías) para cargar tu código.
- Si la CSP está bien hecha y no hay bypass, repórtalo como mitigación efectiva.

## Referencias

- OWASP XSS Filter Evasion Cheat Sheet · PortSwigger — XSS contexts & WAF bypass
