---
description: Almacena tus grabaciones en un entorno propio alojado en Amazon AWS S3.
---

# AWS S3

{% hint style="warning" %}
Una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

Puedes utilizar dos tipos de conexiones dependiendo de tus requisitos de seguridad, mediante:

* Credenciales estáticas
* OIDC

{% hint style="info" %}
Una conexión utilizando OIDC es un mecanísmo más seguro que credenciales estáticas, lo cuál dependerá de tus necesidades.
{% endhint %}

## Información requerida

<table><thead><tr><th>Campo</th><th>Descripción</th><th>Tipo coneión<select multiple><option value="FgK4X2EkyZur" label="Credenciales estáticas" color="blue"></option><option value="HK0Y9q16mKsM" label="OIDC" color="blue"></option></select></th></tr></thead><tbody><tr><td>Bucket name</td><td>Corresponde al nombre del bucket creado. Ejemplo: <code>videsk-storage-s3</code></td><td><span data-option="FgK4X2EkyZur">Credenciales estáticas, </span><span data-option="HK0Y9q16mKsM">OIDC</span></td></tr><tr><td>Region</td><td>Este es el nombre de la región que proporciona AWS S3 al momento de conectarse. Ejemplo: <code>us-west-1</code></td><td><span data-option="FgK4X2EkyZur">Credenciales estáticas, </span><span data-option="HK0Y9q16mKsM">OIDC</span></td></tr><tr><td>Access Key ID</td><td>Corresponde a la clave de acceso (<code>accessKeyId</code> ) que provee AWS para un usuario.</td><td><span data-option="FgK4X2EkyZur">Credenciales estáticas</span></td></tr><tr><td>Secret Access Key</td><td>Corresponde a la clave de acceso secreta (<code>secretAccessKey</code>) que provee AWS para un usuario.</td><td><span data-option="FgK4X2EkyZur">Credenciales estáticas</span></td></tr><tr><td>ARN del rol</td><td>Corresponde al identificador AWS del rol como recurso.</td><td><span data-option="HK0Y9q16mKsM">OIDC</span></td></tr></tbody></table>

## Credenciales estáticas (<5 min)

{% hint style="info" %}
Para integrar Amazon S3 deberás crear un punto de acceso desde la configuración de tu bucket en el menú de **Puntos de acceso**.
{% endhint %}

### 1. Crear usuario IAM

1. Deberás ir a IAM > Personas.
2. Luego, crea un nuevo usuario, configurando la política para acceso S3 con **PutObject**.
3. Añade el ARN y nombre del bucket.
4. Activa la casilla cualquiera para el nombre del objeto.

{% code title="CloudShell version" %}
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::<REPLACE_BUCKET_NAME>/*"
    }
  ]
}
```
{% endcode %}

### 2. Obtener credenciales bucket

1. Deberás ir a la sección de **Claves de acceso**, donde podrás crear una nueva clave.&#x20;

{% hint style="info" %}
Si solicita el caso de uso selecciona "Servicios de terceros".
{% endhint %}

2. Finalmente, obtendrás la clave de acceso y secreto, los cuales deberás copiar y pegar en Videsk.

{% hint style="warning" %}
Considera inmediatamente copiar y pegar estas credenciales, ya que son visibles 1 vez.
{% endhint %}

***

## OIDC (>10 min)

Si tu negocio requiere una seguridad nivel enterprise para cumplimiento normativo, puedes seguir estos pasos de configuración.

| Campo             | Valor                                                          |
| ----------------- | -------------------------------------------------------------- |
| Audience          | `cloud-connector@bridge-fed-connector.iam.gserviceaccount.com` |
| URL del proveedor | `https://accounts.google.com/`                                 |

### 1. Agregar proveedor de identidad

Nuestra infraestructura actualmente está alojada en Google Cloud Platform, por lo que para enviar las grabaciones a tu infraestructura AWS es requerido los siguientes datos:

{% hint style="warning" %}
Debido a una limitación de la interfaz de AWS es necesario agregar el proveedor de identidad mediante CloudShell.
{% endhint %}

{% code fullWidth="false" %}
```bash
aws iam create-open-id-connect-provider \
    --url https://accounts.google.com \
    --client-id-list cloud-connector@bridge-fed-connector.iam.gserviceaccount.com \
    --thumbprint-list 1c58a3a8518e8759bf075b76b750d4f2df264fcd
```
{% endcode %}

### 2. Crear rol IAM con Trust Policy

{% @arcade/embed flowId="40hWhSAOez8XW08ZB53R" url="https://app.arcade.software/share/40hWhSAOez8XW08ZB53R" %}

Al crear la política te recomendamos utilizar la siguiente política la cual puedes copiar y pegar, reemplazando el nombre de tu bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::<REPLACE_BUCKET_NAME>/*"
    }
  ]
}
```

### 3. Configurar ajuste de grabación

{% @arcade/embed flowId="IFcKWdQze46WNkRhqchj" url="https://app.arcade.software/share/IFcKWdQze46WNkRhqchj" %}

***

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
                "AWS": "arn:aws:iam::<ACCOUNT-ID-WITHOUT-HYPHENS>:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<YOUR-BUCKET-NAME>/uploads/*"
        },
        {
            "Sid": "DenyNonPrefixedWrites",
            "Effect": "Deny",
            "Principal": {
                "AWS": "arn:aws:iam::<ACCOUNT-ID-WITHOUT-HYPHENS>:user/videsk-connector"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<YOUR-BUCKET-NAME>/*",
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

Referencia: [S3 ARN Format](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html).

[^1]: Esto es el prefijo del archivo
