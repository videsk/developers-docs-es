---
description: >-
  A continuación, podrás encontrar como usar nuestros endpoints de exportación
  de datos.
---

# Exportación

{% hint style="info" %}
Considera que este endpoint debe ser usado con un medio de Autorización válido, recomendado usando API Token.
{% endhint %}

{% hint style="warning" %}
Recuerda que existe un límite de 5000 registros por solicitud.
{% endhint %}

## Endpoints

{% content-ref url="llamadas.md" %}
[llamadas.md](llamadas.md)
{% endcontent-ref %}

{% content-ref url="filas.md" %}
[filas.md](filas.md)
{% endcontent-ref %}

{% content-ref url="../grabaciones/cloud/metadata.md" %}
[metadata.md](../grabaciones/cloud/metadata.md)
{% endcontent-ref %}

{% content-ref url="comentarios.md" %}
[comentarios.md](comentarios.md)
{% endcontent-ref %}

{% content-ref url="etiquetas.md" %}
[etiquetas.md](etiquetas.md)
{% endcontent-ref %}

{% content-ref url="reuniones.md" %}
[reuniones.md](reuniones.md)
{% endcontent-ref %}

{% content-ref url="grabaciones.md" %}
[grabaciones.md](grabaciones.md)
{% endcontent-ref %}

{% content-ref url="topicos-ia.md" %}
[topicos-ia.md](topicos-ia.md)
{% endcontent-ref %}

{% content-ref url="sentimientos-ia.md" %}
[sentimientos-ia.md](sentimientos-ia.md)
{% endcontent-ref %}

{% content-ref url="formularios.md" %}
[formularios.md](formularios.md)
{% endcontent-ref %}

{% content-ref url="encuestas.md" %}
[encuestas.md](encuestas.md)
{% endcontent-ref %}

## Columnas

A continuación, tenemos un listado de las columnas que pueden usar para traducir y permtir que estén en tu idioma. Esto es completamente opcional.

{% code lineNumbers="true" %}
```json
{
    "id": "Identificador",
    "segment": "Segmento",
    "agent": "Agente",
    "call": "Llamada",
    "appointment": "Cita",
    "queue": "Fila",
    "createdAt": "Fecha",
    "startTime": "Inicio",
    "endTime": "Fin",
    "duration": "Duración",
    "extraData": "Meta Data",
    "canceled": "Abandonada",
    "assigned": "Asignada",
    "dismissed": "Rechazada",
    "canceledReason": "Razón Cancelación",
    "customerLeave": "Cliente cortó",
    "survey": "Encuesta",
    "comments": "Comentarios",
    "tag": "ID Etiqueta",
    "tags": "Etiquetas",
    "transferredAgent": "Transferido a agente",
    "transferredSegment": "Transferido a segmento",
    "disconnections": "Desconexiones",
    "connections": "Conexiones",
    "userAgent": "Usuario agente",
    "osName": "Sistema operativo (nombre)",
    "osVersion": "Sistema operativo (version)",
    "browserName": "Navegador (nombre)",
    "browserVersion": "Navegador (version)",
    "ip": "IP",
    "ipType": "Tipo IP",
    "referrer": "Referido",
    "timezone": "Zona horaria",
    "langCode": "Idioma (code)",
    "langNative": "Idioma",
    "langName": "Idioma (nombre)",
    "carrierName": "ISP",
    "carrierDomain": "ISP (domain)",
    "continentName": "Continente (nombre)",
    "continentCode": "Continente (code)",
    "countryName": "País",
    "countryCode": "País (code)",
    "regionName": "Region",
    "regionCode": "Region (code)",
    "cityName": "Ciudad",
    "coordinates": "Coordenadas",
    "deviceType": "Dispositivo",
    "agentForm": "ID formulario agente",
    "surveyId": "ID Encuesta",
    "baseForm": "ID formulario cliente",
    "url": "URL",
    "tagName": "ID Etiqueta",
    "tagLabel": "Nombre Etiqueta",
    "createdBy": "Creado por",
    "consent": "Fecha de consentimiento del cliente",
    "sentimentText": "Texto del Sentimiento",
    "sentimentNumber": "Número del Sentimiento",
    "requestedAt": "Solicitado en",
    "summary": "Resumen",
    "topicName": "Nombre del Topico",
    "topicScore": "Puntuación del Topico"
}
```
{% endcode %}
