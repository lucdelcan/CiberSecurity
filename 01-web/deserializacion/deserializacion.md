# Deserialización insegura

- **WSTG:** relacionado con `WSTG-INPV` (input validation)
- **OWASP Top 10:** `A08:2021 – Software and Data Integrity Failures`
- **Alias:** insecure deserialization, object injection

## Qué es

La aplicación deserializa datos controlados por el usuario sin validar su integridad. Manipulando el objeto serializado, el atacante puede alterar la lógica o, mediante "gadget chains", llegar a ejecución de código.

## Cómo detectarla

- Identifica datos serializados: cookies/parámetros en base64 que empiezan por patrones conocidos (PHP `O:`, Java `rO0`, .NET, Python pickle).
- Modifica campos del objeto y observa cambios de comportamiento.
- Herramientas: ysoserial (Java), ysoserial.net, phpggc (PHP).

## Cómo explotarla

1. Reconoce el formato y el lenguaje.
2. Manipula atributos para escalar privilegios/alterar lógica.
3. Con una gadget chain disponible en las librerías del target, genera un payload que ejecute comandos (RCE).

## Impacto

Desde manipulación de lógica y escalada hasta RCE (crítico), según las gadget chains disponibles.

## Cómo remediar

- No deserializar datos no confiables; preferir formatos de solo datos (JSON) con parsers seguros.
- Firmar/verificar integridad de los objetos serializados.
- Listas blancas de clases permitidas en la deserialización.

## Referencias

- OWASP — Insecure Deserialization · CWE-502
- PortSwigger — Insecure deserialization

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
