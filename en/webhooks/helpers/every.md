---
description: >-
  The following is the documentation on how to use this helper.
---

# #every

This type of helper is used to make true or false comparisons based on `Array` values.

{% hint style="info" %}
This helper is designed to be used only with `Array.`
{% endhint %}

You will usually use `#every` together with other helpers.

{% hint style="success" %}
We recommend that you use this helper especially to generate a conditional.
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

## Usage examples

{% hint style="info" %}
We recommend that you use `#every` together with other comparison helpers like [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#every fields}}{{properties.required}}{{/every}}
// Output: true

{{#every fields}}{{#isEqual properties.minlength}}5{{/isEqual}}{{/every}}
// Output: true
```