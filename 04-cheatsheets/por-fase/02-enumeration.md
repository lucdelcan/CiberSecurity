# Cheatsheet · Enumeration

Comandos listos para copiar. Corresponde a `00-metodologia/02-enumeration/`.
Sustituye `dominio.com`/`URL` por el objetivo in-scope. **Solo sobre lo autorizado.**

## Crawling / recolección de URLs

```bash
# katana (crawler activo, incluye parseo de JS con -jc)
katana -u https://dominio.com -jc -silent -o urls.txt

# hakrawler
echo https://dominio.com | hakrawler

# URLs históricas (pasivo, de archivos públicos)
gau dominio.com > gau.txt
waybackurls dominio.com > wayback.txt
```

## Content discovery (forced browsing)

```bash
# ffuf (lo más usado)
ffuf -w wordlist.txt -u https://dominio.com/FUZZ -mc 200,204,301,302,307,401,403 -o ffuf.json

# feroxbuster (recursivo por defecto)
feroxbuster -u https://dominio.com -w wordlist.txt -x php,txt,bak,zip

# gobuster
gobuster dir -u https://dominio.com -w wordlist.txt -x php,html,txt
```

## Descubrimiento de parámetros

```bash
# arjun (parámetros ocultos GET/POST/JSON)
arjun -u "https://dominio.com/endpoint"

# x8
x8 -u "https://dominio.com/endpoint" -w params.txt

# ffuf para parámetros GET
ffuf -w params.txt -u "https://dominio.com/page?FUZZ=test" -fs 0
```

## Análisis de JavaScript

```bash
# extraer .js del target
getJS --url https://dominio.com --output js.txt

# buscar endpoints/rutas dentro de los JS
katana -u https://dominio.com -jc -silent | grep -Ei '\.js$'
# LinkFinder (endpoints en un JS)
python3 linkfinder.py -i https://dominio.com/app.js -o cli
```

## APIs

```bash
# documentación típica a probar a mano
curl -s https://dominio.com/swagger.json
curl -s https://dominio.com/openapi.json
curl -s https://dominio.com/api/docs

# GraphQL: fingerprint + introspección
graphw00f -d -t https://dominio.com/graphql
# introspection query (si está habilitada)
curl -s -X POST https://dominio.com/graphql \
  -H 'Content-Type: application/json' \
  -d '{"query":"{__schema{types{name}}}"}'
```

## Virtual hosts

```bash
ffuf -w vhosts.txt -u https://dominio.com -H "Host: FUZZ.dominio.com" -fs 0
```

## Ficheros sensibles a probar

```text
/.git/HEAD        /.env           /web.config
/backup.zip       /config.php.bak /.DS_Store
/robots.txt       /sitemap.xml    /.well-known/
```

## Notas

- Empieza con wordlists **curadas** (raft-small, common) antes de las gigantes → menos ruido.
- Todo el mapeo manual pásalo por **Burp** para que quede en el sitemap.
- Repite content discovery **autenticado** con cada rol (cookie/token en `-H`).
- Las salidas alimentan el mapa de superficie de `03-explotacion/`.
