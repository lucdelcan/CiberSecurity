# Server-Side Template Injection (SSTI) — Índice

- **WSTG:** `WSTG-INPV-18`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** SSTI

## Qué es

La app inserta entrada del usuario en una plantilla de servidor que luego se renderiza. El atacante inyecta sintaxis del motor, que se evalúa en el servidor → con frecuencia RCE.

## Detección (común)

Inyecta operaciones y mira si se evalúan:
```
${7*7}  {{7*7}}  <%= 7*7 %>  #{7*7}  ${{7*7}}  *{7*7}
```
Si devuelve `49`, hay evaluación server-side. Identifica el motor según qué sintaxis funciona y cuál da error.

## Fichas por motor

| Motor | Ficha |
|---|---|
| Jinja2 / Flask (Python) | [jinja2.md](jinja2.md) |
| Twig (PHP) | [twig.md](twig.md) |
| Freemarker (Java) | [freemarker.md](freemarker.md) |

## Impacto

Habitualmente RCE en el servidor → compromiso total. Crítico.

## Remediación (común)

- No pasar entrada del usuario como parte de la plantilla; usarla solo como **datos** (contexto).
- Sandbox del motor (con cautela) y lógica de plantilla mínima.
- Lista blanca/escape de la entrada.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/ssti.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-INPV-18` · CWE-1336 · PortSwigger — SSTI
