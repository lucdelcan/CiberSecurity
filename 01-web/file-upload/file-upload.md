# File Upload Attacks

- **WSTG:** `WSTG-BUSL-08` (tipos inesperados), `WSTG-BUSL-09` (ficheros maliciosos)
- **OWASP Top 10:** `A04:2021 – Insecure Design` / `A03:2021 – Injection`
- **Alias:** subida de ficheros insegura

## Qué es

La aplicación permite subir ficheros sin validar correctamente tipo, contenido o ubicación. El atacante sube un fichero malicioso (típicamente una webshell) y, si consigue ejecutarlo, obtiene RCE.

## Cómo detectarla

- Localiza toda funcionalidad de subida (avatar, adjuntos, importaciones).
- Prueba extensiones ejecutables según el stack (`.php`, `.phtml`, `.asp`, `.aspx`, `.jsp`).
- Comprueba qué validan: extensión, `Content-Type`, magic bytes, y **dónde** cae el fichero (¿ruta accesible por web?).

## Cómo explotarla

- **Bypass de extensión:** dobles extensiones (`shell.php.jpg`), mayúsculas, extensiones alternativas, null byte (legacy).
- **Bypass de Content-Type:** cambiar la cabecera a `image/png`.
- **Bypass de magic bytes:** anteponer cabecera de imagen válida al payload.
- **Ejecución:** acceder a la URL del fichero subido; si el directorio ejecuta código → webshell → reverse shell.
- Otros: SVG con XSS/XXE, ficheros que sobreescriben rutas (path traversal en el nombre).

## Impacto

Ejecución remota de código y compromiso del servidor (crítico) cuando la webshell es ejecutable; XSS/XXE almacenado o DoS en otros casos.

## Cómo remediar

- Lista blanca de extensiones y validación de contenido real (magic bytes).
- Renombrar el fichero y guardarlo **fuera del webroot** o en almacenamiento que no ejecute código.
- Servir descargas con `Content-Disposition` y sin permisos de ejecución.
- Límite de tamaño y análisis antimalware.

## Referencias

- OWASP WSTG `WSTG-BUSL-09` · CWE-434
- OWASP File Upload Cheat Sheet

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/10-business-logic.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
