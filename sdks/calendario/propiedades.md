---
description: Las propiedades te permiten acceder a estados e información en general.
---

# Propiedades

## `appointmentToken`

Esta propiedad permite acceder al token que se obtiene al momento de cargar la URL proveniente del email de confirmación o recordatorio.

```javascript
calendar.appointmentToken;
// ...
```

## `date`

Esta propiedad corresponde a la fecha fallback utilizada cuando no se proporciona una fecha en los métodos que lo requieren y también para otros métodos que almacenan estados.

```javascript
calendar.date
// 2023-04-03T17:00:00.000Z
```

## `type`

Corresponde al tipo de agendamiento que se realizará y afectará el comportamiento cuando ejecutes ciertos métodos del SDK.

El valor puede ser `service` o `user`.

{% hint style="info" %}
No sobreescribas el valor mediante la propiedad, utiliza el método [`change`](metodos.md#change).
{% endhint %}

```javascript
calendar.type
// service or user
```
