---
description: Properties allow you to access states and general information.
---

# Properties

## `appointmentToken`

This property allows access to the token obtained when loading the URL from the confirmation or reminder email.

[REPLACE_CODE_FORMAT]javascript
calendar.appointmentToken;
// ...
[REPLACE_CODE_FORMAT]

## `date`

This property corresponds to the fallback date used when no date is provided in methods that require it and also for other methods that store states.

[REPLACE_CODE_FORMAT]javascript
calendar.date
// 2023-04-03T17:00:00.000Z
[REPLACE_CODE_FORMAT]

## `type`

It corresponds to the type of scheduling that will be done and will affect the behavior when executing certain methods of the SDK.

The value can be `service` or `user`.

{% hint style="info" %}
Do not overwrite the value through the property, use the [`change`](metodos.md#change) method.
{% endhint %}

[REPLACE_CODE_FORMAT]javascript
calendar.type
// service or user
[REPLACE_CODE_FORMAT]
