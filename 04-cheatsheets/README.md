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
| _(pendiente)_ | sqli, xss, ssrf... |

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
