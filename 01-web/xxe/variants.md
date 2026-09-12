# XXE — Variantes

Ver índice: [xxe.md](xxe.md). **Solo sobre objetivos autorizados.** XXE donde no parece haber XML "a la vista".

## Ficheros OOXML (.docx, .xlsx, .pptx)

Son ZIP con XML dentro. Descomprime, inyecta el DOCTYPE/entidad en un `.xml` interno (p. ej. `word/document.xml`), recomprime y sube. Si el servidor lo parsea → XXE.

## SVG

Los `.svg` son XML: en subidas de imagen/avatar que aceptan SVG:
```xml
<?xml version="1.0"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg xmlns="http://www.w3.org/2000/svg"><text>&xxe;</text></svg>
```

## SOAP

APIs SOAP consumen XML directamente → inyecta la entidad en el cuerpo SOAP.

## XInclude

Cuando **no** controlas el DOCTYPE completo (solo un valor dentro del XML), prueba XInclude:
```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
  <xi:include parse="text" href="file:///etc/passwd"/>
</foo>
```

## Content-Type

A veces un endpoint que espera JSON también acepta XML: cambia `Content-Type: application/xml` y envía XML con la entidad.

## Notas

- Las variantes de subida (SVG/OOXML) son de las más rentables en apps modernas.
- Combina con [blind-oob.md](blind-oob.md) si no hay salida directa.
