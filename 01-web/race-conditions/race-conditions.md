# Race Conditions

- **WSTG:** `WSTG-BUSL-04`
- **OWASP Top 10:** `A04:2021 – Insecure Design`
- **Alias:** condiciones de carrera, TOCTOU

## Qué es

Cuando dos operaciones que deberían ser secuenciales se ejecutan casi simultáneamente y la aplicación no controla la concurrencia, se puede provocar un estado inconsistente. Típico en una ventana entre "comprobar" y "usar" (TOCTOU).

## Cómo detectarla

- Funciones con límite o comprobación previa: cupones, saldo, votos, reservas, canje de puntos.
- Envía muchas peticiones idénticas **en paralelo** (single-packet attack / turbo intruder) y observa si el límite se supera.

## Cómo explotarla

1. Identifica una acción que debería ejecutarse una sola vez o depende de un estado.
2. Lánzala muchas veces concurrentemente para colarte en la ventana de carrera.
3. Resultado: aplicar un cupón N veces, gastar saldo duplicado, saltarse límites.

## Impacto

Fraude y ventajas indebidas (dinero, recursos, límites), inconsistencias de datos.

## Cómo remediar

- Bloqueos y transacciones atómicas en servidor; controles de idempotencia.
- Restricciones a nivel de base de datos (constraints, locks).
- Diseño que no dependa de comprobaciones no atómicas.

## Referencias

- OWASP WSTG `WSTG-BUSL-04` · CWE-362
- PortSwigger — Race conditions

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/10-business-logic.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
