---
description: >-
  The documentation for using this helper is as follows.
---

# #date

This type of helper is useful for transforming values of a `Date` (dates) to various formats and time zones.

{% hint style="info" %}
We recommend using this helper to send dates in your local time zone. Videsk sends in UTC by default.
{% endhint %}

#### Sample data

```json
{
  "startedAt": "2021-10-01T05:51:36.000Z"
}
```

## Usage examples

{% code title="UTC to Local Time" %}
```handlebars
// UTC to Santiago, Chile time and format
{{#date startedAt 'es-CL'}}{ "year": "numeric", "month": "numeric", "day": "numeric", "hour": "numeric", "minute": "numeric", "second": "numeric", "timeZone": "America/Santiago" }{{/date}}
// Output: 10-01-2021 02:51:36

// UTC to Mexico Time
```
{% endcode %}

This helper receives the following arguments

* Date
* Format ([BCP 47 language tag](https://www.techonthenet.com/js/language\_tags.php))**\***

Following these, you can include an `Object` inside the helper with the options available in the Javascript [Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/DateTimeFormat/DateTimeFormat) API, which are used to format the date and change the time zone as needed.

## Options

Read the options below, each of which will allow you to make changes to the format, calculation based on calendar, time zone, etc.

{% hint style="warning" %}
The name of the option is case-sensitive.
{% endhint %}

{% hint style="success" %}
Remember, these are **options**, you can use all, some, or none.
{% endhint %}

{% hint style="info" %}
The most up-to-date available options can always be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/DateTimeFormat/DateTimeFormat).
{% endhint %}

#### timeZone

The time zone you want the time to be calculated in. By default, the time in our systems is stored in UTC, so you can perform the conversion with this option.

{% hint style="info" %}
You can find the list of available time zones here [TimezoneDB](https://timezonedb.com/time-zones).
{% endhint %}

{% hint style="danger" %}
Remember, it's written **`timeZone`**, not `timezone`.
{% endhint %}

```handlebars
{{#date startedAt}}{ "timeZone": "America/Santiago" }{{/date}}
```

#### hour12

You can define the 24-hour format (default) or 12-hour format.

```handlebars
{{#date startedAt}}{ "hour12": true }{{/date}}
```

#### hourCycle

You can choose between the following formats for the time:

| hourCycle | Description |
| --------- | ------------------------------------------------------------------ |
| `h12` | The 12-hour clock, with midnight starting at 12:00 am. |
| `h23` | The 24-hour clock, with midnight starting at 0:00. |
| `h11` | The 12-hour clock, with midnight starting at 0:00 am. |
| `h24` | The 24-hour clock, with midnight starting at 24:00. |

```handlebars
{{#date startedAt}}{ "hourCycle": "h23" }{{/date}}
```

#### weekday

Will allow you to choose how the day of the week is displayed, using the following available values `long`, `short`, `narrow`.

```handlebars
{{#date startedAt}}{ "weekday": "long" }{{/date}}
```

#### year

Year format, either `2022` or `22`. The available values are `numeric` and `2-digit`.

```handlebars
{{#date startedAt}}{ "year": "numeric" }{{/date}}
```

#### month

Month format, either `1`, `01`, `January`, `Jan`, `E`. The available values are `numeric`, `2-digit`, `long`, `short`, `narrow`.

```handlebars
{{#date startedAt}}{ "month": "numeric" }{{/date}}
```

#### day

Day format, either `1` or `01`. The available values are `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "day": "numeric" }{{/date}}
```

#### hour

Hour format, either `1` or `01`. The available values are `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "hour": "numeric" }{{/date}}
```

#### minute

Minute format, either `1` or `01`. The available values are `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "minute": "numeric" }{{/date}}
```

#### second

Second format, either `1` or `01`. The available values are `numeric`, `2-digit`.

```handlebars
{{#date startedAt}}{ "second": "numeric" }{{/date}}
```

#### timeZoneName

You'll be able to define the time zone output format, either `Pacific Standard Time`, `GMT-8`, `GMT-0800`, `Los Angeles Zeit`, `Pacific Time`. The available values are `long`, `short`, `shortOffset`, `longOffset`, `shortGeneric`, `longGeneric`.

```handlebars
{{#date startedAt}}{ "timeZoneName": "short" }{{/date}}
```

#### dateStyle

Corresponds to the format of the date, not including the time (hours, minutes, seconds, etc.). The available values are `full`, `long`, `medium` and `short`.

```handlebars
{{#date startedAt}}{ "dateStyle": "full" }{{/date}}
```

#### timeStyle

Corresponds to the time format, not including (year, month, day). The available values are `full`, `long`, `medium`, `short`.

```handlebars
{{#date startedAt}}{ "timeStyle": "full" }{{/date}}
```

#### calendar

Available values are `buddhist`, `chinese`, `coptic`, `dangi`, `ethioaa`, `ethiopic`, `gregory`, `hebrew`, `islamic`, `indian`, `islamic-umalqura`, `islamic-tbla`, `islamic-civil`, `islamic-rgsa`, `iso8601`, `japanese`, `persian`, `roc`.

```handlebars
{{#date startedAt}}{ "calendar": "chinese" }{{/date}}
```

#### dayPeriod

Available values are `narrow`, `short`, `long`.

```handlebars
{{#date startedAt}}{ "dayPeriod": "long" }{{/date}}
```

#### numberingSystem

Available values are `arab`, `arabext`, `bali`, `beng`, `deva`, `fullwide`, `gujr`, `guru`, `hanidec`, `khmr`, `knda`, `laoo`, `latn`, `limb`, `mlym`, `mong`, `mymr`, `orya`, `tamldec`, `telu`, `thai`, `tibt.`

```handlebars
{{#date startedAt}}{ "numberingSystem": "fullwide" }{{/date}}
```

{% hint style="info" %}
For more information about using <mark style="color:purple;">`@root`</mark> or <mark style="color:purple;">`this`</mark> [click here](../syntax.md#content-of-a-helper).
{% endhint %}