# Server-Side Request Forgery (SSRF) — Índice

- **WSTG:** `WSTG-INPV-19`
- **OWASP Top 10:** `A10:2021 – SSRF`
- **Alias:** SSRF

## Qué es

La aplicación hace una petición de red a una URL que controla el usuario, sin restringir el destino. El atacante consigue que **el servidor** haga peticiones en su nombre a recursos internos no expuestos.

## Dónde aparece

Webhooks, importadores de URL, generadores de PDF/imágenes, previsualizadores de enlaces, integraciones, parámetros `?url=`, `?dest=`, `?feed=`, `?image=`.

## Fichas a fondo

| Tema | Ficha |
|---|---|
| SSRF ciego y exfiltración OOB | [blind-oob.md](blind-oob.md) |
| Metadatos cloud (AWS/GCP/Azure) | [cloud-metadata.md](cloud-metadata.md) |
| Evasión de filtros anti-SSRF | [filter-bypass.md](filter-bypass.md) |

## Impacto

Acceso a recursos internos, robo de credenciales cloud (→ compromiso de la infra), escaneo/pivote a la red interna. A menudo alto/crítico.

## Remediación (común)

- Lista blanca de dominios/IPs de destino permitidos.
- Bloquear rangos internos y la IP de metadatos; validar **tras** la resolución DNS.
- Deshabilitar redirecciones y esquemas innecesarios (`file://`, `gopher://`).
- Respuestas/errores que no revelen el resultado interno.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/ssrf.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: OWASP WSTG `WSTG-INPV-19` · CWE-918 · PortSwigger — SSRF
