---
description: Almacena tus grabaciones en un entorno propio alojado en Amazon AWS S3
---

# AWS S3



{% hint style="warning" %}
Una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

{% hint style="info" %}
Para integrar Amazon S3 deberás crear un punto de acceso desde la configuración de tu bucket en el menú de **Puntos de acceso**.
{% endhint %}

## Sugerencias de configuración

Deberás crear un perfil IAM exclusivo para la conexión con la cual puedas realizar una trazabilidad de acceso y limitaciones de acciones sobre tu bucket S3.

* Te sugerimos activar permisos IAM para S3 con escritura en **PutObject**.
* Añade un ARN con el nombre del bucket y activa la casilla cualquiera para el nombre del objeto.

{% hint style="danger" %}
No crees un perfil IAM con acceso completo, **protege tus activos**.
{% endhint %}

Puedes copiar y pegar esta política en el editor JSON de IAM, **recuerda reemplazar el nombre de tu bucket**.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "16933222-fba4-4de3-bf3e-427759b73a9d",
            "Effect": "Allow",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<REPLACE_BUCKET_NAME>/*"
        }
    ]
}
```

<figure><img src="../../.gitbook/assets/Captura desde 2022-09-24 21-30-32.png" alt=""><figcaption><p>Deberías visualizar una configuración similar</p></figcaption></figure>

Finalmente tras crear la política deberás acceder a la pestaña **Credenciales de seguridad** y luego haz clic en el botón **Generar claves de acceso**.

## Access key ID

Corresponde al `accessKeyId` que provee AWS S3 al momento en que creas un bucket.

## Secret access key

Corresponde a la llave de acceso secreta (`secretAccessKey`) que provee AWS S3 para conectarse de forma externa al bucket.

## Region

Este es el nombre de la región que proporciona AWS S3 al momento de conectarse. Ejemplo: `us-west-1`

## Bucket name

Corresponde al nombre del bucket creado. Ejemplo: `videsk-storage-s3`

## Sugerencias de seguridad

Si estás utilizando un bucket multipropósito te sugerimos añadir políticas de control de acceso a tus bucket para evitar accesos no deseados a otros ficheros.

En el siguiente ejemplo usamos un perfil IAM `videsk-connector` para definir reglas de escritura en la carpeta (prefijos) [`uploads/`](#user-content-fn-1)[^1] , siendo `ACCOUNT-ID-WITHOUT-HYPHENS` tu ID de cuenta.

{% hint style="info" %}
Recuerda reemplazar los valores de ejemplo con tus ajustes.
{% endhint %}

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPrefixedWrites",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::ACCOUNT-ID-WITHOUT-HYPHENS:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/uploads/*"
        },
        {
            "Sid": "DenyNonPrefixedWrites",
            "Effect": "Deny",
            "Principal": {
                "AWS": "arn:aws:iam::ACCOUNT-ID-WITHOUT-HYPHENS:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*",
            "Condition": {
                "StringNotLikeIfExists": {
                    "s3:prefix": [
                        "uploads/*"
                    ]
                }
            }
        }
    ]
}

```

Referencia: [https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html)

[^1]: Esto es el prefijo del archivo
