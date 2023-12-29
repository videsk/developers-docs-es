---
description: >-
  This following describes how to use this helper.
---

# #filter

This helper filter elements of an `Array` given a set of conditions.

{% hint style="info" %}
This helper is designed to be used with `Array` only.
{% endhint %}

#### Sample data

```json
{
  "users": [
    {
      "id": "61d389418a63e556a14d704d",
      "name": "John Doe",
      "org": "61d389800464df1d4ea02c7b"
    },
    {
      "id": "61d3895e3f52541cf9709398",
      "name": "Maria Doe",
      "org": "61d389800464df1d4ea02c7b"
    }
  ]
}
```

## Usage examples

{% hint style="info" %}
It's strongly recommended to use `#filter` with other comparison helpers, like [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#filter fields}}{{#includes name}}Doe{{/includes}}{{/filter}}
// Output: [{ "id": "61d389418a63e556a14d704d", ... }]
```