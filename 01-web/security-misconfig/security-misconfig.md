# Security Misconfiguration

- **WSTG:** `WSTG-CONF-*`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** configuración de seguridad deficiente

## Qué es

Configuraciones inseguras o por defecto en cualquier capa: servidor, framework, cabeceras, métodos HTTP, permisos, servicios innecesarios habilitados.

## Vectores frecuentes

- **Cabeceras de seguridad** ausentes (CSP, HSTS, X-Content-Type-Options, X-Frame-Options).
- **Métodos HTTP** peligrosos habilitados (PUT, DELETE, TRACE).
- Configuraciones y credenciales por defecto; paneles de admin expuestos.
- Directory listing, ficheros de ejemplo, servicios de debug en producción.
- Permisos de fichero laxos; almacenamiento cloud mal configurado.

## Cómo detectarla

- Revisa cabeceras de respuesta y métodos permitidos (`OPTIONS`).
- Busca configuraciones por defecto, listados de directorio y endpoints de debug.
- Comprueba buckets/blobs y permisos.

## Impacto

Aumenta la superficie de ataque y facilita explotar otras vulns; por sí solo suele ser bajo/medio salvo casos concretos (debug expuesto, admin accesible).

## Cómo remediar

- Endurecer la configuración por defecto (hardening) en todas las capas.
- Aplicar cabeceras de seguridad; deshabilitar métodos y servicios innecesarios.
- Proceso de despliegue reproducible y revisado.

## Referencias

- OWASP WSTG `WSTG-CONF-*` · CWE-16

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/02-config-deploy.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
