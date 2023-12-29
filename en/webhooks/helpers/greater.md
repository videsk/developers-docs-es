---
description: >-
  Below, you'll find the documentation for how to use this helper.
---

# #greater

This type of helper serves to make true or false comparisons based on entered values.

You'll normally use `#greater` together with other helpers.

{% hint style="success" %}
We recommend using this helper to especially generate a conditional.
{% endhint %}

#### Example Data

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
`#greater` is a type of **exclusive comparison**. Example: `101 is greater than 100`. **Inclusive conditions cannot be created** like `101 is greater than or equal to 100`.
{% endhint %}

```handlebars
{{#greater number}}99{{/greater}}
// Output: false

{{#greater number}}1{{/greater}}
// Output: true
```

{% hint style="info" %}
`#greater` will automatically do parsing of both comparison values as numbers.
{% endhint %}