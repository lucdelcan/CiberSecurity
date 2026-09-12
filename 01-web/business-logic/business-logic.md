# Business Logic Flaws

- **WSTG:** `WSTG-BUSL-*`
- **OWASP Top 10:** `A04:2021 – Insecure Design`
- **Alias:** fallos de lógica de negocio

## Qué es

Fallos en las reglas de negocio de la aplicación (no en la implementación técnica) que permiten usarla de formas no previstas. No los detecta un scanner: requieren entender qué **debería** hacer la app.

## Vectores frecuentes

- Validación de datos incoherente: cantidades negativas, precios manipulables, saltarse límites.
- Saltarse el orden de un flujo (llegar al paso final sin completar los previos).
- Abusar de límites de uso: aplicar un cupón varias veces, votar/repetir acciones.
- Forjar peticiones que la interfaz no permite.
- Race conditions (ver `../race-conditions/`).

## Cómo detectarla

- Entiende el propósito de cada funcionalidad y pregúntate "¿qué pasa si hago esto de forma inesperada?".
- Manipula valores, orden de pasos, y repite acciones que deberían ser únicas.
- Prueba valores límite y combinaciones no contempladas.

## Impacto

Muy variable: fraude, acceso o ventajas indebidas, pérdidas económicas. Puede ser crítico según el negocio.

## Cómo remediar

- Validar las reglas de negocio en **servidor**, no en cliente.
- Máquinas de estado que fuercen el orden correcto del flujo.
- Controles de idempotencia y límites de uso robustos.

## Referencias

- OWASP WSTG `WSTG-BUSL-*`
- OWASP — Business Logic Vulnerability

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/10-business-logic.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
