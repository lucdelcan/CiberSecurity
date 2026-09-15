# 01 · Web — Fichas por vulnerabilidad

El catálogo técnico: **qué es cada vuln, cómo detectarla, explotarla y remediarla.** Complementa a la metodología (`../00-metodologia/` = proceso) y a los cheatsheets (`../04-cheatsheets/` = payloads).

## Cómo está organizado

- **Cajón (carpeta) = categoría**; **fichero = vulnerabilidad concreta**. Cada cajón tiene su propio `README.md` de índice.
- Vuln nueva → nuevo `.md` en el cajón que toque (copia [`_plantilla-vuln.md`](_plantilla-vuln.md)). Solo se añade carpeta si aparece una *clase* nueva.

## Cajones y mapeo con WSTG

| Cajón | Contenido | WSTG |
|---|---|---|
| [`injection/`](injection/README.md) | SQLi (por motor), command injection, LDAP, XPath, file inclusion | INPV-05/06/09/11/12 |
| [`xss/`](xss/README.md) | reflected, stored, DOM, bypass | INPV-01/02, CLNT-01 |
| [`ssrf/`](ssrf/README.md) | in-band, blind/OOB, cloud metadata, filter bypass | INPV-19 |
| [`xxe/`](xxe/README.md) | básico, blind/OOB, variantes (SVG, OOXML) | INPV-07 |
| [`ssti/`](ssti/README.md) | por motor (Jinja2, Twig, Freemarker) | INPV-18 |
| [`deserializacion/`](deserializacion/README.md) | PHP, Java, Python | — |
| [`file-upload/`](file-upload/README.md) | bypass, a RCE | BUSL-08/09 |
| [`request-smuggling/`](request-smuggling/README.md) | CL.TE, TE.CL, H2 desync | INPV-15 |
| [`auth/`](auth/README.md) | broken auth, JWT, OAuth, brute force | AUTHN-\* |
| [`session-management/`](session-management/README.md) | cookies, fixation, hijacking | SESS-\* |
| [`access-control/`](access-control/README.md) | IDOR, path traversal, privesc | AUTHZ-\* |
| [`csrf/`](csrf/README.md) | token bypass, SameSite bypass | SESS-05 |
| [`cors/`](cors/README.md) | CORS mal configurado | CLNT-07 |
| [`open-redirect/`](open-redirect/README.md) | redirecciones abiertas | CLNT-04 |
| [`business-logic/`](business-logic/README.md) | fallos de lógica de negocio | BUSL-\* |
| [`race-conditions/`](race-conditions/README.md) | single-packet attack | BUSL-04 |
| [`cryptography/`](cryptography/README.md) | TLS débil, padding oracle | CRYP-\* |
| [`info-disclosure/`](info-disclosure/README.md) | fugas, errores, metafiles | INFO-\*, ERR-\* |
| [`security-misconfig/`](security-misconfig/README.md) | cabeceras, configs, métodos HTTP | CONF-\* |
| [`web-cache/`](web-cache/README.md) | poisoning, deception | — |
| [`client-side/`](client-side/README.md) | clickjacking, postMessage… | CLNT-\* |
| [`api/`](api/README.md) | GraphQL, REST (API Top 10) | APIT-01 |

## Las cuatro piezas por vuln

1. **Ficha** (aquí) · 2. **Checklist** (`../00-metodologia/06-checklists/`) · 3. **Cheatsheet** (`../04-cheatsheets/por-vuln/`) · 4. **Redacción** (`../00-metodologia/05-informe/catalogo-redacciones.md`).
