---
description: >-
  A continuación, te explicamos cómo funcionan nuestros Webhooks de cara a
  soluciones integradoras externas a Videsk.
---

# 🔌 Integradores (3rd party)

Videsk entrega la funcionalidad a sus clientes de enviar solicitudes HTTP a cualquier destino válido, con la flexibilidad de definir la estructura de esta solicitud utilizando variables con nuestro lenguaje de marcado `{{ }}`.

Estas variables se pueden utilizar en cabeceras, parámetros de URL, rutas de URL y cuerpo de la solicitud.

Los métodos disponibles son `POST`, `GET`, `PATCH`, `DELETE`, `PUT`, `OPTIONS` y `HEAD.`

{% hint style="info" %}
Si tienes alguna duda pueden escribirnos a [developers@videsk.io](mailto:developers.videsk.io).
{% endhint %}

## Formatos (encoding)

Dentro de cada webhook nuestros mismos clientes pueden definir el formato del cuerpo de la solicitud, esto ya sea en `JSON`, `XML`, `plain text`, etc.

Considerando que siempre se enviará la cabecera `Content-Type` adecuado.

Si requieres un formato en particular para la integración, basta con entregarle a nuestro cliente un ejemplo del formato/esquema para que este pueda añadirlo dentro de su cuenta y reemplazar los valores con las variables disponibles. **Por ejemplo**, si el cuerpo de la solicitud debe ser un formato `XML`, `JSON`, `CSV`, `YAML`, etc. deberás enviarle algo como:

{% tabs %}
{% tab title="JSON" %}
{% code lineNumbers="true" %}
```json
{
  "id": "REPLACE_ID",
  "values": [
    { "id": "REPLACE_FIELD_ID", "value": "REPLACE_FIELD_VALUE" }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="XML" %}
{% code lineNumbers="true" %}
```xml
<users>
    <user>
        <name>REPLACE_NAME</name>
        <lastConnection>REPLACE_DATE</lastConnection>
    </user>
</users>
```
{% endcode %}
{% endtab %}

{% tab title="CSV" %}
{% code lineNumbers="true" %}
```csv
customerName,customerEmail,customerPhone,salesUser,date
REPLACE_NAME,REPLACE_EMAIL,REPLACE_PHONE,REPLACE_AGENT,REPLACE_DATE
```
{% endcode %}
{% endtab %}

{% tab title="YAML" %}
```yaml
apiVersion: v1
kind: user
spec:
  properties:
    - name: Customer Name
      value: REPLACE_NAME
      
    - name: Customer email
      value: REPLACE_EMAIL
      
    - name: Customer phone
      value: REPLACE_PHONE
```
{% endtab %}
{% endtabs %}

## Errores

En caso que al enviar un webhook a tus sistemas este retorne un código de estado igual o mayor a `500` reintentaremos 60 segundos después de forma incremental, hasta por 3 veces.

En caso de superar un `Rate-limit` de tu sistema, lo intentaremos en el intervalo mencionado anteriormente.

Para códigos de estado menores a `500` y superiores o iguales a `400` capturaremos la respuesta pero no se realizará un intento, ya que estos estados se interpretan como errores en la integración, no de sistemas.

{% hint style="warning" %}
No leemos códigos de estado desde el cuerpo de la respuesta, por lo tanto utiliza códigos de estado de forma correcta.
{% endhint %}

## Limitaciones

Utilizamos tecnología serverless para envío de webhooks, por lo tanto **las IPs utilizadas rotarán**. Actualmente, esta infraestructura está alojada en Google Cloud Platform, por consecuencia no cntrolamos las IPs emisoras de las soliticudes.

Sugerimos utilizar mecanismos de seguridad como tokens en cabeceras para determinar la procedencia de la solicitud, de esta manera podrás bloquear otro tipo de solicitudes.

{% hint style="info" %}
En cada solicitud HTTP enviamos las cabeceras `User-Agent`, `X-Powered-By` y `X-Requested-With`. No utilices estos valores como mecanismo de autenticidad, ya que son fácilmente falsibicables.
{% endhint %}

## Eventos

Estos son los eventos disponibles y dependiendo de cada evento existen ciertos valores disponibles a nivel individual que nuestros clientes pueden obtener en el editor de webhooks.

| Nombre                      | Descripción                                             |
| --------------------------- | ------------------------------------------------------- |
| **Nueva fila**              | Una nueva fila ha sido creada                           |
| **Fila abandonada**         | El cliente ha abandonado la fila                        |
| **Llamada creada**          | Se ha creado una nueva llamada contestada               |
| **Usuario conectado**       | Un agente se ha conectado a su cuenta                   |
| **Usuario desconectado**    | Un agente se ha desconectado de su cuenta               |
| **Nuevo usuario**           | Se ha creado un nuevo agente en su cuenta               |
| **Usuario eliminado**       | Se ha eliminado un agente de su cuenta                  |
| **Usuario editado**         | Se ha editado información de un agente de su cuenta     |
| **Formulario editado**      | Se ha editado información de un formulario de su cuenta |
| **Formulario eliminado**    | Se ha eliminado un formulario de su cuenta              |
| **Nuevo formulario**        | Se ha creado un formulario en su cuenta                 |
| **Formulario recibido**     | Se ha recibido un nuevo formulario de un cliente        |
| **Segmento editado**        | Se ha editado información de un segmento de su cuenta   |
| **Segmento eliminado**      | Se ha eliminado un segmento de su cuenta                |
| **Nuevo segmento**          | Se ha creado un nuevo segmento en su cuenta             |
| **Nuevo comentario**        | Se ha creado un nuevo comentario en una llamada         |
| **Formulario agente**       | Formulario rellenado por el agente                      |
| **Encuesta recibida**       | Encuesta enviada por el cliente a finalizar una llamada |
| **Nueva grabación**         | Nueva grabación recibida                                |
| **Grabación aprobada**      | Grabación aprobada por un revisor o administrador.      |
| **Grabación rechazada**     | Grabación rechazada por un revisor o administrador.     |
| **Grabación eliminada**     | Grabación eliminada por un administrador.               |
| **Nueva reunión**           | Nueva reunión agendada.                                 |
| **Reunión cancelada**       | Una reunión ha sido cancelada.                          |
| **Recordatorio reunión**    | Se debe enviar un recordatorio de reunión               |
| **Notificación ticket QMS** | Notificación de ticket asignado a QMS                   |
