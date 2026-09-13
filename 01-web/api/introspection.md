# GraphQL — Introspección y descubrimiento

Ver índice: [graphql.md](graphql.md). **Solo sobre objetivos autorizados.**

## Introspección completa

```graphql
query { __schema { types { name fields { name } } } }
```

```bash
curl -s -X POST https://sitio/graphql -H 'Content-Type: application/json' \
  -d '{"query":"{__schema{queryType{name} types{name kind fields{name}}}}"}'
```
Devuelve todo el esquema: tipos, queries, mutations, argumentos → el mapa de la API.

## Enumerar un tipo

```graphql
{ __type(name:"User") { name fields { name type { name kind } } } }
```

## Si la introspección está deshabilitada

- **Sugerencias de campo:** muchos servidores devuelven "Did you mean ...?" ante un campo mal escrito → filtra nombres válidos.
- **clairvoyance:** reconstruye el esquema a partir de esas sugerencias.
- **Wordlists** de campos/tipos comunes por diccionario.

## Herramientas

```
graphw00f      # fingerprint del motor (Apollo, Hasura, etc.)
InQL           # extensión de Burp: introspección + generación de queries
clairvoyance   # esquema sin introspección
```

## Notas

- La introspección abierta en producción es en sí un hallazgo (information disclosure).
- Con el esquema en mano, ataca autorización y abusos → [authz-batching.md](authz-batching.md).
