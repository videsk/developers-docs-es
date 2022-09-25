---
description: Almacena tus grabaciones en un entorno propio alojado en GCP Storage
---

# GCP

{% hint style="warning" %}
Una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

Las credenciales necesarias para almacenar en GCP son:

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
