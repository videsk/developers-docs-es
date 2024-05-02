---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #date

Este tipo de helper tiene como utilidad transformar valores de un `Date` (fechas) a diversos formatos y zonas horarias.

{% hint style="info" %}
Te sugerimos utilizar este helper para enviar las fechas en tu zona horaria local. Videsk envía por defecto en UTC.
{% endhint %}

Los argumentos que recibe este helper son los siguientes:

* Fecha
* Formato ([BCP 47 language tag](../formatos-locales.md))**\***

Luego dentro del helper podrás ingresar como un JSON con las opciones disponibles en la API de Javascript [Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/DateTimeFormat/DateTimeFormat), opciones que darán el formato que necesites junto con el cambio de horario correspondiente a la zona horaria que ingreses.

{% hint style="info" %}
Recuerda que el formato de las opciones es en JSON, cada nombre de opción deberá tener comillas dobles.
{% endhint %}

## Ejemplos de uso

{% code title="Datos de ejemplo" %}
```json
{
    "startedAt": "2021-10-01T05:51:36.000Z"
}
```
{% endcode %}

{% code title="UTC a hora Santiago" %}
```handlebars
{{#date startedAt 'es-CL'}}
    {
        "year": "numeric",
        "month": "numeric",
        "day": "numeric",
        "hour": "numeric",
        "minute": "numeric",
        "second": "numeric",
        "timeZone": "America/Santiago"
    }
{{/date}}
```
{% endcode %}

La salida de este helper será `01-10-2021, 02:51:36`.

***

## Valores por defecto

{% hint style="warning" %}
Lee con detención los valores por defecto, ya que la salida de la fecha podría variar.
{% endhint %}

Por defecto, al usar este helper **sin entregar opciones** la zona horaria será **`UTC`** y en el siguiente formato (en-US) `12/20/2020, 03:23:16`, equivalente a `mes-dia-año, hora:minutos:segundos`.

Adicionalmente, añadimos por defecto las opciones con los siguientes valores, los cuáles son reemplazados solo si están definidos en tus opciones ingresadas.

{% code title="Opciones por defecto" %}
```javascript
{
    "year": "numeric",
    "month": "numeric",
    "day": "numeric",
    "hour": "2-digit",
    "minute": "2-digit",
    "second": "2-digit",
    "hour12": false
}
```
{% endcode %}

### Quitar valores por defecto

Si necesitas quitar valores del formato, podrás definirlos como `null`, por ejemplo:

```handlebars
{{#date startedAt 'es-CL'}}
    { "weekday": null, "timeZone": "America/Mexico_City" }
{{/date}}
```

Esto provocará como en el ejemplo que `weekday` no esté presente en el formato, pero el resto de opciones por defecto seguirán activas.

***

## Opciones

Lee las opciones a continuación, cada una de ellas te permitirá realizar modificaciones en el formato, cálculo en base a calendario, zona horaria, etc.

{% hint style="warning" %}
El nombre de la opción es sensible a mayúsculas y minúsculas.
{% endhint %}

{% hint style="success" %}
Recuerda que son **opciones**, puedes usar todas, algunas o ninguna.
{% endhint %}

{% hint style="info" %}
Las opciones disponibles actualizadas siempre las podrás encontrar [acá](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/DateTimeFormat/DateTimeFormat).
{% endhint %}

#### timeZone

Corresponde a la zona horaria que deseas que la hora se calcule. Por defecto la hora en nuestros sistemas se almacenan en UTC, por lo que podrás realizar la conversión con esta opción.

