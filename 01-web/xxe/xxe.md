# XML External Entity (XXE)

- **WSTG:** `WSTG-INPV-07`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** XXE, inyección de entidades externas XML

## Qué es

Un parser XML procesa entrada con entidades externas habilitadas. El atacante define entidades que hacen al parser leer ficheros locales, hacer peticiones de red (SSRF) o provocar DoS.

## Cómo detectarla

- Cualquier endpoint que acepte XML (SOAP, APIs XML, subida de `.docx`/`.svg`/`.xml`).
- Inyecta una entidad de prueba y observa si se resuelve:
  define un `DOCTYPE` con una entidad externa que apunte a un fichero o a tu servidor (OOB).

## Cómo explotarla

- **Lectura de ficheros:** entidad externa `SYSTEM "file:///etc/passwd"` reflejada en la respuesta.
- **Blind/OOB:** exfiltrar por DNS/HTTP con DTD externa cuando no hay salida directa.
- **SSRF** vía entidad que apunta a recursos internos.
- **DoS:** expansión de entidades ("billion laughs").

## Impacto

Lectura de ficheros sensibles del servidor, SSRF a la red interna, y en casos DoS. Puede escalar a RCE en escenarios concretos.

## Cómo remediar

- Deshabilitar DTD y entidades externas en el parser (configuración segura por defecto).
- Usar formatos menos complejos (JSON) donde sea posible.
- Parsers actualizados y con resolución de entidades externas desactivada.

## Referencias

- OWASP WSTG `WSTG-INPV-07` · CWE-611
- OWASP XXE Prevention Cheat Sheet

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
