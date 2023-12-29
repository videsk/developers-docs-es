---
description: >-
  Below, you can find documentation on using this
  helper.
---

# #lower

This helper is used to perform true or false type comparison, based on the values entered.

You will usually use `#lower` together with other helpers.

{% hint style="success" %}
We recommend using this helper especially to generate a conditional.
{% endhint %}

#### Example data

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

{% hint style="warning" %}
`#lower` is a type of **exclusive comparison**. For example: `100 is less than 101`. **It is not possible to condition inclusively** `100 is less than or equal to 101`.
{% endhint %}

```handlebars
{{#lower number}}100{{/greater}}
// Output: true

{{#lower number}}1{{/greater}}
// Output: false
```

{% hint style="info" %}
`#lower` will automatically parse both comparison values as numbers.
{% endhint %}