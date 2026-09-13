# Race Conditions — Single-packet attack

Ver índice: [race-conditions.md](race-conditions.md). **Solo sobre objetivos autorizados.**

## El problema del "casi a la vez"

Para ganar la carrera, las peticiones deben llegar dentro de una ventana de milisegundos. La latencia de red introduce "jitter" que arruina el timing si mandas las peticiones en serie.

## Single-packet attack

Técnica (Turbo Intruder / Burp) que **elimina el jitter de red**: prepara N peticiones dejando el último byte de cada una sin enviar, y luego libera todos los últimos bytes juntos. En HTTP/2 se envían en un solo paquete → llegan prácticamente simultáneas al servidor.

## Cómo probarlo

1. Identifica una acción que **debería ejecutarse una sola vez** o que comprueba un estado antes de actuar (canjear cupón, retirar saldo, aceptar invitación).
2. Con Turbo Intruder, envía muchas copias con la técnica single-packet (o "last-byte sync").
3. Observa si el efecto se aplica más veces de lo permitido (cupón aplicado N veces, saldo gastado dos veces).

## Ejemplos de impacto

```
- Aplicar un código de descuento múltiples veces.
- Retirar/transferir el mismo saldo dos veces (double-spend).
- Superar un límite de intentos / de uso.
- Registrar el mismo recurso único dos veces.
```

## Notas

- HTTP/2 facilita el single-packet; en HTTP/1.1 se usa sincronización del último byte con muchas conexiones.
- Repite varias veces: las carreras son probabilísticas.
- Documenta el número de peticiones y el resultado (p. ej. "10 peticiones → cupón aplicado 4 veces").
