---
description: >-
  A continuaci贸n podr谩s encontrar informaci贸n de como depurar errores sobre
  webhooks.
---

# 馃悶 Errores

Dentro de las funciones que podr谩s encontrar en webhooks son los registros de errores los cuales te podr谩n entregar informaci贸n relacionada a las peticiones que sean enviadas y que puedan fallar ya sean en el proceso de mutaci贸n, red (env铆o) o la plataforma a respondido con un error.

De esta forma podr谩s identificar de forma f谩cil qu茅 es lo que no est谩 funcionando correctamente en las integraciones.

Esta funci贸n est谩 activa por defecto y no es posible desactivarla.

{% hint style="info" %}
La duraci贸n de los registros son de 30 d铆as desde su creaci贸n, luego de ello ser谩n eliminados de forma autom谩tica.

En caso que requieras mantener los registros m谩s tiempo env铆anos un correo a support@videsk.io
{% endhint %}

{% hint style="warning" %}
**Solo detectamos errores con c贸digos de estado 4XX o superior**. Si la plataforma a integrar responde con errores con c贸digos de estado 2XX no considerar谩n como errores.



Para el caso de errores de formato en el webhook, autom谩ticamente capturaremos el error.
{% endhint %}

## Estructura

Los errores capturados durante el proceso de env铆o contienen una estructura que podr谩s visualizar de forma sencilla.

![Estructura de un error](<../.gitbook/assets/image (56).png>)

Por defecto podr谩s ver los siguientes datos, los cuales describiremos a continuaci贸n.

### Context

Esta informaci贸n es relativa al evento como un id de trazabilidad `traceId` y fecha en que se gener贸 `createdAt`.



### Request

Esta informaci贸n contiene datos de la petici贸n como:

#### URL

Este valor corresponde a la URL que haz ingresado en la configuraci贸n del webhook.

#### Method

Este es el m茅todo con el cual se envi贸 la petici贸n el cual puede ser `POST`, `GET`, `PATCH`, `PUT`, `HEAD`, `OPTIONS` o `DELETE`.

#### Source

Este valor corresponde a la fuente del error, el cual puede ser `parsing`, que corresponde a la sintaxis `{{mustache}}` o `third-party` que ser铆an errores provocados en respuestas de la plataforma externa como `4XX` o `5XX`.

{% hint style="warning" %}
Recuerda, que solo detectamos errores con c贸digos de estado 4XX o superior.
{% endhint %}

#### SSL

Valor booleano si se verific贸 o no el certificado SSL.



### Headers

Estos valores son din谩micos, ya que corresponden a las cabeceras que hayas configurado en el webhook. Por defecto, `Content-Type` es obligatorio.



### Parameters

Estos son valores din谩micos, ya que corresponden a los par谩metros por url que hayas configurado en el webhook.



### Response

En caso de ser un error de fuente `third-party` existir谩n datos como:

#### Status code

Corresponde al c贸digo de estado HTTP que ha respondido la plataforma, como `4XX` o `5XX`.

#### Status name

Corresponde al nombre del c贸digo de estado HTTP, como `BadRequest`, `NotAuthenticated`, `ServerError`, etc.



### Error

Este valor es de mayor relevancia ya que te indicar谩 el error que se ha provocado, tanto si es error de sintaxis como en el caso que sea un error que haya respondido la plataforma a integrar.

Es posible que no siempre una plataforma responda con contenido, por lo tanto este valor podr铆a ser vac铆o.

{% hint style="info" %}
Recuerda comparar este valor comparando el par谩metro `source` para identificar la causa del error.
{% endhint %}

###

### Payload

Este es el valor sin mutar, es decir, con la sintaxis en puro.

{% hint style="info" %}
Almacenamos este valor para mantener su atomicidad y evitar confusiones si editas el webhook.
{% endhint %}
