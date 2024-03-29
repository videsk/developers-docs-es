---
description: Estos son los métodos disponibles para usar nuestro calendario mediante SDK.
---

# Métodos

Los siguientes métodos te permiten acceder a funciones que cambiarán el comportamiento o ayudantes para ciertas acciones.

{% hint style="warning" %}
Todas las fechas que vayas a utilizar deben estar en horario UTC y formato ISO-8601. Es decir, `2023-04-03T17:00:00.000Z`.
{% endhint %}

## `getServices`

Con este método puedes obtener el listado de servicios asociados a tu cuenta.

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

{% tabs %}
{% tab title="Código" %}
```javascript
const services = await calendar.getServices();
```
{% endtab %}

{% tab title="Respuesta" %}
```javascript
{
    "total": 1,
    "limit": 10,
    "skip": 0,
    "data": [
        {
            "automatic": true,
            "title": "Reunión demo",
            "description": "Reunión demo",
            "id": "61202d32a13b4cf9004eaab1"
        }
    ],
    "cached": true
}
```
{% endtab %}
{% endtabs %}

## `change`

Con este método puedes cambiar la entidad con la cual buscarás fechas según mes y día, además de definir si al agendar se realiza con un servicio general o con un usuario específico. Los valores aceptados son:

* `service` (por defecto)
* `user`

```javascript
calendar
  .change('user')
  .getDays('639a438084d5a0b0690d5cb5');
```

## `getDays`

Con este método puedes obtener el listado de días disponibles en base al ID de un servicio y un mes en específico.

1. `serviceId`: Corresponde al ID del servicio
2. `ISODate`: Corresponde al mes en formato ISO-8601 en horario UTC, por defecto hoy.
3. `timezone`: Corresponde a la zona horario del usuario (opcional)

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

{% tabs %}
{% tab title="Código" %}
```javascript
const days = await calendar.getDays(serviceId);
```
{% endtab %}

{% tab title="Respuesta" %}
El valor que retorna este método corresponde a un listado de fechas como objetos, cada una de las claves entrega la fecha en distintos formatos y **en el idioma del usuario**:

1. `date`: Día de la semana + día del mes + mes abreviado
2. `weekday`: Día de la semana
3. `day`: Día del mes
4. `month`: Mes del año
5. `utc`: Fecha en UTC y formato ISO-8601



