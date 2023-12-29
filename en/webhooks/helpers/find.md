---
description: >-
  Here you'll find the documentation on how to use this helper.
---

# #find

This helper filters values from an array based on comparisons using comparison helpers finding the first value that matches all the comparisons.

{% hint style="info" %}
This helper is meant to be used only with arrays.
{% endhint %}

#### Sample data

```json
{
  "orders": [
    "61b1fbc001e98ee2f8c1f18f",
    "61d389800464df1d4ea02c7b",
    "61d3895e3f52541cf9709398"
  ],
  "cart": [
    {
      "product": "61d38c4b63f59bb2af02cf4d",
      "stock": true,
      "quantity": 2
    },
    {
      "product": "61d38c7a80683ba3dfd05c63",
      "stock": false,
      "quantity": 1
    }
  ]

}
```

## Usage examples

{% hint style="info" %}
We recommend you use `#find` along with other comparison helpers like [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md) and so on.
{% endhint %}

{% code title="Simple array with single condition" %}
```handlebars
{{#find orders}}
    {{#isEqual this}}61b1fbc001e98ee2f8c1f18f{{/isEqual}}
{{/find}}
// Output: "61b1fbc001e98ee2f8c1f18f"
```
{% endcode %}

{% code title="Object find with single condition" %}
```handlebars
{{#find cart}}
    {{#isEqual this.stock}}true{{/isEqual}}
{{/find}}
// Output: { id: "61d38c4b63f59bb2af02cf4d", stock: true, ... }
```
{% endcode %}

{% code title="Object find with multiple conditionals" %}
```handlebars
{{#find cart}}
    {{#greater this.quantity}}1{{/greater}}
    {{#isEqual this.stock}}true{{/isEqual}}
{{/find}}
// Output: { id: "61d38c4b63f59bb2af02cf4d", ... }
```
{% endcode %}

{% hint style="info" %}
Ultimately the output will always be the value of one of the elements of the array.
{% endhint %}

{% hint style="info" %}
For more info about the usage of <mark style="color:purple;">`@root`</mark> and <mark style="color:purple;">`this`</mark> [click here](../syntax.md#helper-contents).
{% endhint %}