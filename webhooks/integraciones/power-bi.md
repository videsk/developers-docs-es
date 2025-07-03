---
description: >-
  A continuación, te explicamos como realizar la integración de Videsk Webhooks
  con PowerBI.
---

# Power BI

{% hint style="info" %}
Si no conoces como funcionan nuestros Webhooks te sugerimos leer nuestra [introducción](../introduccion.md).
{% endhint %}

{% hint style="warning" %}
De momento solo es posible conectar Videsk con Power BI en su versión Pro, la cual puede ser profesional o educativa.
{% endhint %}

{% hint style="warning" %}
Debes contar con autorización para añadir conjunto de datos a tu cuenta de PowerBI.
{% endhint %}

{% hint style="success" %}
Para este tutorial está basado en la **versión web de PowerBI**.
{% endhint %}

## 1. Crear conjunto de datos

Para realizar la conexión utilizaremos la API de Power BI llamada [Real-time streaming](https://docs.microsoft.com/es-es/power-bi/connect-data/service-real-time-streaming).

Debes ir al menú lateral, seleccionar **Examinar > Recientes**, y luego selecciona el espacio de trabajo que desees añadir el conjunto de datos.

![](<../../.gitbook/assets/image (12) (1).png>)

Luego en tu espacio de trabajo deberás dar clic en Nuevo y seleccionar la opción **Conjunto de datos de streaming**.

![](<../../.gitbook/assets/image (17).png>)

Posteriormente, se desplegará un menú lateral derecho, donde deberás selecciona la opción **API** y dar clic en el botón siguiente ubicado en la parte inferior.

![](<../../.gitbook/assets/image (45).png>)

A continuación, te mostrará un formulario el cual deberemos rellenar con los datos que necesitamos exportar. Ingresaremos un nombre de referencia el cual puede ser el que tú quieras.

![](<../../.gitbook/assets/image (30).png>)

## 2. Modelo de datos

Para cargar los datos de forma automática en PowerBI es necesario que indiquemos cuales serán los datos a guardar en este conjunto.

Para ello dejaremos abierto PowerBI unos minutos, abriremos una nueva pestaña y deberás acceder a tu cuenta dashboard ([clic aquí](https://app.videsk.io)), luego seleccionar en el menú la opción de **Webhooks**.

![](<../../.gitbook/assets/image (63).png>)

Ya en Webhooks deberás dar clic en el botón azul ![](<../../.gitbook/assets/image (26) (1).png>)ubicado en la parte superior derecha. Posteriormente, deberás seleccionar la opción **Personalizado**.

![](<../../.gitbook/assets/image (40).png>)

Luego, deberás seleccionar qué tipo de evento quieres enviar a PowerBI.

{% hint style="info" %}
**Para este ejemplo utilizaremos los datos del evento de llamada creada,** pero recuerda que las instrucciones aplican para cualquier otro event&#x6F;**.**
{% endhint %}

![](<../../.gitbook/assets/image (35).png>)

Luego de dar clic en el evento ingresarás al editor Webhook.



Ya en el editor irás al menú lateral derecho, en la parte superior encontrarás una pestaña llamada **Example data**. Allí podrás encontrar un ejemplo de los datos del evento, que en este caso es de una llamada.

{% hint style="info" %}
Los datos que puedes observar son completamente aleatorios y no son asociados a tus clientes o negocio.
{% endhint %}

![](<../../.gitbook/assets/image (19).png>)

{% hint style="info" %}
Te sugerimos hacer un listado con los datos que quieres cargar en PowerBI.
{% endhint %}

Para este ejemplo, utilizaremos datos como **nombre del agente, segmento, tiempo en fila, fecha de inicio, duración y país**.

## 3. Modelo en PowerBI

El siguiente paso es definir el modelo de datos cargar en PowerBI, por lo tanto, debemos volver a la pestaña donde esté PowerBI.

En el formulario verás la sección de **Valores de transmisión**, allí es donde definiremos el nombre de los campos. Para este ejemplo definiremos la siguiente estructura:

| Nombre de valor | Tipo de valor |
| --------------- | ------------- |
| Agente          | Texto         |
| Segmento        | Texto         |
| Tiempo en fila  | Número        |
| Fecha de inicio | DateTime      |
| Duración        | Número        |
| País            | Texto         |

Deberías obtener una estructura de valores de transmisión similar a esto:

```json
[
    {
        "Agente" :"AAAAA555555",
        "Segmento" :"AAAAA555555",
        "Tiempo en fila" :98.6,
        "Fecha de inicio" :"2022-07-07T01:59:39.724Z",
        "Duración" :98.6,
        "País" :"AAAAA555555"
    }
]
```

![](<../../.gitbook/assets/image (14).png>)

{% hint style="warning" %}
Los nombres de valor son sensibles a mayúsculas, minúsculas, espacios, caracteres especiales, etc.
{% endhint %}

{% hint style="info" %}
Recuerda seleccionar correctamente el tipo de valor, de lo contrario los datos podrían no ser utilizados para cálculos.
{% endhint %}

Deberás activar la opción de **Análisis de historial de datos**. La cual permite almacenar los datos que enviemos generando un historial de datos.

![](<../../.gitbook/assets/image (2) (1).png>)

Para finalizar das clic en el botón **Crear**. Posteriormente, nos mostrará datos de integración que usaremos en Videsk.

## 4. Modelo en Videsk

Ya con los datos de integración que nos proporciona PowerBI, iremos a la configuración de Webhooks en Videsk.

* Copia la URL de inserción de PowerBI, y pégala en el campo Método y URL.

![](<../../.gitbook/assets/image (34).png>)

![](<../../.gitbook/assets/image (11).png>)

* Copia el contenido **Raw** de PowerBI y pégalo en el editor de código de Webhook que se encuentra al final del editor.

![](<../../.gitbook/assets/image (39).png>)

![](<../../.gitbook/assets/image (8) (1).png>)

Ahora falta el último y más importante paso que corresponde a extraer los datos dinámicos mediante nuestro lenguaje de marcado.

{% hint style="info" %}
Esto proceso es conocido como ETL, siendo una función incorporada en Videsk lo que permite reducir trabajos tecnológicos, costos y mantenimiento.
{% endhint %}

## 5. Asignar datos a valores

Ahora solo debemos asignar los datos a los valores en la estructura que obtuvimos de PowerBI, la cual se llama JSON.

Para ello utilizaremos el lenguaje de marcado `{{}}`de esta manera podrás asignar los datos.

{% hint style="info" %}
En este ejemplo solo estaremos utilizando 6 tipos de datos, pero puedes extraer más de 30 de una llamada.
{% endhint %}



| Valor           | Dato                                      |
| --------------- | ----------------------------------------- |
| Agente          | `"{{agent.firstname}}{{agent.lastname}}"` |
| Segmento        | `{{parser segment.name}}`                 |
| Tiempo en fila  | `{{parser queue.duration}}`               |
| Fecha de inicio | `{{parser startedAt}}`                    |
| Duración        | `{{parser duration}}`                     |
| País            | `{{parser extraData.countryName}}`        |

{% hint style="info" %}
En este caso usamos `"{{agent.firstname}} {{agent.lastname}}"` entre comillas ya que es un dato compuesto. Cuando es un dato simple te sugerimos utilizar el ayudante [parser](../helpers/parser.md).
{% endhint %}

![](<../../.gitbook/assets/image (10).png>)

```javascript
[
  {
    "Agente": "{{agent.firstname}} {{agent.lastname}}",
    "Segmento": {{parser segment.name}},
    "Tiempo en fila": {{parser queue.duration}},
    "Fecha de inicio": {{parser startedAt}},
    "Duración": {{parser duration}},
    "País": {{parser extraData.countryName}}
  }
]
```

Ya lista la estructura podrás observar en el visualizador (texto en verde) los cambios en vivo y cómo sería la salida de datos.

Verificando que se asemeje la estructura a la que PowerBI espera recibir, solo faltaría asignar un nombre a este Webhook el cual es solo para que tu equipo pueda diferenciar entre múltiples Webhooks.

![](<../../.gitbook/assets/image (36).png>)

No olvides dar clic en **Guardar**.

![](<../../.gitbook/assets/image (61).png>)

Listo! Ya está integrada tu cuenta Videsk con PowerBI. Ya puedes realizar llamadas y se cargarán en tiempo real! :tada:

{% hint style="info" %}
Recuerda asignar el conjunto de datos creado a un informe nuevo o existente.
{% endhint %}

![Ejemplo de informe en PowerBI con datos enviados mediante Webhooks](<../../.gitbook/assets/image (48).png>)

## Ejemplo webhook

```javascript
[
	{
      "segmento": {{parser segment.name}},
      "agente": "{{agent.firstname}} {{agent.lastname}}",
      "fecha_inicio" : {{parser startedAt}},
      "fecha_fin": {{parser endedAt}},
      "cliente_cuelga": {{parser customerLeave}},
      "comentario": {{parser comment.text}},
      "formulario_agente": {{parser agentForm}},
      "formulario_cliente": {{parser baseForm}},
      "sistema_operativo_nombre": {{parser extraData.osName}},
      "sistema_operativo_version": {{parser extraData.osVersion}},
      "navegador_nombre": {{parser extraData.browserName}},
      "navegador_version": {{parser extraData.browserVersion}},
      "dispositivo": {{parser extraData.deviceType}},
      "sitio_web": {{parser extraData.referrer}},
      "zona_horaria": {{parser extraData.timezone}},
      "idioma": {{parser extraData.langName}},
      "region": {{parser extraData.regionName}},
      "ciudad": {{parser extraData.cityName}},
      "latitud": {{parser extraData.coordinates.[0]}},
      "longitud": {{parser extraData.coordinates.[1]}},
      "duracion": {{parser duration}},
      "id" :{{parser id}},
      "duracion_acw": {{parser acwDuration}},
      "duracion_efectiva": {{parser effectiveDuration}},
      "dia": {{#date startedAt 'es-CL'}}{ "day": "numeric" }{{/date}},
      "mes": {{#date startedAt 'es-CL'}}{ "month": "numeric" }{{/date}},
      "ano": {{#date startedAt 'es-CL'}}{ "year": "numeric" }{{/date}}
    }
]
```
