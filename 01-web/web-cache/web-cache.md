# Web Cache Attacks

- **WSTG:** relacionado con `WSTG-CONF` / `WSTG-INPV-17` (Host header)
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** cache poisoning, cache deception

## Qué es

- **Cache poisoning:** el atacante consigue que la caché almacene una respuesta maliciosa (p. ej. vía cabeceras no incluidas en la clave de caché) que luego se sirve a otros usuarios.
- **Cache deception:** engañar a la caché para que almacene contenido sensible de una víctima y luego recuperarlo.

## Cómo detectarla

- Identifica cachés (cabeceras `X-Cache`, `Age`, CDN).
- **Poisoning:** busca "unkeyed inputs" (cabeceras que afectan la respuesta pero no forman parte de la clave de caché) — p. ej. `X-Forwarded-Host`, `X-Forwarded-Scheme`.
- **Deception:** prueba añadir extensiones estáticas a rutas dinámicas (`/perfil/foo.css`) y ver si se cachea contenido privado.

## Cómo explotarla

- Poisoning: inyecta un input no incluido en la clave que altere la respuesta (XSS reflejado, redirect) y consigue que se cachee para todos.
- Deception: fuerza el cacheo de una página autenticada de la víctima y accede a la versión cacheada.

## Impacto

Distribución masiva de contenido malicioso (XSS a todos los usuarios), o robo de datos sensibles cacheados.

## Cómo remediar

- Configurar bien la **clave de caché** (incluir todo input que afecte la respuesta).
- No cachear contenido sensible/autenticado; cabeceras `Cache-Control` correctas.
- Normalizar y validar cabeceras como `Host`/`X-Forwarded-*`.

## Referencias

- PortSwigger — Web cache poisoning / deception · CWE-524

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/02-config-deploy.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
