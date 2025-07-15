# 📡 Analytics

Nuestro widget ya cuenta con integraciones nativas con las siguientes herramientas de analytics.

{% hint style="info" %}
Recuerda que estos son integraciones existentes en nuestro widget, para personalizadas puedes seguir usando los [eventos nativos del widget](../api/eventos.md).
{% endhint %}

## Compatibles Plug\&Play

<table data-view="cards"><thead><tr><th data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><a href="adobe-experience-cloud.md">adobe-experience-cloud.md</a></td><td><a href="../../.gitbook/assets/Adobe-Experience-Cloud-logo.jpg">Adobe-Experience-Cloud-logo.jpg</a></td></tr><tr><td><a href="google-analytics-tag-manager.md">google-analytics-tag-manager.md</a></td><td><a href="../../.gitbook/assets/image001.jpg">image001.jpg</a></td></tr></tbody></table>

## Eventos

Los eventos disponibles son casi equivalentes a los que se describen en la [sección de eventos](../api/eventos.md) de nuestro widget, los cuales varían de la siguiente manera:

| Evento Original   | Evento Parseado        | Descripción                                                                                                                                            |
| ----------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| onToggle          | videsk.toggle          | Se dispara cuando cambia la visibilidad del widget (cliente hace clic en burbuja o se ejecuta `videsk.toggle()`). Retorna `status` (boolean) y `date`  |
| onFullToggle      | videsk.fulltoggle      | Se dispara cuando cambia la visibilidad tanto de la burbuja como del cuerpo del widget. Retorna `status` (boolean) y `date`                            |
| onSelected        | videsk.selected        | Se dispara cuando el cliente selecciona un segmento. Retorna `name` (string del segmento), `available` (boolean de disponibilidad de agentes) y `date` |
| onUnavailable     | videsk.unavailable     | Se dispara cuando se intenta llamar pero no hay agentes conectados disponibles                                                                         |
| onQueued          | videsk.queued          | Se dispara cuando el cliente es añadido a la fila virtual de espera. Retorna `position` (number) y `date`                                              |
| onQueueUpdated    | videsk.queueupdated    | Se dispara cuando la posición del cliente en la fila es actualizada. Retorna `position` (number actualizada) y `date`                                  |
| onQueueAbandoned  | videsk.queueabandoned  | Se dispara cuando el cliente abandona la fila virtual (hace clic en cancelar o ejecuta función de abandonar). Retorna `date`                           |
| onDismissed       | videsk.dismissed       | Se dispara cuando un agente rechaza una llamada entrante. Retorna `date`                                                                               |
| onStart           | videsk.start           | Se dispara cuando el cliente ingresa a la videollamada (agente contesta y cliente entra). Retorna `date`                                               |
| onEnd             | videsk.end             | Se dispara cuando termina la videollamada (cliente o agente cuelga). Retorna `date`                                                                    |
| onSurvey          | videsk.survey          | Se dispara cuando el cliente envía la encuesta post-llamada. Retorna `survey` (object) y `date`                                                        |
| onReconnected     | videsk.reconnected     | Se dispara cuando se reconecta a una llamada activa tras recargar/cerrar ventana. Retorna `date`                                                       |
| onConnectionError | videsk.connectionerror | Se dispara cuando hay errores de conexión antes de la llamada. Retorna `date`                                                                          |
