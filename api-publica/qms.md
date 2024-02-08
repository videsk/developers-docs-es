---
description: A continuación verás como utilizar nuestra API para conectar con sistemas QMS.
---

# QMS

Con nuestra Rest API de llamadas podrás generar llamadas en vivo para tus clientes de manera programática integrado con sistemas QMS (Queue management systems).

Los endpoints a continuación son públicos, es decir, se antepone `/public/` como medio diferenciador de endpoints privados.

{% hint style="warning" %}
Recomendamos hacer uso de los códigos de estados para aplicar lógica a tus integraciones.
{% endhint %}

{% hint style="info" %}
Debido a la nomenclatura de sistemas QMS se menciona `queue`como referencia a segmentos, siendo similares.
{% endhint %}

## Consideraciones

Debes considerar que la forma de comunicación entre nuestro ACD y POCs (puntos de contactos) se realiza de forma automática. Cuando un ticket (llamada) se asigna a un ejecutivo y este contesta se dispara nuestro webhook QMS el cual se configura en cada cuenta.

Puedes ver más información en la [documentación de Webhooks](broken-reference).

### Flujo de integración

Glosario:

* QMS: Sistema de administración de filas (Queues Management System)
* POC: Puntos de contacto (Point of contact)
* Screens: Pantallas con turnos

```mermaid
sequenceDiagram

    participant Screens
    participant QMS
    participant Videsk

    QMS->>Videsk: Solicita añadir cliente a fila video
    Note over QMS,Videsk: Respuesta de éxito o falla inmediata
    Videsk->>QMS: Responde a solicitud de adición fila
    activate Videsk
    Videsk-->>Videsk: Asigna llamada a un agente y POC
    Videsk->>QMS: (Webhook) Notificación de asignación
    deactivate Videsk
    QMS->>Screens: Notifica a cliente número POC en pantalla
    Screens->>Videsk: Cliente se sienta frente a POC

```

{% swagger method="post" path="/branches/:branch/queues/:queue" baseUrl="https://api.videsk.io/public/video-contact-center" summary="Solicitud de añadir a fila" %}
{% swagger-description %}
Solicitar añadir a la fila un ticket de QMS
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Backend API Key
{% endswagger-parameter %}

{% swagger-parameter in="body" name="integrationData" type="Mixed" %}
Datos del ticket (Array, Object o String)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="branch" type="String" required="true" %}
ID de oficina
{% endswagger-parameter %}

{% swagger-parameter in="path" name="queue" type="String" required="true" %}
ID de fila (segment)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="form" type="String" %}
ID del formulario
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Ticket añadido a la fila" %}
```json
{
    "id": "652a1ae848880e168884e49b",
    "segment": "Trámites ABC"
}
```

La respuesta contiene el ID interno del ticket en la fila y el nombre del segmento (fila)
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="ID de oficina o segmento incorrecto" %}
```json
{
    "name": "NotFound",
    "message": "The segment for the branch \"1234567890\" is not assigned or the branch id is incorrect",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Sin agentes disponibles" %}
```json
{
    "name": "NotAcceptable",
    "message": "Not agent available in the segment \"652a1ae848880e168884e49b\", please try later.",
    "code": 406,
    "className": "not-acceptable",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="No es posible procesar la solicitud" %}
```json
{
    "name": "Unprocessable",
    "message": "We're not able to request adding you to the queue, try again.",
    "code": 422,
    "className": "unprocessable",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="428: Precondition Required" description="Formulario obligatorio" %}
```json
{
    "name": "PreconditionRequired",
    "message": "Is mandatory to provide a forms submission id.",
    "code": 426,
    "className": "precondition-require",
    "errors": {}
}
```

Para más información de los errores generados por formulario visita la [documentación de formularios](formularios.md).
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
El valor `integrationData`será usado para ser enviado mediante nuestros webhooks, por lo que es útil en caso que desees enviar un ID interno, metadata, etc. para la sincronización. **Tiene un límite de 50 Kb**, recibe cualquier tipo de dato `String`, `Objetcs`, `Arrays`, etc.



Esto no se mostrará al agente, solo estará disponible en los webhooks de integración.
{% endhint %}

{% swagger method="get" path="/branches" baseUrl="https://api.videsk.io/public/video-contact-center" summary="Obtener listado de oficinas" %}
{% swagger-description %}
Listado de oficinas usando API Key
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Backend API Key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de oficinas" %}
```json
[
    {
        "location": [
            7,
            9
        ],
        "label": "Virtual Main branch",
        "address": "1345 Main Street, CA",
        "name": "branch-main-1345",
        "id": "652720d479497a1b62df288b"
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/branches/:branch/queues" baseUrl="https://api.videsk.io/public/video-contact-center" summary="Obtener listado de filas" %}
{% swagger-description %}
Listado de filas disponibles en la oficina
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Backend API Key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de filas disponibles" %}
```json
[
    {
        "name": "Atención a clientes",
        "id": "652a1ae848880e168884e49b",
        "users": 0
    }
]
```

La respuesta incluye `users` que corresponde al número de agentes disponibles para realizar un atención inmediata.
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Oficina no encontrada" %}
```json
{
    "name": "NotFound",
    "message": "The branch was not found",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/branches/:branch/queues/:queue" baseUrl="https://api.videsk.io/public/video-contact-center" summary="Obtener información fila" %}
{% swagger-description %}
Obtén información de una fila individual
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Backend API Key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Información de la fila" %}
```json
{
    "name": "Atención a clientes",
    "id": "652a1ae848880e168884e49b",
    "users": 1
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Oficina o segmento no encontrado" %}
```json
{
    "name": "NotFound",
    "message": "The branch or segment was not found",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}
{% endswagger %}
