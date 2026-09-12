# File Upload Attacks — Índice

- **WSTG:** `WSTG-BUSL-08` (tipos inesperados), `WSTG-BUSL-09` (ficheros maliciosos)
- **OWASP Top 10:** `A04:2021 – Insecure Design` / `A03:2021 – Injection`
- **Alias:** subida de ficheros insegura

## Qué es

La app permite subir ficheros sin validar bien tipo, contenido o ubicación. El atacante sube un fichero malicioso (típicamente webshell) y, si consigue ejecutarlo, obtiene RCE.

## Método base

1. Localiza toda subida (avatar, adjuntos, importaciones).
2. Comprueba qué valida: extensión, `Content-Type`, magic bytes, y **dónde** cae el fichero (¿ruta accesible/ejecutable por web?).
3. Sube y accede a la URL del fichero.

## Fichas a fondo

| Tema | Ficha |
|---|---|
| Bypass de validaciones | [bypass.md](bypass.md) |
| De subida a RCE y otras variantes | [to-rce.md](to-rce.md) |

## Impacto

RCE y compromiso del servidor (crítico) si la webshell es ejecutable; XSS/XXE almacenado o DoS en otros casos.

## Remediación (común)

- Lista blanca de extensiones + validación de contenido real (magic bytes).
- Renombrar y guardar **fuera del webroot** o en almacenamiento sin ejecución.
- Servir con `Content-Disposition`, sin permisos de ejecución; límite de tamaño y antimalware.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/file-upload.md`
- Checklist: `../../00-metodologia/06-checklists/10-business-logic.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-BUSL-09` · CWE-434 · OWASP File Upload Cheat Sheet
