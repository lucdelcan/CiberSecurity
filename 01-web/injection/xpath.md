# XPath Injection

- **WSTG:** `WSTG-INPV-09`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** inyección XPath

## Qué es

Cuando la aplicación consulta un documento XML mediante XPath construyendo la expresión con entrada del usuario sin sanitizar. Análogo a SQLi pero sobre XML.

## Cómo detectarla

- Inyecta `'`, `"`, `or 1=1`, `]` y observa errores o cambios de resultado.
- En logins: `' or '1'='1`.

## Cómo explotarla

- **Bypass:** condiciones siempre verdaderas (`' or '1'='1`).
- **Extracción ciega:** funciones como `substring()`, `string-length()`, `count()` para inferir nodos y valores carácter a carácter.

## Impacto

Bypass de autenticación y extracción de todo el documento XML (que suele contener credenciales o datos sensibles).

## Cómo remediar

- Consultas XPath parametrizadas / precompiladas.
- Escapar y validar la entrada (lista blanca).

## Referencias

- OWASP WSTG `WSTG-INPV-09` · CWE-643

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
