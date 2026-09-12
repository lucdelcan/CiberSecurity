# Deserialización — PHP

Ver índice: [deserializacion.md](deserializacion.md). **Solo sobre objetivos autorizados.**

## Formato

```
O:4:"User":1:{s:4:"name";s:5:"admin";}   # objeto
a:2:{i:0;s:1:"a";i:1;s:1:"b";}            # array
```

## Vectores

- **Manipular propiedades:** cambiar valores del objeto serializado (rol, ruta, flags).
- **Magic methods:** `__wakeup()`, `__destruct()`, `__toString()` se ejecutan al deserializar/usar el objeto → un objeto elegido con propiedades controladas puede disparar acciones (POP chain).
- **Gadget chains (POP):** encadenar clases presentes para llegar a escritura de fichero/RCE.
- **Phar deserialization:** disparar deserialización vía `phar://` en funciones de sistema de ficheros.

## Herramientas

```
phpggc <gadget> system id        # genera payloads POP para frameworks conocidos
phpggc -l                        # lista gadgets disponibles
```

## Notas

- Localiza el `unserialize()` y qué clases (gadgets) están disponibles en el código/framework.
- Prueba `phar://` si no ves un `unserialize()` directo pero controlas una ruta de fichero.
