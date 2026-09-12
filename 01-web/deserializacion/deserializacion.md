# Deserialización insegura — Índice

- **WSTG:** relacionado con `WSTG-INPV`
- **OWASP Top 10:** `A08:2021 – Software and Data Integrity Failures`
- **Alias:** insecure deserialization, object injection

## Qué es

La app deserializa datos controlados por el usuario sin validar integridad. Manipulando el objeto, el atacante altera la lógica o, con "gadget chains" en las librerías presentes, llega a RCE.

## Detección (común)

Identifica blobs serializados por su formato:

| Lenguaje | Pista |
|---|---|
| PHP | empieza por `O:` , `a:` (serialize) |
| Java | base64 que empieza por `rO0` (`AC ED 00 05` en hex) |
| Python (pickle) | opcodes; a menudo base64 |
| .NET | `AAEAAAD/////` (BinaryFormatter) |

## Fichas por lenguaje

| Lenguaje | Ficha |
|---|---|
| PHP | [php.md](php.md) |
| Java | [java.md](java.md) |
| Python (pickle) | [python.md](python.md) |

## Impacto

Desde manipulación de lógica/escalada hasta RCE (crítico), según las gadget chains disponibles.

## Remediación (común)

- No deserializar datos no confiables; preferir formatos de solo datos (JSON).
- Firmar/verificar integridad de los objetos serializados.
- Listas blancas de clases permitidas.

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: CWE-502 · PortSwigger — Insecure deserialization
