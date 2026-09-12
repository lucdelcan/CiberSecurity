# TTY Upgrade

Estabilizar una shell "tonta" (reverse/bind) para tener una TTY interactiva completa (Ctrl-C, autocompletado, editores).

## Método clásico (Python)

```bash
# en la shell de la víctima
python3 -c 'import pty; pty.spawn("/bin/bash")'
# o: python -c ...
export TERM=xterm

# ahora en TU máquina (background la shell y arregla el tty)
# Ctrl-Z
stty raw -echo; fg
# pulsa Enter un par de veces
```

## Alternativas para spawnear

```bash
/bin/bash -i
script -qc /bin/bash /dev/null
socat exec:'bash -li',pty,stderr,setsid,sigint,sane -   # requiere socat
```

## Ajustar tamaño de la terminal

```bash
# en tu máquina, mira filas/columnas
stty size          # ej. 38 190
# en la víctima
stty rows 38 columns 190
```
