---
description: >-
  A continuación podrás encontrar información de como depurar errores sobre
  webhooks.
---

# 🐞 Errores

Dentro de las funciones que podrás encontrar en webhooks son los registros de errores los cuales te podrán entregar información relacionada a las peticiones que sean enviadas y que puedan fallar ya sean en el proceso de mutación, red (envío) o la plataforma a respondido con un error.

De esta forma podrás identificar de forma fácil qué es lo que no está funcionando correctamente en las integraciones.

Esta función está activa por defecto y no es posible desactivarla.

{% hint style="info" %}
La duración de los registros son de 30 días desde su creación, luego de ello serán eliminados de forma automática.

En caso que requieras mantener los registros más tiempo envíanos un correo a support@videsk.io
{% endhint %}

{% hint style="warning" %}
**Solo detectamos errores con códigos de estado 4XX o superior**. Si la plataforma a integrar responde con errores con códigos de estado 2XX no considerarán como errores.



Para el caso de errores de formato en el webhook, automáticamente capturaremos el error.
{% endhint %}

## Estructura

Los errores capturados durante el proceso de envío contienen una estructura que podrás visualizar de forma sencilla.

![Estructura de un error](<../.gitbook/assets/image (19).png>)

Por defecto podrás ver los siguientes datos, los cuales describiremos a continuación.

### Context

Esta información es relativa al evento como un id de trazabilidad `traceId` y fecha en que se generó `createdAt`.



### Request

Esta información contiene datos de la petición como:

#### URL

Este valor corresponde a la URL que haz ingresado en la configuración del webhook.

#### Method

Este es el método con el cual se envió la petición el cual puede ser `POST`, `GET`, `PATCH`, `PUT`, `HEAD`, `OPTIONS` o `DELETE`.

#### Source

Este valor corresponde a la fuente del error, el cual puede ser `parsing`, que corresponde a la sintaxis `{{mustache}}` o `third-party` que serían errores provocados en respuestas de la plataforma externa como `4XX` o `5XX`.

{% hint style="warning" %}
Recuerda, que solo detectamos errores con códigos de estado 4XX o superior.
{% endhint %}

#### SSL

Valor booleano si se verificó o no el certificado SSL.



### Headers

Estos valores son dinámicos, ya que corresponden a las cabeceras que hayas configurado en el webhook. Por defecto, `Content-Type` es obligatorio.



### Parameters

Estos son valores dinámicos, ya que corresponden a los parámetros por url que hayas configurado en el webhook.



### Response

En caso de ser un error de fuente `third-party` existirán datos como:

#### Status code

Corresponde al código de estado HTTP que ha respondido la plataforma, como `4XX` o `5XX`.

#### Status name

Corresponde al nombre del código de estado HTTP, como `BadRequest`, `NotAuthenticated`, `ServerError`, etc.



### Error

Este valor es de mayor relevancia ya que te indicará el error que se ha provocado, tanto si es error de sintaxis como en el caso que sea un error que haya respondido la plataforma a integrar.

Es posible que no siempre una plataforma responda con contenido, por lo tanto este valor podría ser vacío.

{% hint style="info" %}
Recuerda comparar este valor comparando el parámetro `source` para identificar la causa del error.
{% endhint %}

###

### Payload

Este es el valor sin mutar, es decir, con la sintaxis en puro.

{% hint style="info" %}
Almacenamos este valor para mantener su atomicidad y evitar confusiones si editas el webhook.
{% endhint %}
