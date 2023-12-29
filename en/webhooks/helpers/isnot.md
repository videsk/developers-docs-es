---
description: >-
  The following are the docs of how to use this
  helper.
---

# #isNot

This type of helper is used to make True or False comparisons, based on the entered values.

Typically, you will use `#isNot` together with other helpers.

{% hint style="success" %}
We recommend that you use this helper especially to generate a conditional.
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

### Example usages

```handlebars
{{#isNot number}}99{{/isNot}}
// Output: false

{{#isNot number}}{{/isNot}}
// Output: true

{{#isNot list}}["ABC", "DEF"]{{/isNot}}
// Output: true

{{#isNot named}}{{/isNot}}
// Output: false ("named" doesn't exist in json and the comparison value is not defined)
```