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
```javascript
{
    startAt: "2023-04-03T12:00:00.000Z",
    timezone: "America/Santiago",
    form: "639a48f0a00c1b57a2ea0e52"
}
```
{% endtab %}

{% tab title="Por usuario" %}
{% hint style="warning" %}
La key `service` es requerida cuando agendas por usuario.
{% endhint %}

```javascript
{
    startAt: '2023-04-03T12:00:00.000Z',
    timezone: 'America/Santiago',
    form: '639a48f0a00c1b57a2ea0e52',
    service: '639a490f4362d0a814b5c7fd'
}
```
{% endtab %}
{% endtabs %}

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

{% hint style="info" %}
Deberás usar este método cuando el evento `join` se dispara.
{% endhint %}

```javascript
await calendar.connect();
```

## `join`

Con este método podrás unirte a la videollamada.

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
