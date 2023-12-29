---
description: >-
  Below, you will find the documentation on how to use this
  helper.
---

# #includes

This type of helper is useful for performing true or false type comparison, based on the values entered.

You will usually use `#includes` in conjunction with other helpers.

{% hint style="success" %}
We recommend using this helper especially to generate a conditional.
{% endhint %}

#### Sample data

```json
{
  "number": 99,
  "name": "John Doe",
  "list": [
    "ABC",
    "DEF"
  ],
  "object": [
    { "name": "ABC" },
    { "name": "DEF" }
  ]
}
```

### Usage examples

```handlebars
{{#includes list}}ABC{{/includes}}
// Output: true

{{#includes list}}{ "name": "ABC" }{{/includes}}
// Output: false
```