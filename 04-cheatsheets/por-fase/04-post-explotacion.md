# Cheatsheet · Post-explotación

Comandos de **reconocimiento una vez dentro** (situational awareness) y localización de loot.
El detalle de *escalada* concreta está en `02-infra-redes/` (linux/windows privesc).
Para subir/bajar ficheros ver [03-explotacion](03-explotacion.md). **Solo sobre objetivos autorizados.**

## Situational awareness — Linux

```bash
id; whoami; hostname; uname -a          # quién soy / qué sistema
sudo -l                                 # qué puedo ejecutar como root
cat /etc/os-release                     # distro y versión
ip a; cat /etc/hosts                    # red y hosts conocidos
ps aux --forest                         # procesos
ss -tulpn                               # puertos en escucha
cat /etc/passwd | grep -v nologin       # usuarios con shell
crontab -l; ls -la /etc/cron*           # tareas programadas
env                                     # variables de entorno
```

## Situational awareness — Windows

```cmd
whoami /all                             :: usuario, grupos y privilegios
systeminfo                              :: SO, parches, arquitectura
ipconfig /all                           :: red
net user; net localgroup administrators :: usuarios y admins
tasklist /v                             :: procesos
netstat -ano                            :: conexiones/puertos
whoami /priv                            :: privilegios (SeImpersonate...)
```

## Enumeración automática de privesc

```bash
# Linux
./linpeas.sh                            # todo-en-uno
./pspy64                                # procesos/cron sin ser root
# Windows
winpeas.exe
```
> El *cómo explotar* lo que encuentren estas tools → `02-infra-redes/`.

## Búsqueda de loot (credenciales / secretos)

```bash
# Linux
grep -rniE "password|passwd|secret|api[_-]?key|token" /var/www 2>/dev/null
find / -name "*.bak" -o -name "*.config" -o -name ".env" 2>/dev/null
cat ~/.bash_history; cat ~/.ssh/id_rsa 2>/dev/null

# Windows
findstr /si password *.txt *.xml *.config *.ini
```

## Limpieza (dejar la máquina como estaba)

```bash
# borra lo que subiste
rm -f /tmp/shell.elf /var/www/html/shell.php /tmp/linpeas.sh
# revisa que no queden procesos/artefactos tuyos
```

## Notas

- Recoge la evidencia del acceso (`id`/`whoami` + captura) **antes** de tocar nada más.
- Nada de persistencia en un pentest normal; limpia todo al terminar.
- Registra cada comando con su hora para el informe.
