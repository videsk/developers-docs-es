---
description: We explain how to use the Calendar through Rest API.
---

# Calendar

With our Rest API calendar, you can easily schedule appointments or meetings for your clients.

The following endpoints are public, that is, `/public/` is prefixed as a means of differentiating from private endpoints.

{% hint style="info" %}
We suggest you check the [flow diagram](../sdks/calendar/#flows) to have an overview of the order of requests to be made before using our API.
{% endhint %}

{% swagger method="get" path="/public/video-contact-center/services" baseUrl="https://api.videsk.io" summary="Get calendar services" expanded="true" %}
{% swagger-description %}
You will be able to obtain the listing of available public services
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of services" %}
{% code lineNumbers="true" %}
```javascript
{
  "total":1,
    "limit":10,
    "skip":0,
    "data":[
    {
      "users":[
        {
          "_id":"63bdbf3230013a2792550a1c",
          "firstname":"John",
          "lastname":"Doe"
        },
        {
          "_id":"63bdbf3b25ab497401602d07",
          "firstname":"Mark",
          "lastname":"Zuckerberg"
        }
      ],
      "title":"My service",
      "description":"Service description",
      "automatic":false,
      "id":"63bdbf49394aad976d4aa43b"
    }
  ]
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/services/:id/dates" baseUrl="https://api.videsk.io" summary="Get available service days of the month by service ID" %}
{% swagger-description %}
Available days of the month based on the service ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
Service ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Month in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Timezone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of days of the month" %}
```javascript
[
  "2023-02-01T03:00:00.000Z",
  "2023-02-02T03:00:00.000Z",
  "2023-02-03T03:00:00.000Z",
  "2023-02-04T03:00:00.000Z",
  "2023-02-05T03:00:00.000Z",
  "2023-02-06T03:00:00.000Z",
  "2023-02-07T03:00:00.000Z",
  "2023-02-08T03:00:00.000Z",
  "2023-02-09T03:00:00.000Z",
  "2023-02-10T03:00:00.000Z",
  "2023-02-11T03:00:00.000Z",
  "2023-02-12T03:00:00.000Z",
  "2023-02-13T03:00:00.000Z",
  "2023-02-14T03:00:00.000Z",
  "2023-02-15T03:00:00.000Z",
  "2023-02-16T03:00:00.000Z",
  "2023-02-17T03:00:00.000Z",
  "2023-02-18T03:00:00.000Z",
  "2023-02-19T03:00:00.000Z",
  "2023-02-20T03:00:00.000Z",
  "2023-02-21T03:00:00.000Z",
  "2023-02-22T03:00:00.000Z",
  "2023-02-23T03:00:00.000Z",
  "2023-02-24T03:00:00.000Z",
  "2023-02-25T03:00:00.000Z",
  "2023-02-26T03:00:00.000Z",
  "2023-02-27T03:00:00.000Z",
  "2023-02-28T03:00:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Date is in the past" %}
```javascript
{
  "name": "BadRequest",
    "message": "The date can not be in the past.",
    "code": 400,
    "className": "bad-request",
    "data": "dateInPast",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"date\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "date",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid timezone" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"timezone\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "timezone",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/services/:id/hours" baseUrl="https://api.videsk.io" summary="Get available service hours of the day by service ID" %}
{% swagger-description %}
Available hours of the day based on the service ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
Service ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Hour in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Timezone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of hours" %}
Dates are in ISO-8601, you can use our [Calendar SDK](../sdks/calendar/) to format dates in local timezone.

```javascript
[
  "2023-02-24T11:00:00.000Z",
  "2023-02-24T11:05:00.000Z",
  "2023-02-24T11:10:00.000Z",
  "2023-02-24T11:15:00.000Z",
  "2023-02-24T11:20:00.000Z",
  "2023-02-24T11:25:00.000Z",
  "2023-02-24T11:30:00.000Z",
  "2023-02-24T11:35:00.000Z",
  "2023-02-24T11:40:00.000Z",
  "2023-02-24T11:45:00.000Z",
  "2023-02-24T11:50:00.000Z",
  "2023-02-24T11:55:00.000Z",
  "2023-02-24T12:00:00.000Z",
  "2023-02-24T12:05:00.000Z",
  "2023-02-24T12:10:00.000Z",
  "2023-02-24T12:15:00.000Z",
  "2023-02-24T12:20:00.000Z",
  "2023-02-24T12:25:00.000Z",
  "2023-02-24T12:30:00.000Z",
  "2023-02-24T12:35:00.000Z",
  "2023-02-24T12:40:00.000Z",
  "2023-02-24T12:45:00.000Z",
  "2023-02-24T12:50:00.000Z",
  "2023-02-24T12:55:00.000Z",
  "2023-02-24T16:00:00.000Z",
  "2023-02-24T16:05:00.000Z",
  "2023-02-24T16:10:00.000Z",
  "2023-02-24T16:15:00.000Z",
  "2023-02-24T16:20:00.000Z",
  "2023-02-24T16:25:00.000Z",
  "2023-02-24T16:30:00.000Z",
  "2023-02-24T16:35:00.000Z",
  "2023-02-24T16:40:00.000Z",
  "2023-02-24T16:45:00.000Z",
  "2023-02-24T16:50:00.000Z",
  "2023-02-24T16:55:00.000Z",
  "2023-02-24T17:00:00.000Z",
  "2023-02-24T17:05:00.000Z",
  "2023-02-24T17:10:00.000Z",
  "2023-02-24T17:15:00.000Z",
  "2023-02-24T17:20:00.000Z",
  "2023-02-24T17:25:00.000Z",
  "2023-02-24T17:30:00.000Z",
  "2023-02-24T17:35:00.000Z",
  "2023-02-24T17:40:00.000Z",
  "2023-02-24T17:45:00.000Z",
  "2023-02-24T17:50:00.000Z",
  "2023-02-24T17:55:00.000Z",
  "2023-02-24T18:00:00.000Z",
  "2023-02-24T18:05:00.000Z",
  "2023-02-24T18:10:00.000Z",
  "2023-02-24T18:15:00.000Z",
  "2023-02-24T18:20:00.000Z",
  "2023-02-24T18:25:00.000Z",
  "2023-02-24T18:30:00.000Z",
  "2023-02-24T18:35:00.000Z",
  "2023-02-24T18:40:00.000Z",
  "2023-02-24T18:45:00.000Z",
  "2023-02-24T18:50:00.000Z",
  "2023-02-24T18:55:00.000Z",
  "2023-02-24T19:00:00.000Z",
  "2023-02-24T19:05:00.000Z",
  "2023-02-24T19:10:00.000Z",
  "2023-02-24T19:15:00.000Z",
  "2023-02-24T19:20:00.000Z",
  "2023-02-24T19:25:00.000Z",
  "2023-02-24T19:30:00.000Z",
  "2023-02-24T19:35:00.000Z",
  "2023-02-24T19:40:00.000Z",
  "2023-02-24T19:45:00.000Z",
  "2023-02-24T19:50:00.000Z",
  "2023-02-24T19:55:00.000Z",
  "2023-02-24T20:00:00.000Z",
  "2023-02-24T20:05:00.000Z",
  "2023-02-24T20:10:00.000Z",
  "2023-02-24T20:15:00.000Z",
  "2023-02-24T20:20:00.000Z",
  "2023-02-24T20:25:00.000Z",
  "2023-02-24T20:30:00.000Z",
  "2023-02-24T20:35:00.000Z",
  "2023-02-24T20:40:00.000Z",
  "2023-02-24T20:45:00.000Z",
  "2023-02-24T20:50:00.000Z",
  "2023-02-24T20:55:00.000Z",
  "2023-02-24T21:00:00.000Z",
  "2023-02-24T21:05:00.000Z",
  "2023-02-24T21:10:00.000Z",
  "2023-02-24T21:15:00.000Z",
  "2023-02-24T21:20:00.000Z",
  "2023-02-24T21:25:00.000Z",
  "2023-02-24T21:30:00.000Z",
  "2023-02-24T21:35:00.000Z",
  "2023-02-24T21:40:00.000Z",
  "2023-02-24T21:45:00.000Z",
  "2023-02-24T21:50:00.000Z",
  "2023-02-24T21:55:00.000Z",
  "2023-02-24T22:00:00.000Z",
  "2023-02-24T22:05:00.000Z",
  "2023-02-24T22:10:00.000Z",
  "2023-02-24T22:15:00.000Z",
  "2023-02-24T22:20:00.000Z",
  "2023-02-24T22:25:00.000Z",
  "2023-02-24T22:30:00.000Z",
  "2023-02-24T22:35:00.000Z",
  "2023-02-24T22:40:00.000Z",
  "2023-02-24T22:45:00.000Z",
  "2023-02-24T22:50:00.000Z",
  "2023-02-24T22:55:00.000Z",
  "2023-02-24T23:00:00.000Z",
  "2023-02-24T23:05:00.000Z",
  "2023-02-24T23:10:00.000Z",
  "2023-02-24T23:15:00.000Z",
  "2023-02-24T23:20:00.000Z",
  "2023-02-24T23:25:00.000Z",
  "2023-02-24T23:30:00.000Z",
  "2023-02-24T23:35:00.000Z",
  "2023-02-24T23:40:00.000Z",
  "2023-02-24T23:45:00.000Z",
  "2023-02-24T23:50:00.000Z",
  "2023-02-24T23:55:00.000Z",
  "2023-02-25T00:00:00.000Z",
  "2023-02-25T00:05:00.000Z",
  "2023-02-25T00:10:00.000Z",
  "2023-02-25T00:15:00.000Z",
  "2023-02-25T00:20:00.000Z",
  "2023-02-25T00:25:00.000Z",
  "2023-02-25T00:30:00.000Z",
  "2023-02-25T00:35:00.000Z",
  "2023-02-25T00:40:00.000Z",
  "2023-02-25T00:45:00.000Z",
  "2023-02-25T00:50:00.000Z",
  "2023-02-25T00:55:00.000Z",
  "2023-02-25T01:00:00.000Z",
  "2023-02-25T01:05:00.000Z",
  "2023-02-25T01:10:00.000Z",
  "2023-02-25T01:15:00.000Z",
  "2023-02-25T01:20:00.000Z",
  "2023-02-25T01:25:00.000Z",
  "2023-02-25T01:30:00.000Z",
  "2023-02-25T01:35:00.000Z",
  "2023-02-25T01:40:00.000Z",
  "2023-02-25T01:45:00.000Z",
  "2023-02-25T01:50:00.000Z",
  "2023-02-25T01:55:00.000Z",
  "2023-02-25T02:00:00.000Z",
  "2023-02-25T02:05:00.000Z",
  "2023-02-25T02:10:00.000Z",
  "2023-02-25T02:15:00.000Z",
  "2023-02-25T02:20:00.000Z",
  "2023-02-25T02:25:00.000Z",
  "2023-02-25T02:30:00.000Z",
  "2023-02-25T02:35:00.000Z",
  "2023-02-25T02:40:00.000Z",
  "2023-02-25T02:45:00.000Z",
  "2023-02-25T02:50:00.000Z",
  "2023-02-25T02:55:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Date is in the past" %}
```javascript
{
  "name": "BadRequest",
    "message": "The date can not be in the past.",
    "code": 400,
    "className": "bad-request",
    "data": "dateInPast",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"date\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "date",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid timezone" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"timezone\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "timezone",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/users/:id/dates" baseUrl="https://api.videsk.io" summary="Get available days of the month by user ID" %}
{% swagger-description %}
Available days of the month based on the user ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
User ID
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Month in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Timezone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of days of the month" %}
Dates are in ISO-8601, you can use our [Calendar SDK](../sdks/calendar/) to format dates in local timezone.

```javascript
[
  "2023-02-01T03:00:00.000Z",
  "2023-02-02T03:00:00.000Z",
  "2023-02-03T03:00:00.000Z",
  "2023-02-04T03:00:00.000Z",
  "2023-02-05T03:00:00.000Z",
  "2023-02-06T03:00:00.000Z",
  "2023-02-07T03:00:00.000Z",
  "2023-02-08T03:00:00.000Z",
  "2023-02-09T03:00:00.000Z",
  "2023-02-10T03:00:00.000Z",
  "2023-02-11T03:00:00.000Z",
  "2023-02-12T03:00:00.000Z",
  "2023-02-13T03:00:00.000Z",
  "2023-02-14T03:00:00.000Z",
  "2023-02-15T03:00:00.000Z",
  "2023-02-16T03:00:00.000Z",
  "2023-02-17T03:00:00.000Z",
  "2023-02-18T03:00:00.000Z",
  "2023-02-19T03:00:00.000Z",
  "2023-02-20T03:00:00.000Z",
  "2023-02-21T03:00:00.000Z",
  "2023-02-22T03:00:00.000Z",
  "2023-02-23T03:00:00.000Z",
  "2023-02-24T03:00:00.000Z",
  "2023-02-25T03:00:00.000Z",
  "2023-02-26T03:00:00.000Z",
  "2023-02-27T03:00:00.000Z",
  "2023-02-28T03:00:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Date is in the past" %}
```javascript
{
  "name": "BadRequest",
    "message": "The date can not be in the past.",
    "code": 400,
    "className": "bad-request",
    "data": "dateInPast",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"date\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "date",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid time zone" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"timezone\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "timezone",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/users/:id/hours" baseUrl="https://api.videsk.io" summary="Get available hours of the day by user id" %}
{% swagger-description %}
Available hours of the day based on the user ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
User ID
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="String" required="true" %}
Time in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Time zone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of hours" %}
Dates are in ISO-8601, you can use our [Calendar SDK](../sdks/calendar/) to format dates in local time zone.

```javascript
[
  "2023-02-24T11:00:00.000Z",
  "2023-02-24T11:05:00.000Z",
  "2023-02-24T11:10:00.000Z",
  "2023-02-24T11:15:00.000Z",
  "2023-02-24T11:20:00.000Z",
  "2023-02-24T11:25:00.000Z",
  "2023-02-24T11:30:00.000Z",
  "2023-02-24T11:35:00.000Z",
  "2023-02-24T11:40:00.000Z",
  "2023-02-24T11:45:00.000Z",
  "2023-02-24T11:50:00.000Z",
  "2023-02-24T11:55:00.000Z",
  "2023-02-24T12:00:00.000Z",
  "2023-02-24T12:05:00.000Z",
  "2023-02-24T12:10:00.000Z",
  "2023-02-24T12:15:00.000Z",
  "2023-02-24T12:20:00.000Z",
  "2023-02-24T12:25:00.000Z",
  "2023-02-24T12:30:00.000Z",
  "2023-02-24T12:35:00.000Z",
  "2023-02-24T12:40:00.000Z",
  "2023-02-24T12:45:00.000Z",
  "2023-02-24T12:50:00.000Z",
  "2023-02-24T12:55:00.000Z",
  "2023-02-24T16:00:00.000Z",
  "2023-02-24T16:05:00.000Z",
  "2023-02-24T16:10:00.000Z",
  "2023-02-24T16:15:00.000Z",
  "2023-02-24T16:20:00.000Z",
  "2023-02-24T16:25:00.000Z",
  "2023-02-24T16:30:00.000Z",
  "2023-02-24T16:35:00.000Z",
  "2023-02-24T16:40:00.000Z",
  "2023-02-24T16:45:00.000Z",
  "2023-02-24T16:50:00.000Z",
  "2023-02-24T16:55:00.000Z",
  "2023-02-24T17:00:00.000Z",
  "2023-02-24T17:05:00.000Z",
  "2023-02-24T17:10:00.000Z",
  "2023-02-24T17:15:00.000Z",
  "2023-02-24T17:20:00.000Z",
  "2023-02-24T17:25:00.000Z",
  "2023-02-24T17:30:00.000Z",
  "2023-02-24T17:35:00.000Z",
  "2023-02-24T17:40:00.000Z",
  "2023-02-24T17:45:00.000Z",
  "2023-02-24T17:50:00.000Z",
  "2023-02-24T17:55:00.000Z",
  "2023-02-24T18:00:00.000Z",
  "2023-02-24T18:05:00.000Z",
  "2023-02-24T18:10:00.000Z",
  "2023-02-24T18:15:00.000Z",
  "2023-02-24T18:20:00.000Z",
  "2023-02-24T18:25:00.000Z",
  "2023-02-24T18:30:00.000Z",
  "2023-02-24T18:35:00.000Z",
  "2023-02-24T18:40:00.000Z",
  "2023-02-24T18:45:00.000Z",
  "2023-02-24T18:50:00.000Z",
  "2023-02-24T18:55:00.000Z",
  "2023-02-24T19:00:00.000Z",
  "2023-02-24T19:05:00.000Z",
  "2023-02-24T19:10:00.000Z",
  "2023-02-24T19:15:00.000Z",
  "2023-02-24T19:20:00.000Z",
  "2023-02-24T19:25:00.000Z",
  "2023-02-24T19:30:00.000Z",
  "2023-02-24T19:35:00.000Z",
  "2023-02-24T19:40:00.000Z",
  "2023-02-24T19:45:00.000Z",
  "2023-02-24T19:50:00.000Z",
  "2023-02-24T19:55:00.000Z",
  "2023-02-24T20:00:00.000Z",
  "2023-02-24T20:05:00.000Z",
  "2023-02-24T20:10:00.000Z",
  "2023-02-24T20:15:00.000Z",
  "2023-02-24T20:20:00.000Z",
  "2023-02-24T20:25:00.000Z",
  "2023-02-24T20:30:00.000Z",
  "2023-02-24T20:35:00.000Z",
  "2023-02-24T20:40:00.000Z",
  "2023-02-24T20:45:00.000Z",
  "2023-02-24T20:50:00.000Z",
  "2023-02-24T20:55:00.000Z",
  "2023-02-24T21:00:00.000Z",
  "2023-02-24T21:05:00.000Z",
  "2023-02-24T21:10:00.000Z",
  "2023-02-24T21:15:00.000Z",
  "2023-02-24T21:20:00.000Z",
  "2023-02-24T21:25:00.000Z",
  "2023-02-24T21:30:00.000Z",
  "2023-02-24T21:35:00.000Z",
  "2023-02-24T21:40:00.000Z",
  "2023-02-24T21:45:00.000Z",
  "2023-02-24T21:50:00.000Z",
  "2023-02-24T21:55:00.000Z",
  "2023-02-24T22:00:00.000Z",
  "2023-02-24T22:05:00.000Z",
  "2023-02-24T22:10:00.000Z",
  "2023-02-24T22:15:00.000Z",
  "2023-02-24T22:20:00.000Z",
  "2023-02-24T22:25:00.000Z",
  "2023-02-24T22:30:00.000Z",
  "2023-02-24T22:35:00.000Z",
  "2023-02-24T22:40:00.000Z",
  "2023-02-24T22:45:00.000Z",
  "2023-02-24T22:50:00.000Z",
  "2023-02-24T22:55:00.000Z",
  "2023-02-24T23:00:00.000Z",
  "2023-02-24T23:05:00.000Z",
  "2023-02-24T23:10:00.000Z",
  "2023-02-24T23:15:00.000Z",
  "2023-02-24T23:20:00.000Z",
  "2023-02-24T23:25:00.000Z",
  "2023-02-24T23:30:00.000Z",
  "2023-02-24T23:35:00.000Z",
  "2023-02-24T23:40:00.000Z",
  "2023-02-24T23:45:00.000Z",
  "2023-02-24T23:50:00.000Z",
  "2023-02-24T23:55:00.000Z",
  "2023-02-25T00:00:00.000Z",
  "2023-02-25T00:05:00.000Z",
  "2023-02-25T00:10:00.000Z",
  "2023-02-25T00:15:00.000Z",
  "2023-02-25T00:20:00.000Z",
  "2023-02-25T00:25:00.000Z",
  "2023-02-25T00:30:00.000Z",
  "2023-02-25T00:35:00.000Z",
  "2023-02-25T00:40:00.000Z",
  "2023-02-25T00:45:00.000Z",
  "2023-02-25T00:50:00.000Z",
  "2023-02-25T00:55:00.000Z",
  "2023-02-25T01:00:00.000Z",
  "2023-02-25T01:05:00.000Z",
  "2023-02-25T01:10:00.000Z",
  "2023-02-25T01:15:00.000Z",
  "2023-02-25T01:20:00.000Z",
  "2023-02-25T01:25:00.000Z",
  "2023-02-25T01:30:00.000Z",
  "2023-02-25T01:35:00.000Z",
  "2023-02-25T01:40:00.000Z",
  "2023-02-25T01:45:00.000Z",
  "2023-02-25T01:50:00.000Z",
  "2023-02-25T01:55:00.000Z",
  "2023-02-25T02:00:00.000Z",
  "2023-02-25T02:05:00.000Z",
  "2023-02-25T02:10:00.000Z",
  "2023-02-25T02:15:00.000Z",
  "2023-02-25T02:20:00.000Z",
  "2023-02-25T02:25:00.000Z",
  "2023-02-25T02:30:00.000Z",
  "2023-02-25T02:35:00.000Z",
  "2023-02-25T02:40:00.000Z",
  "2023-02-25T02:45:00.000Z",
  "2023-02-25T02:50:00.000Z",
  "2023-02-25T02:55:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Date is in the past" %}
```javascript
{
  "name": "BadRequest",
    "message": "The date can not be in the past.",
    "code": 400,
    "className": "bad-request",
    "data": "dateInPast",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"date\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "date",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid time zone" %}
```javascript
{
  "name": "BadRequest",
    "message": "A valid \"timezone\" is required",
    "code": 400,
    "className": "bad-request",
    "data": "timezone",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/service/:id" baseUrl="https://api.videsk.io" summary="Schedule a time for service" %}
{% swagger-description %}
Schedule a time using a service with automatic agent selection
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
Service ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startAt" type="Date" required="true" %}
Date in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timezone" type="String" required="true" %}
Time zone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="body" name="form" type="Array" required="true" %}
Form fields
{% endswagger-parameter %}

{% swagger-parameter in="body" name="referrer" type="String" required="true" %}
Referred campaign or website
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Scheduled time" %}
```javascript
{
  "email":"john.doe@example.com",
    "service":"Service name",
    "startAt":"2023-02-01T03:00:00.000Z",
    "endAt":"2023-02-01T03:07:00.000Z",
    "duration":7,
    "timezone":"America/Santiago",
    "joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "message":"Your appointment was successfully scheduled."
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid \"date\" is required",
"code": 400,
"className": "bad-request",
"data": "date",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid timezone" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid \"timezone\" is required",
"code": 400,
"className": "bad-request",
"data": "timezone",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error in form fields" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "You reach the max characters is 50 for element \"60dbe3416af0be33b8b372b1\".",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]

[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "Some element not as field, please check or try again",
"code": 400,
"className": "bad-request",
"data": "Maybe the organization has changed the form and you're submit is not valid anymore.",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](autorizacion.md).
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Time unavailable" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "Conflict",
"message": "Sorry, the hour \"2023-02-07T03:56:00.000Z\" is unavailable.",
"code": 409,
"className": "conflict",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/user/:id" baseUrl="https://api.videsk.io" summary="Schedule a time with an agent" %}
{% swagger-description %}
Schedule a time through an agent
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
User ID
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="service" type="String" required="true" %}
Service ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startAt" type="Date" required="true" %}
Date in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timezone" type="String" required="true" %}
Time zone in ISO-8601 format
{% endswagger-parameter %}

{% swagger-parameter in="body" name="form" type="Array" required="true" %}
Form fields
{% endswagger-parameter %}

{% swagger-parameter in="body" name="referrer" type="String" required="true" %}
Campaign or web referral
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Time scheduled" %}
[REPLACE_CODE_FORMAT]javascript
{
"email":"john.doe@example.com",
"service":"Service name",
"startAt":"2023-02-01T03:00:00.000Z",
"endAt":"2023-02-01T03:07:00.000Z",
"duration":5,
"timezone":"America/Santiago",
"joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"message":"Your appointment was successfully scheduled."
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid service ID" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid service id is required",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid \"date\" is required",
"code": 400,
"className": "bad-request",
"data": "date",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid timezone" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid \"timezone\" is required",
"code": 400,
"className": "bad-request",
"data": "timezone",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error in form fields" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "You reach the max characters is 50 for element \"60dbe3416af0be33b8b372b1\".",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]

[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "Some element not as field, please check or try again",
"code": 400,
"className": "bad-request",
"data": "Maybe the organization has changed the form and you're submit is not valid anymore.",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in [authorization](autorizacion.md).
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Time unavailable" %}
```javascript
{
  "name": "Conflict",
    "message": "Sorry, the hour \"2023-02-07T04:24:00.000Z\" is unavailable.",
    "code": 409,
    "className": "conflict",
    "errors": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/cancel" baseUrl="https://api.videsk.io" summary="Cancel a time" %}
{% swagger-description %}
Cancel a time using `actionToken`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {actionToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancelReason" type="String" %}
Cancellation reason
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Appointment canceled" %}
[REPLACE_CODE_FORMAT]javascript
{
"service": "Service name",
"message": "The appointment was successfully canceled"
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid cancellation reason" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "Cast to string failed for value \"[]\" (type Array) at path \"cancelReason\"",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]

[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "Validation failed: cancelReason: Path `cancelReason` (`...`) is longer than the maximum allowed length (1000).",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Cancellation error" %}
This error indicates that the appointment has already been canceled previously, it is not possible to cancel after the start time or it has already ended.

[REPLACE_CODE_FORMAT]javascript
{
"name": "NotAuthenticated",
"message": "The token is not valid any more.",
"code": 401,
"className": "not-authenticated",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid action token" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/reschedule" baseUrl="https://api.videsk.io" summary="Reschedule an appointment" %}
{% swagger-description %}
Reschedule an appointment using `actionToken`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {actionToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="date" type="Date" required="true" %}
Date in ISO-8601 format
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Appointment rescheduled" %}
[REPLACE_CODE_FORMAT]javascript
{
"email":"john.doe@example.com",
"service":"Service name",
"startAt":"2023-02-01T03:00:00.000Z",
"endAt":"2023-02-01T03:07:00.000Z",
"duration":5,
"timezone":"America/Santiago",
"joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9l
"cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
"message":"Your appointment was successfully scheduled."
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid date" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "BadRequest",
"message": "A valid \"date\" is required",
"code": 400,
"className": "bad-request",
"data": "date",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Rescheduling error" %}
This error indicates that the appointment has already been rescheduled previously, it is not possible to reschedule after the start time or it has already ended.

[REPLACE_CODE_FORMAT]javascript
{
"name": "NotAuthenticated",
"message": "The token is not valid any more.",
"code": 401,
"className": "not-authenticated",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid action token" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/schedule/info" baseUrl="https://api.videsk.io" summary="Get information about an appointment" %}
{% swagger-description %}
Get information about an appointment such as the agent, service, start date, end date, and status.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Appointment information" %}
[REPLACE_CODE_FORMAT]javascript
{
"id":"63be2378f0dd1fdbf86dac48",
"service":{
"id":"620fedcc8951823b744f3122",
"title":"Service name",
"description":"Service description"
},
"user":{
"firstname":"Mark",
"lastname":"Zuckerberg",
"_id":"6179480f5aa331375394e6a9"
},
"startAt":"2023-02-07T05:13:00.000Z",
"endAt":"2023-02-07T05:20:00.000Z",
"status":"pending"
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Expired appointment" %}
This error is thrown when attempting to get information about an appointment that has already been canceled, rescheduled, or has ended.

[REPLACE_CODE_FORMAT]javascript
{
"name": "NotAuthenticated",
"message": "The token is not valid any more.",
"code": 401,
"className": "not-authenticated",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid action token" %}
Error reference in [authorization](authorization.md).
{% endswagger-response %}
{% endswagger %}
