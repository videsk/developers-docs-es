---
description: Almacena tus grabaciones en un entorno propio alojado en GCP Storage
---

# GCP

{% hint style="warning" %}
Una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

## Sugerencias de configuración

### 1. Crear función/rol

Deberás crear una nueva función, para ello ve a IAM, luego haz clic en **Crear función**, y rellena los campos requeridos. Te sugerimos ingresar el nombre de función o rol como "Videsk Connector", así podrás buscarlo más fácilmente.

En la sección de permisos deberás dar clic en el botón **Añadir permisos**, donde buscarás **Storage Object Creator**, para finalmente seleccionar los permisos:

* `storage.multipartUploads.create`
* `storage.multipartUploads.abort`
* `storage.objects.create`

Haz clic en **Crear**.

{% hint style="info" %}
En caso que tu interfaz esté en inglés una función corresponde a **Roles** en el menú de IAM.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Deberás usar este rol para crear las credenciales en el siguiente paso. Así aseguras que solo tendremos permisos para crear archivos, no leer o modificar.
{% endhint %}

### 2. Crear credenciales

Ve a **APIs & Services**, luego en la parte superior haz clic en **Crear credenciales**, y después en **Cuenta de servicio**. Ingresa los campos requeridos, donde Nombre de la cuenta de servicio puede ser "_Videsk Connector_" y ID de la cuenta de servicio "_videsk-connector-1234_" (_esto es opcional, puedes escoger cualquier nombre_). Haz clic en **crear y continuar**.

Luego en el rol a seleccionar busca "videsk", y selecciona el rol creado anteriormente.

Adicionalmente, puedes añadir una condición IAM, donde limites el acceso al Servicio storage.googleapis.com y el nombre del bucket.

Si deseas (opcional) puedes crear estas condiciones copiando y pegando el siguiente snippet en **Editor de condición**.

```sql
resource.service == "storage.googleapis.com" &&
resource.name == "my-bucket-name"
```

Haz clic en **Continuar** y luego en el botón **Listo.**

{% hint style="info" %}
No es requerido otorgar acceso a usuarios a la cuenta de servicio.
{% endhint %}

Luego deberás buscar la cuenta de servicio, dando clic en el nombre. Posteriormente en el menú superior haz clic en claves, **Añadir clave** > **Crear nueva clave**.

Finalmente haz clic en el tipo de clave **JSON**.

<figure><img src="../../.gitbook/assets/image (8) (2).png" alt=""><figcaption><p>Generar clave privada</p></figcaption></figure>

Como último paso deberás pegar el contenido del archivo JSON en nuestra interfaz de configuración y Probar las credenciales.

{% hint style="info" %}
Solo puedes probar las credenciales la primera vez que las creas, luego no podrás utilizar la función.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

## Opción 1

### Bucket Name

Corresponde al nombre del `bucket` específico donde se almacenarán los archivos.

### Key file credentials

Archivo `JSON` de credenciales autogenerado por Google Cloud asociado a una cuenta de servicio que tenga permisos de escritura.

{% hint style="info" %}
Este archivo entrega una configuración más rápida y segura, aunque cumple con el mismo objetivo que las credenciales por separado.
{% endhint %}

#### Ejemplo:

```json
{
  "type": "service_account",
  "project_id": "PROJECT_ID",
  "private_key_id": "KEY_ID",
  "private_key": "-----BEGIN PRIVATE KEY-----\nPRIVATE_KEY\n-----END PRIVATE KEY-----\n",
  "client_email": "SERVICE_ACCOUNT_EMAIL",
  "client_id": "CLIENT_ID",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/SERVICE_ACCOUNT_EMAIL"
}
```

## Opción 2

### Project ID

Corresponde al ID del proyecto en el que se encuentra el `bucket` de almacenamiento destinado a los archivos.

### Bucket Name

Corresponde al nombre del `bucket` específico donde se almacenarán los archivos.

### Private Key

Clave privada otorgada a la cuenta de servicio con permiso de escritura para crear archivos.

### Client email

Dirección de correo electrónico de la cuenta de servicio asociada y que cuenta con los permisos de escritura.

{% content-ref url="metadata.md" %}
[metadata.md](metadata.md)
{% endcontent-ref %}