```javascript
[
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "day": "3",
        "month": "abril",
        "utc": "2023-04-03T04:00:00.000Z"
    },
    {
        "date": "mar, 04 abr",
        "weekday": "mar",
        "day": "4",
        "month": "abril",
        "utc": "2023-04-04T04:00:00.000Z"
    },
    {
        "date": "mié, 05 abr",
        "weekday": "mié",
        "day": "5",
        "month": "abril",
        "utc": "2023-04-05T04:00:00.000Z"
    },
    {
        "date": "jue, 06 abr",
        "weekday": "jue",
        "day": "6",
        "month": "abril",
        "utc": "2023-04-06T04:00:00.000Z"
    },
    {
        "date": "vie, 07 abr",
        "weekday": "vie",
        "day": "7",
        "month": "abril",
        "utc": "2023-04-07T04:00:00.000Z"
    },
    {
        "date": "lun, 10 abr",
        "weekday": "lun",
        "day": "10",
        "month": "abril",
        "utc": "2023-04-10T04:00:00.000Z"
    },
    {
        "date": "mar, 11 abr",
        "weekday": "mar",
        "day": "11",
        "month": "abril",
        "utc": "2023-04-11T04:00:00.000Z"
    },
    {
        "date": "mié, 12 abr",
        "weekday": "mié",
        "day": "12",
        "month": "abril",
        "utc": "2023-04-12T04:00:00.000Z"
    },
    {
        "date": "jue, 13 abr",
        "weekday": "jue",
        "day": "13",
        "month": "abril",
        "utc": "2023-04-13T04:00:00.000Z"
    },
    {
        "date": "vie, 14 abr",
        "weekday": "vie",
        "day": "14",
        "month": "abril",
        "utc": "2023-04-14T04:00:00.000Z"
    },
    {
        "date": "lun, 17 abr",
        "weekday": "lun",
        "day": "17",
        "month": "abril",
        "utc": "2023-04-17T04:00:00.000Z"
    },
    {
        "date": "mar, 18 abr",
        "weekday": "mar",
        "day": "18",
        "month": "abril",
        "utc": "2023-04-18T04:00:00.000Z"
    },
    {
        "date": "mié, 19 abr",
        "weekday": "mié",
        "day": "19",
        "month": "abril",
        "utc": "2023-04-19T04:00:00.000Z"
    },
    {
        "date": "jue, 20 abr",
        "weekday": "jue",
        "day": "20",
        "month": "abril",
        "utc": "2023-04-20T04:00:00.000Z"
    },
    {
        "date": "vie, 21 abr",
        "weekday": "vie",
        "day": "21",
        "month": "abril",
        "utc": "2023-04-21T04:00:00.000Z"
    },
    {
        "date": "lun, 24 abr",
        "weekday": "lun",
        "day": "24",
        "month": "abril",
        "utc": "2023-04-24T04:00:00.000Z"
    },
    {
        "date": "mar, 25 abr",
        "weekday": "mar",
        "day": "25",
        "month": "abril",
        "utc": "2023-04-25T04:00:00.000Z"
    },
    {
        "date": "mié, 26 abr",
        "weekday": "mié",
        "day": "26",
        "month": "abril",
        "utc": "2023-04-26T04:00:00.000Z"
    },
    {
        "date": "jue, 27 abr",
        "weekday": "jue",
        "day": "27",
        "month": "abril",
        "utc": "2023-04-27T04:00:00.000Z"
    },
    {
        "date": "vie, 28 abr",
        "weekday": "vie",
        "day": "28",
        "month": "abril",
        "utc": "2023-04-28T04:00:00.000Z"
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
El listado de días están en formato horario UTC ISO-8601, esta fecha las debes usar para obtener las horas disponibles.
{% endhint %}

## `getHours`

Con este método puedes obtener el listado de horas disponibles en base al ID de un servicio y un día en específico.

1. `serviceId`: Corresponde al ID del servicio
2. `ISODate`: Corresponde al mes en formato ISO-8601 en horario UTC, por defecto hoy.
3. `timezone`: Corresponde a la zona horario del usuario (opcional)

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

{% tabs %}
{% tab title="Código" %}
```javascript
const hours = await calendar.getHours(serviceId, ISODate);
```
{% endtab %}

{% tab title="Respuesta" %}
El valor que retorna este método corresponde a un listado de fechas como objetos, cada una de las claves entrega la fecha en distintos formatos y **en el idioma del usuario**:

1. `date`: Día de la semana + día del mes + mes abreviado
2. `weekday`: Día de la semana
3. `day`: Día del mes
4. `time`: Hora en formato `HH:mm`
5. `hour`: Hora en formato `HH`
6. `minutes`: Minutos en formato `mm`
7. `utc`: Fecha en UTC y formato ISO-8601



```javascript
[
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "08:00",
        "day": "3",
        "hour": "08",
        "minutes": "0",
        "utc": "2023-04-03T12:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "08:15",
        "day": "3",
        "hour": "08",
        "minutes": "15",
        "utc": "2023-04-03T12:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "08:30",
        "day": "3",
        "hour": "08",
        "minutes": "30",
        "utc": "2023-04-03T12:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "08:45",
        "day": "3",
        "hour": "08",
        "minutes": "45",
        "utc": "2023-04-03T12:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "09:00",
        "day": "3",
        "hour": "09",
        "minutes": "0",
        "utc": "2023-04-03T13:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "09:15",
        "day": "3",
        "hour": "09",
        "minutes": "15",
        "utc": "2023-04-03T13:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "09:30",
        "day": "3",
        "hour": "09",
        "minutes": "30",
        "utc": "2023-04-03T13:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "09:45",
        "day": "3",
        "hour": "09",
        "minutes": "45",
        "utc": "2023-04-03T13:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "10:00",
        "day": "3",
        "hour": "10",
        "minutes": "0",
        "utc": "2023-04-03T14:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "10:15",
        "day": "3",
        "hour": "10",
        "minutes": "15",
        "utc": "2023-04-03T14:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "10:30",
        "day": "3",
        "hour": "10",
        "minutes": "30",
        "utc": "2023-04-03T14:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "10:45",
        "day": "3",
        "hour": "10",
        "minutes": "45",
        "utc": "2023-04-03T14:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "11:00",
        "day": "3",
        "hour": "11",
        "minutes": "0",
        "utc": "2023-04-03T15:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "11:15",
        "day": "3",
        "hour": "11",
        "minutes": "15",
        "utc": "2023-04-03T15:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "11:30",
        "day": "3",
        "hour": "11",
        "minutes": "30",
        "utc": "2023-04-03T15:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "11:45",
        "day": "3",
        "hour": "11",
        "minutes": "45",
        "utc": "2023-04-03T15:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "12:00",
        "day": "3",
        "hour": "12",
        "minutes": "0",
        "utc": "2023-04-03T16:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "12:15",
        "day": "3",
        "hour": "12",
        "minutes": "15",
        "utc": "2023-04-03T16:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "12:30",
        "day": "3",
        "hour": "12",
        "minutes": "30",
        "utc": "2023-04-03T16:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "12:45",
        "day": "3",
        "hour": "12",
        "minutes": "45",
        "utc": "2023-04-03T16:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "13:00",
        "day": "3",
        "hour": "13",
        "minutes": "0",
        "utc": "2023-04-03T17:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "13:15",
        "day": "3",
        "hour": "13",
        "minutes": "15",
        "utc": "2023-04-03T17:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "13:30",
        "day": "3",
        "hour": "13",
        "minutes": "30",
        "utc": "2023-04-03T17:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "13:45",
        "day": "3",
        "hour": "13",
        "minutes": "45",
        "utc": "2023-04-03T17:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "14:00",
        "day": "3",
        "hour": "14",
        "minutes": "0",
        "utc": "2023-04-03T18:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "14:15",
        "day": "3",
        "hour": "14",
        "minutes": "15",
        "utc": "2023-04-03T18:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "14:30",
        "day": "3",
        "hour": "14",
        "minutes": "30",
        "utc": "2023-04-03T18:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "14:45",
        "day": "3",
        "hour": "14",
        "minutes": "45",
        "utc": "2023-04-03T18:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "15:00",
        "day": "3",
        "hour": "15",
        "minutes": "0",
        "utc": "2023-04-03T19:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "15:15",
        "day": "3",
        "hour": "15",
        "minutes": "15",
        "utc": "2023-04-03T19:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "15:30",
        "day": "3",
        "hour": "15",
        "minutes": "30",
        "utc": "2023-04-03T19:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "15:45",
        "day": "3",
        "hour": "15",
        "minutes": "45",
        "utc": "2023-04-03T19:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "16:00",
        "day": "3",
        "hour": "16",
        "minutes": "0",
        "utc": "2023-04-03T20:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "16:15",
        "day": "3",
        "hour": "16",
        "minutes": "15",
        "utc": "2023-04-03T20:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "16:30",
        "day": "3",
        "hour": "16",
        "minutes": "30",
        "utc": "2023-04-03T20:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "16:45",
        "day": "3",
        "hour": "16",
        "minutes": "45",
        "utc": "2023-04-03T20:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "17:00",
        "day": "3",
        "hour": "17",
        "minutes": "0",
        "utc": "2023-04-03T21:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "17:15",
        "day": "3",
        "hour": "17",
        "minutes": "15",
        "utc": "2023-04-03T21:15:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "17:30",
        "day": "3",
        "hour": "17",
        "minutes": "30",
        "utc": "2023-04-03T21:30:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "17:45",
        "day": "3",
        "hour": "17",
        "minutes": "45",
        "utc": "2023-04-03T21:45:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "18:00",
        "day": "3",
        "hour": "18",
        "minutes": "0",
        "utc": "2023-04-03T22:00:00.000Z"
    },
    {
        "date": "lun, 03 abr",
        "weekday": "lun",
        "time": "18:15",
        "day": "3",
        "hour": "18",
        "minutes": "15",
        "utc": "2023-04-03T22:15:00.000Z"
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
El listado de horas están en formato horario UTC ISO-8601, esta fecha para agendar.
{% endhint %}

## `create`

Con este método puedes crear una cita entregando 2 argumentos obligatorios.

1. `entityId`: Id del serivicio o agente
2. `data`: Datos del agendamiento como `Object` siendo:

{% tabs %}
{% tab title="Por servicio" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>    startAt: "2023-04-03T12:00:00.000Z",
    timezone: "America/Santiago",
    form: [{...}],
    referrer: 'https://schedule.example.com',
    token: '0.AOpYir-gaFDC4NreNyXVyXTRPhJREe3dv33S9hdQ0H3lsJkOM'
}
</code></pre>
{% endtab %}

{% tab title="Por usuario" %}
{% hint style="warning" %}
La key `service` solo es requerida cuando agendas por usuario.
{% endhint %}

```javascript
{
    startAt: '2023-04-03T12:00:00.000Z',
    timezone: 'America/Santiago',
    form: [{...}],
    service: '639a490f4362d0a814b5c7fd',
    referrer: 'https://schedule.example.com/',
    token: '0.AOpYir-gaFDC4NreNyXVyXTRPhJREe3dv33S9hdQ0H3lsJkOM'
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Para poder obtener el formulario deberás usar el [SDK de formulario](../forms.md).
{% endhint %}

Por lo que deberás:

```javascript
await calendar.create('639a490f4362d0a814b5c7fd', data);
```

En caso que falle deberás escuchar el evento `error`, donde podrás obtener el motivo del error.

## `cancel`

Con este método puedes cancelar una cita. Este método requiere el uso de un token, por defecto se detecta automáticamente en la URL.

Los parámetros presente en la URL son:

1. `v-schedule-action`: corresponde a la acción a realizar
2. `v-schedule-auth`: corresponde al token de autorización enviado por email

{% hint style="info" %}
Deberás usar este método cuando el evento `modify se dispara.`
{% endhint %}

```javascript
await calendar.cancel();
```

## `reschedule`

Con este método puedes reagendar una cita previamente agendada. Recibe un argumento obligatorio `data` que corresponde a un `Object`.

{% hint style="info" %}
Deberás usar este método cuando el evento `modify se dispara.`
{% endhint %}

```javascript
const data = { date: "2023-04-03T12:00:00.000Z" };
await calendar.reschedule(data);
```

## `getInfo`

Con este método puedes obtener la información de la cita **solo 5 minutos antes** de la hora agendada.

```javascript
await calendar.getInfo();
```

## `connect`

Este método te permite generar la conexión necesaria para unirse a la videollamada. Exige el uso del token de acceso enviado en el email de confirmación o recordatorio.

{% hint style="info" %}
Para acceder al token puedes usar `calendar.appointmentToken`.
{% endhint %}

{% hint style="danger" %}
Solo deberás ejecutar el método `connect` si los parámetros `v-schedule-action` y `v-sechdule-auth` no están presentes en la URL.
{% endhint %}

```javascript
await calendar.connect();
```

## `join`

Con este método podrás unirte a la videollamada.

{% hint style="danger" %}
Deberás ejecutar este método solo 5 minutos antes de la fecha de inicio y máximo 30 minutos después de la fecha de término.
{% endhint %}

```javascript
calendar.join();
```

## `addEventListener`

Con este método podrás añadir oyentes de eventos con un callback. Donde el primer argumento corresponde al nombre del evento y el segundo el callback donde retorna un solo argumento como evento.

Este evento corresponde a un `CustomEvent` donde la información relevante está en la key `detail`.

```javascript
calendar.addEventListener('join', (event) => {
    const { ... } = event.detail;
});
```

## `calendarLink`

Con este método puedes generar enlaces para los servicios de calendario más populares de esta manera tus usuarios podrán añadir la cita con un clic.

```javascript
const link = calendar.calendarLink('google', payload);
```

{% hint style="info" %}
Para abrir el link en otra pestaña puedes utilizar <mark style="color:green;background-color:purple;">`window.open(link, "_blank")`</mark>.
{% endhint %}

El método recibe dos argumentos:

* `type`: nombre del servicio puede ser `google`, `outlook`, `office365`, `yahoo` o `ics`.
* `payload`: formato para generar el enlace

{% tabs %}
{% tab title="Payload" %}
```javascript
{
    "title": String,
    "description": String,
    "start": UTCDate,
    "end": UTCDate,
    "duration": [Number, "minutes"],
    "url": String,
    "busy": Boolean,
    "location": String,
    "guests": [String],
}
```


{% endtab %}

{% tab title="Example" %}
```javascript
{
    "title": "Reunión de {duration} min con {service}",
    "description": "...",
    "start": "2023-02-02T19:10:00.000Z",
    "end": "2023-02-02T19:15:00.000Z",
    "duration": [15, "minutes"],
    "url": "https://videsk.io/?=&v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "busy": true,
    "location": "https://videsk.io/?=&v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "guests": ["john.doe@gmail.com"]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Los valores mencionados se obtienen en la respuesta luego de haber usando el método [`create`](metodos.md#create) or [`reschedule`](metodos.md#reschedule).
{% endhint %}

#### `title`

Valor por defecto que utilizamos en el título inyectando variables.

```handlebars
Reunión de {duration} min con {service}
```

#### `description`

Valor por defecto que utilizamos en la descripción inyectando variables.

```handlebars
Puedes acceder a la reunión a través de este enlace:\n\n{joinURL}. \n\n------------\n\nTambién puedes cancelar la reunión desde este enlace:\n\n{cancelURL}. \n\n------------\n\nO reagendar desde este enlace:\n\n{rescheduleURL}.
```

#### `start`

Corresponde a la fecha de inicio que se entrega como UTC llamada `startAt`.

#### `end`

Corresponde a la fecha de término que se entrega como UTC llamada `endAt`.

#### `duration`

Corresponde a un array con dos índices, el primero es la duración que se obtiene de la respuesta como `duration` y el segundo la unidad de tiempo, que por defecto debe ser `minutes`, ya que `duration` está en minutos.

#### `url`

Corresponde al enlace de acceso a la reunión. Lo obtienes de la respuesta como `joinUrl`.

#### `busy`

Corresponde al estado del usuario cuando inicie la reunión en su calendario. Se sugiere utilizar `true`.

#### `location`

Corresponde a la ubicación de la reunión, que en este caso se utiliza para rellenar con el enlace de acceso. Algunos clientes de calendario detectan este campo como enlace de videollamada. Obtiene este valor de la respuesta como `joinUrl`.

#### `guests`

Corresponde al listado `Array` de invitados a la reunión. Puedes obtener el valor de la respuesta como `email`.
