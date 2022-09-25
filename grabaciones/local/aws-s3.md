---
description: >-
  Aprende como sincronizar las grabaciones con descarga local hacia un bucket
  AWS S3
---

# AWS S3

{% hint style="warning" %}
Recuerda que es de tú responsabilidad restringir el acceso a las grabaciones en un bucket AWS S3.
{% endhint %}

{% hint style="danger" %}
Te recomendamos encarecidamente gestionar las credenciales de forma correcta restringiendo acceso a escritura, sin lectura o modificación de los archivos existentes, junto con políticas de extensiones a `.mp4` y `.webm`.
{% endhint %}

Antes de configurar la carpeta a sincronizar te recomendamos configurar la ubicación de descarga de las grabaciones del navegador del agente.

{% content-ref url="ubicacion-de-descargas.md" %}
[ubicacion-de-descargas.md](ubicacion-de-descargas.md)
{% endcontent-ref %}

## S3 Browser

Este gestor gratuito de S3 con interfaz que te permite administrar un bucket, definir permisos y crear una sincronización de archivos locales a S3.

{% hint style="info" %}
Solo disponible para Windows.
{% endhint %}

Para ello te sugerimos dirigirte a la [página de descarga](https://s3browser.com/download.aspx) y posteriormente lee la documentación de [cómo sincronizar una carpeta local hacia S3](https://s3browser.com/amazon-s3-folder-sync.aspx) de forma segura.

{% hint style="danger" %}
Te sugerimos restringir permisos solo de escritura y de ser posible extensiones a `.webm` y `.mp4`.
{% endhint %}

## AWS CLI

AWS CLI es una herramienta oficial de AWS que permite gestionar buckets S3 mediante línea de comandos.

Para ello dirígite a la [página de AWS CLI](https://aws.amazon.com/es/cli/) e instala la herramienta en los equipos.

Te sugerimos ver el siguiente video de teckno.net donde explica cómo realizar una configuración de `AWS CLI` para la sincronización de archivos local hacia un S3.

O puedes acceder directamente a su publicación: [https://www.tekco.net/?p=1590](https://www.tekco.net/?p=1590)

{% embed url="https://www.youtube.com/watch?v=3vpcsvNZQsY" %}

{% hint style="warning" %}
Recuerda almacenar de forma segura las credenciales S3 mediante cifrado.
{% endhint %}

{% hint style="info" %}
Si tienes dudas puedes contactarnos a [support@videsk.io](mailto:support@videsk.io).
{% endhint %}
