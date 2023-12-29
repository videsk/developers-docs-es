---
description: >-
  Below you will find the documentation to use this helper.
---

# #some

This kind of helper has the usefulness of making true or false type comparison based on `Array` values.

{% hint style="info" %}
This helper is designed to be used only with `Array`.
{% endhint %}

Usually you will use `#some` together with other helpers.

{% hint style="success" %}
We recommend using this helper especially to generate a conditional.
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

{% hint style="info" %}
We recommend using `#some` together with other comparison helpers such as [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#some list}}{{#includes @root.list}}ABC{{/includes}}{{/some}}
// Output: true

{{#some object}}{{#isEqual name}}ABC{{/isEqual}}{{/some}}
// Output: true
```

{% hint style="info" %}
For more information on the use of <mark style="color:purple;">`@root`</mark> or <mark style="color:purple;">`this`</mark> [click here](../syntax.md#helper-contents).
{% endhint %}