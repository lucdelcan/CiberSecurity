# File Inclusion (LFI / RFI) — Índice

- **WSTG:** `WSTG-INPV-11` (11.1 LFI, 11.2 RFI) · relacionado con `WSTG-AUTHZ-01`
- **OWASP Top 10:** `A03:2021 – Injection` / `A01:2021 – Broken Access Control`
- **Alias:** Local/Remote File Inclusion

## Qué es

La aplicación incluye un fichero cuya ruta procede de entrada del usuario sin validar. **LFI** incluye ficheros locales; **RFI** incluye uno remoto controlado por el atacante. Puede derivar en lectura de ficheros sensibles o en ejecución de código.

## Dónde aparece

Parámetros que cargan páginas/plantillas/idiomas: `?page=`, `?file=`, `?lang=`, `?template=`, `?include=`.

## Fichas a fondo

| Tema | Ficha |
|---|---|
| LFI (lectura) y bypass | [lfi.md](lfi.md) |
| RFI (inclusión remota) | [rfi.md](rfi.md) |
| LFI → RCE | [lfi-to-rce.md](lfi-to-rce.md) |

Traversal "solo lectura" sin inclusión → ver `../access-control/path-traversal.md`.

## Impacto

Desde divulgación de código y ficheros sensibles hasta RCE (crítico).

## Remediación (común)

- No usar entrada del usuario para rutas; lista blanca/índice de ficheros permitidos.
- Deshabilitar inclusión remota (`allow_url_include=Off`).
- Canonizar y confinar rutas (`basename()`, chroot).

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/file-inclusion.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-INPV-11` · CWE-98/CWE-22 · PortSwigger — File path traversal
