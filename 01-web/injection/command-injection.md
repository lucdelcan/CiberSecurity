# Command Injection — Índice

- **WSTG:** `WSTG-INPV-12`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** OS command injection, inyección de comandos

## Qué es

La app pasa entrada del usuario a una llamada al sistema operativo sin sanitizarla. El atacante encadena comandos con operadores del shell → ejecución de comandos (RCE).

## Detección rápida

```bash
; id      | id      && id      || id      `id`      $(id)      %0a id
```
Sin salida visible → ve a [blind.md](blind.md). Si hay filtros → [bypass.md](bypass.md).

## Fichas a fondo

| Tema | Ficha |
|---|---|
| Command injection ciega (OOB / time) | [blind.md](blind.md) |
| Evasión de filtros | [bypass.md](bypass.md) |

## Impacto

Ejecución de comandos con los privilegios del servicio web → compromiso del host y pivote. Crítico.

## Remediación (común)

- Evitar el shell; usar APIs nativas que separan comando y argumentos (arrays).
- Nunca concatenar entrada; lista blanca estricta.
- Mínimo privilegio del servicio.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/command-injection.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-INPV-12` · CWE-78 · PortSwigger — OS command injection
