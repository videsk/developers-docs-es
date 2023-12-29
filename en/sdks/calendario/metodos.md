---
description: These are the available methods for using our calendar through SDK.
---

# Methods

The following methods allow you to access functions that will change behavior or helpers for certain actions.

{% hint style="warning" %}
All dates you are going to use must be in UTC time and ISO-8601 format. That is, `2023-04-03T17:00:00.000Z`.
{% endhint %}

## `getServices`

With this method, you can obtain the list of services associated with your account.

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

{% tabs %}
{% tab title="Code" %}
```javascript
const services = await calendar.getServices();
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "total": 1,
    "limit": 10,
    "skip": 0,
    "data": [
        {
            "automatic": true,
            "title": "Demo Meeting",
            "description": "Demo Meeting",
            "id": "61202d32a13b4cf9004eaab1"
        }
    ],
    "cached": true
}
```
{% endtab %}
{% endtabs %}

## `change`

With this method, you can change the entity with which you will search for dates by month and day, in addition to defining if scheduling is done with a general service or a specific user. The accepted values are:

* `service` (default)
* `user`

```javascript
calendar
  .change('user')
  .getDays('639a438084d5a0b0690d5cb5');
```

## `getDays`

With this method, you can obtain the list of available days based on the ID of a service and a specific month.

1. `serviceId`: Corresponds to the service ID
2. `ISODate`: Corresponds to the month in ISO-8601 format in UTC time, by default today.
3. `timezone`: Corresponds to the user's time zone (optional)

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

{% tabs %}
{% tab title="Code" %}
```javascript
const days = await calendar.getDays(serviceId);
```
{% endtab %}

{% tab title="Response" %}
The value returned by this method corresponds to a list of dates as objects, each of the keys provides the date in different formats and **in the user's language**:

1. `date`: Weekday + day of the month + abbreviated month
2. `weekday`: Weekday
3. `day`: Day of the month
4. `month`: Month of the year
5. `utc`: Date in UTC and ISO-8601 format



