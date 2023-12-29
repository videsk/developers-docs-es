---
description: >-
  The following documentation explains how to use this helper.
---

# #concat

This helper's purpose is to concatenate two `Array` into one.

{% hint style="info" %}
This helper is meant to be used only with `Array`.
{% endhint %}

#### Example data

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
  ],
  "customers": [
    {
      "id": "61d38a3a49cfea276739506f",
      "email": "john.doe@business.com",
    },
    {
      "id": "61d38a3e1a257213607919bc",
      "email": "ma.doe@business.com",
    }
  ]
}
```

## Usage examples

{% hint style="warning" %}
You must use this helper with [parser](parser.md), otherwise you'll get an error.
{% endhint %}

```handlebars
{{#concat users}}{{parser @root.customers}}{{/concat}}
// Output: [{ "name": "John Doe", ... }, { "email": "john.doe@business.com", ... }]
```

{% hint style="info" %}
To learn more about the use of <mark style="color:purple;">`@root`</mark> or <mark style="color:purple;">`this`</mark> [click here](../syntax.md#helper-contents).
{% endhint %}