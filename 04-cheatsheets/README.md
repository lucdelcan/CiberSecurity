# 04 · Cheatsheets

Comandos y payloads listos para copiar. Organizados con los mismos ejes que el resto del repo para que el mapa mental sea uno solo.

## Índice

### `por-fase/` — siguen la metodología (`00-metodologia/`)

| Cheatsheet | Contenido |
|---|---|
| [01-recon](por-fase/01-recon.md) | Subdominios, hosts vivos, puertos, fingerprinting, dirbusting, dorks |
| [02-enumeration](por-fase/02-enumeration.md) | Crawling, content discovery, parámetros, análisis JS, APIs, vhosts |
| [03-explotacion](por-fase/03-explotacion.md) | Utilidades genéricas: listeners, msfvenom, servir/descargar ficheros, encoding |
| [04-post-explotacion](por-fase/04-post-explotacion.md) | Situational awareness Linux/Windows, enum de privesc, búsqueda de loot, limpieza |

### `por-vuln/` — payloads por tipo de bug (espejan `01-web/`)

| Cheatsheet | Contenido |
|---|---|
| [sqli](por-vuln/sqli.md) | Detección, comentarios, auth bypass, union, error, blind (boolean/time), sqlmap |
| [xss](por-vuln/xss.md) | Prueba por contexto, evasión de filtros, DOM sinks, robo de cookie |
| [command-injection](por-vuln/command-injection.md) | Operadores, OOB/blind, evasión, reverse shell |
| [ssrf](por-vuln/ssrf.md) | Destinos internos, metadata cloud, bypass de filtros, OOB |
| [ssti](por-vuln/ssti.md) | Detección polyglot, RCE por motor (Jinja2, Twig, Freemarker) |
| [xxe](por-vuln/xxe.md) | Lectura de ficheros, SSRF, blind OOB, wrappers PHP |
| [file-inclusion](por-vuln/file-inclusion.md) | LFI/RFI, path traversal, bypass, LFI a RCE |
| [idor](por-vuln/idor.md) | Qué manipular, técnica con 2 cuentas, enumeración |
| [csrf](por-vuln/csrf.md) | PoC formulario/fetch, bypass de token |
| [file-upload](por-vuln/file-upload.md) | Webshell, bypass de extensión/Content-Type/magic bytes |
| [ldap](por-vuln/ldap.md) | Detección, auth bypass, extracción ciega |
| [xpath](por-vuln/xpath.md) | Detección, auth bypass, extracción ciega |
| [graphql](por-vuln/graphql.md) | Introspección, enumeración, BOLA, batching |

### `transversal/` — no cuelgan de una fase ni de una vuln

| Cheatsheet | Contenido |
|---|---|
| [reverse-shells](transversal/reverse-shells.md) | Reverse shells por lenguaje/entorno |
| [comandos-rapidos](transversal/comandos-rapidos.md) | One-liners de uso frecuente |
| [wordlists](transversal/wordlists.md) | Rutas y notas sobre wordlists |
| [tty-upgrade](transversal/tty-upgrade.md) | Estabilizar una shell a TTY completa |

## Convenciones

- **Un fichero por tema**, nunca un mega-archivo. Nombres en kebab-case y predecibles.
- **Cheatsheet ≠ ficha de vuln.** Aquí van payloads para *pegar*; la *explicación* (qué es, cómo detectar, remediar) vive en `01-web/`. Se enlazan entre sí, no se duplican.
- Al añadir un cheatsheet, **añádelo también a este índice**. Es la tabla de contenidos del repo.
- Todo comando se usa **solo sobre objetivos autorizados**.
