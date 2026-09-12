# LDAP Injection

- **WSTG:** `WSTG-INPV-06`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** inyección LDAP

## Qué es

La aplicación construye un filtro de búsqueda LDAP con entrada del usuario sin escaparla. El atacante manipula la sintaxis de los filtros LDAP para alterar la consulta (típico en logins contra directorio o buscadores de usuarios).

## Cómo detectarla

- Inyecta metacaracteres de filtros LDAP: `*`, `(`, `)`, `|`, `&`, `\`.
- En un login, prueba `*` como usuario/contraseña, o `admin)(&)` y variantes.
- Cambios en el número de resultados o bypass de login indican inyección.

## Cómo explotarla

- **Bypass de autenticación:** cerrar el filtro y añadir una condición siempre verdadera (`*)(uid=*))(|(uid=*`).
- **Extracción:** usar comodines y condiciones para inferir atributos carácter a carácter (similar a blind).

## Impacto

Bypass de autenticación, enumeración/extracción de información del directorio (usuarios, atributos). Según el caso, escalada de privilegios.

## Cómo remediar

- Escapar la entrada según RFC 4515 antes de meterla en el filtro.
- Usar librerías/bindings parametrizados.
- Lista blanca de caracteres permitidos y mínimo privilegio de la cuenta de bind.

## Referencias

- OWASP WSTG `WSTG-INPV-06` · CWE-90

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
