# Path Traversal

- **WSTG:** `WSTG-AUTHZ-01`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** directory traversal, `../`

## Qué es

La aplicación usa entrada del usuario para construir una ruta de fichero sin canonizarla ni confinarla, permitiendo salir del directorio previsto con secuencias `../` y leer (o escribir) ficheros arbitrarios del servidor.

## Cómo detectarla

- Parámetros que referencian ficheros: `?file=`, `?download=`, `?path=`, nombres en subidas.
- Prueba `../../../../etc/passwd` y `..\\..\\windows\\win.ini`.
- Bypass: codificación (`%2e%2e%2f`), doble codificación, prefijos absolutos, null byte (legacy).

## Cómo explotarla

- Leer ficheros sensibles: configuración, credenciales, código fuente, claves.
- Escritura (si aplica) para sobrescribir ficheros → puede escalar a RCE.
- Relacionado con LFI cuando el fichero se **incluye** en vez de solo leerse (ver `../injection/lfi-rfi.md`).

## Impacto

Divulgación de ficheros sensibles del servidor; según permisos, escritura y escalada a ejecución de código.

## Cómo remediar

- Canonizar la ruta y verificar que queda dentro del directorio permitido.
- No usar entrada del usuario como ruta; usar identificadores mapeados a rutas fijas.
- Mínimo privilegio del proceso sobre el sistema de ficheros.

## Referencias

- OWASP WSTG `WSTG-AUTHZ-01` · CWE-22

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/05-authorization.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
