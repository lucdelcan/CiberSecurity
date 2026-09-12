# 01 · Recon — Entender la superficie de ataque

Corresponde a **WSTG-INFO** (Information Gathering). Todo lo previo a atacar. El objetivo no es "lanzar herramientas", es **entender qué es la aplicación, de qué está hecha y por dónde se le puede entrar**, para no atacar a ciegas.

Regla mental: *no puedes probar lo que no conoces*. Una superficie mal mapeada = findings que se te escapan.

---

## 0. Pre-engagement (antes de tocar nada)

Esto no es opcional y suele decidir la calidad del test:

- **Confirmar el alcance (scope):** qué dominios, subdominios, IPs, apps y APIs están *in-scope* y, sobre todo, **qué está fuera**. Anotar wildcards (`*.cliente.com`) y entornos (prod vs pre).
- **Ventanas y reglas:** horario permitido, si se puede hacer fuzzing agresivo, si hay WAF que no deben bloquearte (whitelisting de tu IP), a quién avisar si algo cae.
- **Datos y límites:** qué no se puede tocar (datos reales de usuarios, borrados, pagos reales), y cómo reportar si encuentras datos sensibles.
- **⭐ Pedir usuarios de prueba.** Si la app tiene autenticación, **pide credenciales de test para CADA rol** (admin, usuario normal, usuario de solo lectura, distintos tenants…). Esto es clave porque:
  - Sin usuarios solo pruebas la parte pública → te pierdes la mayoría de la superficie.
  - Necesitas **≥2 usuarios del mismo rol** y usuarios de **distinto rol** para probar control de acceso (IDOR, escalada horizontal/vertical) más adelante en `03-explotacion` / `01-web/access-control`.
  - Idealmente cuentas que puedas "quemar" (registrar, modificar, romper) sin afectar a datos reales.
  - Si el registro es abierto, créate tú los usuarios; si no, pídelos por escrito.
- **Documentación:** pedir (si existe) diagrama de arquitectura, colección de Postman/OpenAPI, manual de roles. Ahorra horas de mapeo.

> Todo esto se apunta: es la base del apartado "Alcance" del informe.

---

## 1. Recon pasivo (sin tocar el target)

Información que se obtiene **sin enviar tráfico a la aplicación** (o mínimo/indistinguible del normal). No levanta alarmas.

- **OSINT del dominio/organización:** whois, registros DNS, certificados (crt.sh / Certificate Transparency → destapa subdominios), buscadores.
- **Google/Bing dorking:** ficheros expuestos, paneles, rutas indexadas.
- **Filtraciones y secretos:** repos públicos (GitHub), credenciales en pastebins, claves en JS.
- **Tecnología a alto nivel:** headers públicos, CDNs, proveedores.

## 2. Recon activo (ya interactúas con el target)

- **Descubrimiento de subdominios** y resolución (cuáles están vivos).
- **Hosts vivos y puertos/servicios** expuestos (qué escucha además del 443).
- **Fingerprinting:** framework, lenguaje, servidor web, WAF/CDN, versiones, tecnologías cliente.
- **Identificar los distintos "apps" dentro del scope:** panel admin, API, app móvil-backend, webs legacy…

---

## 3. Ejes de la superficie de ataque (qué mapear)

Piensa la superficie en dimensiones; para cada una, anota qué encuentras:

| Eje | Qué buscar |
|---|---|
| **Dominios/subdominios** | Todo lo vivo dentro de scope, incluidos assets olvidados/legacy |
| **Tecnologías** | Framework, servidor, lenguaje, versiones, WAF, terceros (SDKs, analytics) |
| **Puntos de entrada** | Formularios, parámetros GET/POST, headers, cookies, uploads |
| **Autenticación** | Cómo se loguea, roles, SSO/OAuth, recuperación de contraseña |
| **APIs** | REST/GraphQL, endpoints, documentación (swagger/openapi) |
| **Contenido oculto** | robots.txt, sitemap, `.js`, comentarios HTML, directorios no enlazados |
| **Terceros/integraciones** | Pasarelas de pago, login social, servicios externos |

---

## 4. Qué registro (inventario de activos)

El entregable de esta fase es un **inventario** que luego alimenta `02-enumeration`:

- Lista de hosts/subdominios vivos + tecnología de cada uno.
- Mapa de las apps identificadas y su propósito.
- Roles/usuarios disponibles para el test.
- Puntos de entrada iniciales y candidatos "jugosos" (paneles, APIs, uploads).
- Cualquier dato sensible o config expuesta encontrada de forma pasiva.

Un simple `activos.md` o una tabla vale. Lo importante es que sea reutilizable.

---

## 5. Herramientas (referencia)

Aquí solo el *qué usar para qué*; los comandos concretos van en `04-cheatsheets/`.

- **Subdominios / CT:** amass, subfinder, crt.sh
- **DNS:** dnsx, dig
- **Hosts vivos / puertos:** httpx, nmap, naabu
- **Fingerprinting:** whatweb, wappalyzer, nuclei (tech-detect)
- **OSINT:** theHarvester, dorks, GitHub search
- **Proxy (todo pasa por aquí):** Burp Suite

---

## Errores comunes a evitar

- Empezar a atacar sin haber mapeado → te pierdes superficie.
- No pedir usuarios → informe pobre, solo cubres lo público.
- Ignorar subdominios legacy → suele estar ahí lo más roto.
- No guardar el inventario → repites trabajo en cada fase.

## Referencias

- OWASP WSTG — categoría **WSTG-INFO** (Information Gathering).
- Ver `../estandares-y-metodologias.md` para el marco general.
