---
description: >-
  The following information will guide you on how to use this
  helper.
---

# #isEqual

This type of helper has the utility of making a comparison of the `true` or `false` type, based on the entered values.

Usually, you use `#isEqual` with other helpers.

{% hint style="success" %}
We recommend that you use this helper especially to generate a conditional.
{% endhint %}

#### Sample Data

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
{{#isEqual number}}99{{/isEqual}}
// Output: true

{{#isEqual number}}{{/isEqual}}
// Output: false

{{#isEqual list}}["ABC", "DEF"]{{/isEqual}}
// Output: false

{{#isEqual named}}{{/isEqual}}
// Output: true ("named" does not exist in json and the comparison value is not defined)
```