{% hint style="info" %}
El listado de zonas horarias disponibles lo podrás encontrar acá [TimezoneDB](https://timezonedb.com/time-zones).
{% endhint %}

{% hint style="danger" %}
Recuerda, se escribe **`timeZone`**, no `timezone`.
{% endhint %}

```handlebars
{{#date startedAt}}{ "timeZone": "America/Santiago" }{{/date}}
```

#### hour12

Podrás definir el formato de 24 horas (por defecto) o 12 horas.

```handlebars
{{#date startedAt}}{ "hour12": true }{{/date}}
```

#### hourCycle

Podrás escoger entre los siguientes formatos para la hora:

| hourCycle | Descripción                                                        |
| --------- | ------------------------------------------------------------------ |
| `h12`     | El reloj de 12 horas, con la medianoche comenzando a las 12:00 am. |
| `h23`     | El reloj de 24 horas, con la medianoche a partir de las 0:00.      |
| `h11`     | El reloj de 12 horas, con la medianoche a partir de las 0:00 am.   |
| `h24`     | El reloj de 24 horas, con la medianoche a partir de las 24:00.     |

```handlebars
{{#date startedAt}}{ "hourCycle": "h23" }{{/date}}
```

#### weekday

Te permitirá escoger como se mostrará el día de la semana, mediante los siguientes valores disponibles `long`, `short`, `narrow`.

```handlebars
{{#date startedAt}}{ "weekday": "long" }{{/date}}
```

#### year

Formato del año ya sea `2022` o `22`. Los valores disponibles son `numeric` y `2-digit`.

```handlebars
{{#date startedAt}}{ "year": "numeric" }{{/date}}
```

#### month

Formato del mes ya sea `1`, `01`, `Enero`, `Ene`, `E`. Los valores disponibles son `numeric`, `2-digit`, `long`, `short`, `narrow`.

```handlebars
{{#date startedAt}}{ "month": "numeric" }{{/date}}
```

#### day

Formato del día ya sea `1` o `01`. Los valores disponibles son `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "day": "numeric" }{{/date}}
```

#### hour

Formato de la hora ya sea `1` o `01`. Los valores disponibles son `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "hour": "numeric" }{{/date}}
```

#### minute

Formato de los minutos ya sea `1` o `01`. Los valores disponibles son `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "minute": "numeric" }{{/date}}
```

#### second

Formato de los segundos ya sea `1` o `01`. Los valores disponibles son `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "second": "numeric" }{{/date}}
```

#### timeZoneName

Podrás definir el formato de salida de la zona horaria ya sea `Pacific Standard Time`, `GMT-8`, `GMT-0800`, `Los Angeles Zeit`, `Pacific Time`. Los valores disponibles son `long`, `short`, `shortOffset`, `longOffset`, `shortGeneric`, `longGeneric`.

```handlebars
{{#date startedAt}}{ "timeZoneName": "short" }{{/date}}
```

#### dateStyle

Corresponde al formato de la fecha, sin incluir el tiempo (hora, minutos, segundos, etc). Los valores disponibles son `full`, `long`, `medium` y `short`.

```handlebars
{{#date startedAt}}{ "dateStyle": "full" }{{/date}}
```

#### timeStyle

Corresponse al formato de tiempo sin incluir (año, mes, dia). Los valores disponibles son `full`, `long`, `medium`, `short`.

```handlebars
{{#date startedAt}}{ "timeStyle": "full" }{{/date}}
```

#### calendar

Los valores disponibles son `buddhist`, `chinese`, `coptic`, `dangi`, `ethioaa`, `ethiopic`, `gregory`, `hebrew`, `islamic`, `indian`, `islamic-umalqura`, `islamic-tbla`, `islamic-civil`, `islamic-rgsa`, `iso8601`, `japanese`, `persian`, `roc`.

```handlebars
{{#date startedAt}}{ "calendar": "chinese" }{{/date}}
```

#### dayPeriod

Los valores disponibles son `narrow`, `short`, `long`.

```handlebars
{{#date startedAt}}{ "dayPeriod": "long" }{{/date}}
```

#### numberingSystem

Los valores disponibles son  `arab`, `arabext`,  `bali`, `beng`, `deva`, `fullwide`,  `gujr`, `guru`, `hanidec`, `khmr`,  `knda`, `laoo`, `latn`, `limb`, `mlym`,  `mong`, `mymr`, `orya`, `tamldec`,  `telu`, `thai`, `tibt.`

```handlebars
{{#date startedAt}}{ "numberingSystem": "fullwide" }{{/date}}
```

{% hint style="info" %}
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
