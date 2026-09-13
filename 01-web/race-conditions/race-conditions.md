# Race Conditions — Índice

- **WSTG:** `WSTG-BUSL-04`
- **OWASP Top 10:** `A04:2021 – Insecure Design`
- **Alias:** condiciones de carrera, TOCTOU

## Qué es

Dos operaciones que deberían ser secuenciales se ejecutan casi a la vez y la app no controla la concurrencia, dejando un estado inconsistente. Típico en la ventana entre "comprobar" y "usar" (TOCTOU).

## Dónde aparece

Cupones/descuentos, saldo o puntos, límites de uso, reservas/stock, aceptar invitaciones, votar, retirar fondos, verificación en múltiples pasos.

## Ficha a fondo

| Tema | Ficha |
|---|---|
| Explotación con single-packet attack | [single-packet.md](single-packet.md) |

## Impacto

Fraude y ventajas indebidas (dinero, recursos, saltarse límites), inconsistencias de datos.

## Remediación (común)

- Bloqueos y transacciones atómicas en servidor; controles de idempotencia.
- Constraints/locks a nivel de base de datos.
- Diseño que no dependa de comprobaciones no atómicas.

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/10-business-logic.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-BUSL-04` · CWE-362 · PortSwigger — Race conditions
