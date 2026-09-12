# Cheatsheet · Recon

Comandos básicos de recon listos para copiar. Se corresponde con el proceso de `00-metodologia/01-recon/`.
Sustituye `TARGET`/`dominio.com` por el objetivo in-scope. **Úsalo solo sobre lo autorizado.**

## Subdominios

```bash
# subfinder (pasivo, rápido)
subfinder -d dominio.com -all -silent -o subs.txt

# amass (más exhaustivo, más lento)
amass enum -passive -d dominio.com -o amass.txt

# Certificate Transparency (crt.sh) sin herramientas
curl -s "https://crt.sh/?q=%25.dominio.com&output=json" | jq -r '.[].name_value' | sort -u
```

## Resolver y ver qué está vivo

```bash
# resolver dominios
dnsx -l subs.txt -a -resp -silent

# probar HTTP/HTTPS y sacar código, título y tecnología
cat subs.txt | httpx -sc -title -tech-detect -silent -o vivos.txt
```

## Puertos y servicios

```bash
# barrido rápido de puertos
naabu -host dominio.com -top-ports 1000 -silent

# nmap sobre lo vivo (versiones + scripts por defecto)
nmap -sC -sV -oA nmap_TARGET -iL ips.txt
```

## Fingerprinting de tecnología

```bash
whatweb https://dominio.com

# detección de tecnologías con nuclei
nuclei -u https://dominio.com -tags tech
```

## Descubrimiento de contenido (dirbusting)

```bash
# ffuf
ffuf -w /ruta/wordlist.txt -u https://dominio.com/FUZZ -mc 200,204,301,302,307,401,403

# feroxbuster (recursivo)
feroxbuster -u https://dominio.com -w /ruta/wordlist.txt
```

## OSINT / recursos públicos

```bash
# emails, hosts y nombres públicos
theHarvester -d dominio.com -b all

# ficheros y comentarios evidentes
curl -s https://dominio.com/robots.txt
curl -s https://dominio.com/sitemap.xml
```

## Google dorks útiles

```text
site:dominio.com -www
site:dominio.com ext:pdf | ext:xls | ext:doc | ext:txt | ext:log
site:dominio.com inurl:admin | inurl:login | inurl:dashboard
site:dominio.com intitle:"index of"
```

## Notas

- Todo el tráfico manual pásalo por **Burp Suite** (proxy) para tenerlo registrado.
- Guarda las salidas (`subs.txt`, `vivos.txt`, `nmap_*`) → alimentan el inventario de activos de la fase de recon.
- Wordlists recomendadas: SecLists (ver `wordlists.md`).
