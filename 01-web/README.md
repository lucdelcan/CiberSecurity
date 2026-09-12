# 01 · Web — Fichas por vulnerabilidad

El catálogo técnico: **qué es cada vuln, cómo detectarla, explotarla y remediarla.** Complementa a la metodología (`00-metodologia/` = proceso) y a los cheatsheets (`04-cheatsheets/` = payloads para pegar).

## Regla de organización

- **Los cajones (carpetas) son categorías** — pocas y estables.
- **Cada vulnerabilidad concreta es un fichero** dentro de su cajón (ej. `injection/sqli.md`, `xss/dom.md`).
- Vuln nueva → nuevo `.md` dentro del cajón que toque. Solo se añade carpeta si aparece una *clase* nueva.
- Toda ficha se crea copiando `_plantilla-vuln.md` (lleva el campo `WSTG-ID` para cruzar con las checklists).

## Cajones y mapeo con WSTG

| Cajón | Qué mete | WSTG |
|---|---|---|
| `injection/` | SQLi, NoSQLi, command, LDAP, XPath, code injection | INPV-05/06/09/11/12 |
| `xss/` | reflected, stored, DOM | INPV-01/02, CLNT-01 |
| `ssrf/` | Server-Side Request Forgery | INPV-19 |
| `xxe/` | XML External Entities | INPV-07 |
| `ssti/` | Server-Side Template Injection | INPV-18 |
| `deserializacion/` | deserialización insegura | — |
| `file-upload/` | subida de ficheros maliciosos/inesperados | BUSL-08/09 |
| `request-smuggling/` | HTTP request smuggling / splitting | INPV-15 |
| `auth/` | login bypass, JWT, OAuth/SSO, MFA, reset, fuerza bruta | AUTHN-\* |
| `session-management/` | cookies, fixation, hijacking, timeout | SESS-\* |
| `access-control/` | IDOR, path traversal, escalada de privilegios | AUTHZ-\* |
| `csrf/` | Cross-Site Request Forgery | SESS-05 |
| `cors/` | CORS mal configurado | CLNT-07 |
| `open-redirect/` | redirecciones abiertas | CLNT-04 |
| `business-logic/` | fallos de lógica de negocio | BUSL-\* |
| `cryptography/` | TLS débil, padding oracle, cifrado débil | CRYP-\* |
| `info-disclosure/` | fugas de info, errores verbosos, metafiles | INFO-\*, ERR-\* |
| `security-misconfig/` | cabeceras, configs por defecto, métodos HTTP | CONF-\* |
| `race-conditions/` | condiciones de carrera | BUSL-04 |
| `web-cache/` | cache poisoning / deception | — |
| `client-side/` | clickjacking, postMessage, WebSockets, prototype pollution, browser storage | CLNT-\* |
| `api/` | REST y GraphQL (+ OWASP API Top 10) | APIT-01 |

## Cómo se relaciona con el resto del repo

Para cada vuln, las cuatro piezas se enlazan entre sí:

1. **Ficha** (aquí) — entiéndela.
2. **Checklist** (`00-metodologia/06-checklists/`) — no olvides probarla.
3. **Cheatsheet** (`04-cheatsheets/por-vuln/`) — payloads para pegar.
4. **Redacción** (`00-metodologia/05-informe/catalogo-redacciones.md`) — cómo reportarla.