```javascript
[
    {
        "date": "Mon, 03 Apr",
        "weekday": "Mon",
        "day": "3",
        "month": "April",
        "utc": "2023-04-03T04:00:00.000Z"
    },
    {
        "date": "Tue, 04 Apr",
        "weekday": "Tue",
        "day": "4",
        "month": "April",
        "utc": "2023-04-04T04:00:00.000Z"
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The list of days is in UTC ISO-8601 format, use this date to obtain the available hours.
{% endhint %}

## `getHours`

With this method, you can obtain the list of available hours based on the ID of a service and a specific day.

1. `serviceId`: Corresponds to the service ID
2. `ISODate`: Corresponds to the month in ISO-8601 format in UTC time, by default today.
3. `timezone`: Corresponds to the user's time zone (optional)

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

{% tabs %}
{% tab title="Code" %}
```javascript
const hours = await calendar.getHours(serviceId, ISODate);
```
{% endtab %}

{% tab title "Response" %}
The value returned by this method corresponds to a list of dates as objects, each of the keys provides the date in different formats and **in the user's language**:

1. `date`: Weekday + day of the month + abbreviated month
2. `weekday`: Weekday
3. `day`: Day of the month
4. `time`: Time in `HH:mm` format
5. `hour`: Hour in `HH` format
6. `minutes`: Minutes in `mm` format
7. `utc`: Date in UTC and ISO-8601 format



```javascript
[
    {
        "date": "Mon, 03 Apr",
       

 "weekday": "Mon",
        "time": "08:00",
        "day": "3",
        "hour": "08",
        "minutes": "0",
        "utc": "2023-04-03T12:00:00.000Z"
    },
    {
        "date": "Mon, 03 Apr",
        "weekday": "Mon",
        "time": "08:15",
        "day": "3",
        "hour": "08",
        "minutes": "15",
        "utc": "2023-04-03T12:15:00.000Z"
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The list of hours is in UTC ISO-8601 format, use this date to schedule.
{% endhint %}

## `create`

With this method, you can create an appointment by providing 2 mandatory arguments.

1. `entityId`: ID of the service or agent
2. `data`: Scheduling data as `Object` being:

{% tabs %}
{% tab title="For service" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>    startAt: "2023-04-03T12:00:00.000Z",
    timezone: "America/Santiago",
    form: [{...}],
    referrer: 'https://schedule.example.com',
    token: '0.AOpYir-gaFDC4NreNyXVyXTRPhJREe3dv33S9hdQ0H3lsJkOM'
}
</code></pre>
{% endtab %}

{% tab title="For user" %}
{% hint style="warning" %}
The `service` key is only required when scheduling for a user.
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
To obtain the form, you should use the [Form SDK](../forms.md).
{% endhint %}

So, you should:

```javascript
await calendar.create('639a490f4362d0a814b5c7fd', data);
```

In case of failure, you should listen to the `error` event, where you can obtain the reason for the error.

## `cancel`

With this method, you can cancel an appointment. This method requires the use of a token, which is automatically detected in the URL by default.

The parameters present in the URL are:

1. `v-schedule-action`: corresponds to the action to be performed
2. `v-schedule-auth`: corresponds to the authorization token sent by email

{% hint style="info" %}
You should use this method when the `modify` event is triggered.
{% endhint %}

```javascript
await calendar.cancel();
```

## `reschedule`

With this method, you can reschedule a previously scheduled appointment. It receives one mandatory argument `data` which corresponds to an `Object`.

{% hint style="info" %}
You should use this method when the `modify` event is triggered.
{% endhint %}

```javascript
const data = { date: "2023-04-03T12:00:00.000Z" };
await calendar.reschedule(data);
```

## `getInfo`

With this method, you can get the information of the appointment **only 5 minutes before** the scheduled time.

```javascript
await calendar.getInfo();
```

## `connect`

This method allows you to generate the necessary connection to join the video call. It requires the use of the access token sent in the confirmation or reminder email.

{% hint style="info" %}
To access the token, you can use `calendar.appointmentToken`.
{% endhint %}

{% hint style="danger" %}
You should only execute the `connect` method if the `v-schedule-action` and `v-schedule-auth` parameters are not present in the URL.
{% endhint %}

```javascript
await calendar.connect();
```

## `join`

With this method, you can join the video call.

{% hint style="danger" %}
You should execute this method only 5 minutes before the start time and up to 30 minutes after the end time.
{% endhint %}

```javascript
calendar.join();
```

## `addEventListener`

With this method, you can add event listeners with a callback. The first argument corresponds to the name of the event and the second to the callback that returns a single argument as an event.

This event corresponds to a `CustomEvent` where the relevant information is in the key `detail`.

```javascript
calendar.addEventListener('join', (event) => {
    const { ... } = event.detail;
});
```

## `calendarLink`

With this method, you can generate links for the most popular calendar services so your users can add the appointment with a click.

```javascript
const link = calendar.calendarLink('google', payload);
```

{% hint style="info" %}
To open the link in a new tab, you can use <mark style="color:green;background-color:purple;">`window.open(link, "_blank")`</mark>.
{% endhint %}

The method takes two arguments:

* `type`: name of the service, can be `google`, `outlook`, `office365`, `yahoo`, or `ics`.
* `payload`: format for generating the link

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
    "title": "Meeting of {duration} min with {service}",
    "description": "...",
    "start": "2023-02-02T19:10:00.000Z",
    "end": "2023-02-02T19:15:00.000Z",
    "duration": [15, "minutes"],
    "url": "https://videsk.io/?=&v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "busy": true,
    "location": "https://videsk.io/?=&v-schedule-action=join

&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "guests": ["john.doe@gmail.com"]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The mentioned values are obtained in the response after using the [`create`](metodos.md#create) or [`reschedule`](metodos.md#reschedule) method.
{% endhint %}

#### `title`

Default value used in the title by injecting variables.

```handlebars
Meeting of {duration} min with {service}
```

#### `description`

Default value used in the description by injecting variables.

```handlebars
You can access the meeting through this link:\n\n{joinURL}. \n\n------------\n\nYou can also cancel the meeting from this link:\n\n{cancelURL}. \n\n------------\n\nOr reschedule from this link:\n\n{rescheduleURL}.
```

#### `start`

Corresponds to the start date given as UTC called `startAt`.

#### `end`

Corresponds to the end date given as UTC called `endAt`.

#### `duration`

Corresponds to an array with two indices, the first is the duration obtained from the response as `duration` and the second the time unit, which should by default be `minutes`, as `duration` is in minutes.

#### `url`

Corresponds to the access link to the meeting. You get this value from the response as `joinUrl`.

#### `busy`

Corresponds to the user's status when the meeting starts in their calendar. It is suggested to use `true`.

#### `location`

Corresponds to the location of the meeting, which in this case is used to fill in with the access link. Some calendar clients detect this field as a video call link. Obtain this value from the response as `joinUrl`.

#### `guests`

Corresponds to the list `Array` of guests to the meeting. You can get the value from the response as `email`.