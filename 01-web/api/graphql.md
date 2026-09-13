# GraphQL Attacks — Índice

- **WSTG:** `WSTG-APIT-01`
- **OWASP:** OWASP API Security Top 10
- **Alias:** ataques a GraphQL

## Qué es

GraphQL expone un único endpoint donde el cliente define la consulta. Una mala configuración permite descubrir todo el esquema, saltarse autorización a nivel de objeto o abusar de consultas para DoS/fuerza bruta.

## Localizar endpoint

```
/graphql  /api/graphql  /v1/graphql  /graphql/console  /graphiql
```
Fingerprint del motor con **graphw00f**.

## Fichas a fondo

| Tema | Ficha |
|---|---|
| Introspección y descubrimiento del esquema | [introspection.md](introspection.md) |
| Abuso de autorización y batching (BOLA, brute force, DoS) | [authz-batching.md](authz-batching.md) |

## Impacto

Divulgación del esquema y datos, bypass de autorización, fuerza bruta y DoS.

## Remediación (común)

- Deshabilitar introspección en producción.
- Autorización a nivel de objeto en cada resolver.
- Límite de profundidad/complejidad y rate limiting que contemple aliases/batching.
- Validación de entrada en resolvers (inyecciones dentro de argumentos).

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/graphql.md`
- Checklist: `../../00-metodologia/06-checklists/12-api.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-APIT-01` · OWASP API Security Top 10 · PortSwigger — GraphQL
