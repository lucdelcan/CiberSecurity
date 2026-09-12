# SSRF ciego y exfiltración OOB

Ver índice: [ssrf.md](ssrf.md). **Solo sobre objetivos autorizados.**

## Qué es

SSRF **ciego**: el servidor hace la petición pero no te devuelve la respuesta. No ves el resultado directo, así que confirmas y exfiltras por un canal fuera de banda (OOB): una interacción de red (DNS/HTTP) hacia un servidor tuyo.

## Confirmación

1. Pon como destino una URL a tu **Collaborator**/servidor propio.
2. Si recibes la petición entrante (DNS o HTTP), hay SSRF aunque no veas la respuesta en la app.

```
http://TU-COLLABORATOR/
http://xxxxx.oastify.com/     (o tu propio listener)
```

## Aprovechar el ciego

Sin respuesta visible, aún puedes:

- **Mapear la red interna** por *diferencias de tiempo/estado*: un host/puerto abierto responde distinto (o tarda distinto) que uno cerrado.
- **Alcanzar servicios internos** que ejecutan acciones sin necesitar respuesta (webhooks internos, colas).
- **Exfiltrar datos** cuando puedes meterlos en el nombre de host de una consulta DNS que provoca el servidor (p. ej. si encadenas con otra vuln que refleje datos en la URL).

## Montar el canal OOB

- Burp Collaborator, o un dominio propio con un servidor DNS/HTTP que registre peticiones.
- Un simple `nc -lvnp 80` o `python3 -m http.server` recoge HTTP entrante para PoC.

## Notas

- El SSRF ciego suele infravalorarse: la clave es demostrar el alcance interno con la interacción OOB.
- Combínalo con `cloud-metadata.md` (a veces la petición a metadata dispara acciones aunque no veas el cuerpo).
