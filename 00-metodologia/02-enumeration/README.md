# 02 · Enumeration — Mapear la aplicación por dentro

Continúa `01-recon/`. Si recon respondía *"¿qué hay ahí fuera?"*, enumeration responde *"¿de qué está hecha esta app y cuáles son todos sus puntos de entrada?"*. Toca sobre todo `WSTG-INFO` (mapeo de contenido) y roza `WSTG-CONF` (config/despliegue) y `WSTG-IDNT` (gestión de identidad).

Objetivo: convertir el inventario de activos de recon en un **mapa completo de la superficie de ataque** de cada app, para no atacar a ciegas en `03-explotacion/`.

---

## Punto de partida

Los `vivos.txt` / inventario que salieron de recon. Para cada host/app vivo, ahora entras a mapearlo.

---

## Flujo

1. **Crawling / spidering** — recorrer la app siguiendo enlaces (con Burp o un crawler) para ver la estructura "oficial".
2. **Descubrimiento de contenido oculto** (forced browsing) — dirbusting de rutas y ficheros no enlazados.
3. **Descubrimiento de endpoints y parámetros** — incluye analizar los ficheros `.js` (ahí viven rutas de API, endpoints ocultos y a veces secretos).
4. **Mapeo de APIs** — REST/GraphQL, buscar documentación (swagger/openapi), enumerar operaciones.
5. **Autenticación e identidad** — cómo se registra/loguea uno, qué roles hay, recuperación de contraseña, política de usuarios (enumeración de usuarios).
6. **Consolidar** — anotar todos los puntos de entrada (parámetros, headers, cookies, uploads) que luego probarás.

> **Autenticado vs no autenticado:** repite el mapeo con cada rol. Muchísima superficie solo aparece una vez logueado. Por eso en recon insistíamos en **pedir usuarios de prueba de cada rol**.

---

## No dejarse sin mirar

- `robots.txt`, `sitemap.xml`, `.well-known/`, comentarios en HTML.
- Ficheros `.js` (mapas de rutas, endpoints de API, claves).
- Documentación de API: `/swagger`, `/openapi.json`, `/graphql`, `/api/docs`.
- Parámetros ocultos y funciones no enlazadas desde la UI.
- Ficheros de backup/config: `.git/`, `.env`, `web.config`, `*.bak`, `*.old`, `*.zip`.
- Paneles y entornos: `/admin`, `/dev`, `/test`, subdominios de staging.
- Códigos de estado reveladores: 401/403 (existe pero protegido), 302 (redirección interesante).

---

## Entregable de la fase

Un **mapa de superficie de ataque** por app que alimenta `03-explotacion/`:

- Árbol de rutas/endpoints descubiertos.
- Lista de parámetros de entrada por endpoint.
- APIs y sus operaciones.
- Roles y flujos de autenticación.
- Candidatos "jugosos": uploads, endpoints admin, parámetros que huelen a inyección, ficheros expuestos.

---

## Herramientas (referencia)

Los comandos concretos van en `04-cheatsheets/por-fase/enumeration.md`.

- **Crawling:** Burp (spider), katana, hakrawler, gospider
- **URLs históricas:** gau, waybackurls
- **Content discovery:** ffuf, feroxbuster, gobuster
- **Parámetros:** arjun, x8, param-miner (Burp)
- **Análisis de JS:** LinkFinder, getJS, katana (`-jc`)
- **APIs:** graphw00f, InQL (GraphQL); swagger UI
- **Vhosts:** ffuf (fuzzing de `Host`)

---

## Errores comunes

- Mapear solo sin loguear → te pierdes la mayor parte de la app.
- No mirar los `.js` → ahí suele estar la API "de verdad".
- Dirbustear con una wordlist gigante desde el minuto uno → ruido y lentitud; empieza con listas curadas.
- No anotar los parámetros → luego en explotación no sabes qué probar.

## Referencias

- OWASP WSTG — `WSTG-INFO` (mapeo), `WSTG-CONF`, `WSTG-IDNT`.
- Ver `../00-fundamentos/estandares-y-metodologias.md`.
