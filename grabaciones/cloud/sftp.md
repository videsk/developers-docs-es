---
description: Almacena tus grabaciones en un entorno propio alojado en un servidor SFTP.
---

# SFTP

Las credenciales de FTP necesarias son las siguientes:

{% hint style="warning" %}
Por razones de seguridad, una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

## Host

Corresponde al dominio (FQDN) o dirección IP del servidor de destino. Ejemplo: `sftp.example.com`

{% hint style="info" %}
Ingresa el dominio o dirección IP sin el puerto.
{% endhint %}

## Username

Corresponde al nombre de usuario autorizado para subir los archivos. Ejemplo: `videsk`

{% hint style="warning" %}
Te sugerimos crear este usuario con permisos de escritura en una ruta específica.
{% endhint %}

{% hint style="danger" %}
Por razones de seguridad denegamos el uso del usuario `root`. Evita usar un super usuario.
{% endhint %}

## Port

Corresponde al puerto del servidor FTP de destino. Ejemplo: `21`

{% hint style="info" %}
Por defecto el valor es el puerto 21.
{% endhint %}

## TLS

Activa o desactiva la conexión mediante verificación TLS.

{% hint style="info" %}
Te recomendamos utilizar conexiones con TLS activado, lo que nos permite asegurar una conexión cifrada entre nuestros servidores y el de destino.
{% endhint %}
