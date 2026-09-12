# GraphQL Attacks

- **WSTG:** `WSTG-APIT-01`
- **OWASP:** OWASP API Security Top 10
- **Alias:** ataques a GraphQL

## Qué es

GraphQL expone un único endpoint donde el cliente define la consulta. Una mala configuración permite descubrir todo el esquema, abusar de consultas anidadas o saltarse controles de acceso a nivel de objeto.

## Cómo detectarla

- Localiza el endpoint (`/graphql`, `/api/graphql`, `/v1/graphql`).
- **Introspección:** lanza la introspection query; si responde, tienes todo el esquema (tipos, queries, mutations).
- Herramientas: graphw00f (fingerprint), InQL, GraphQL Voyager (visualizar esquema).

## Cómo explotarla

- **Introspección** → mapa completo de la API y sus operaciones.
- **BOLA/IDOR:** acceder a objetos de otros por ID en queries/mutations sin autorización.
- **Batching/aliases:** múltiples operaciones en una petición para saltarse rate limiting (p. ej. fuerza bruta).
- **DoS:** consultas profundamente anidadas/circulares.
- **Inyecciones** en resolvers que pasan argumentos a SQL/NoSQL/comandos.

## Impacto

Divulgación del esquema y datos, bypass de autorización, fuerza bruta y DoS.

## Cómo remediar

- Deshabilitar introspección en producción.
- Autorización a nivel de objeto en cada resolver.
- Límite de profundidad/complejidad y rate limiting que contemple aliases/batching.
- Validación de entrada en los resolvers.

## Referencias

- OWASP WSTG `WSTG-APIT-01` · OWASP API Security Top 10
- PortSwigger — GraphQL API vulnerabilities

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/12-api.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
