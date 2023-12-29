---
description: >-
  Below, you can find the documentation on how to use this helper.
---

# #get

This type of helper is used to get values from an `Object` as the result of using a search helper.

#### Sample data

```json
{
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
We recommend using `#get` together with the [`#find`](find.md) helper.
{% endhint %}

{% code title="Simple array with single conditional" %}
```handlebars
{{#get 'product'}}
    {{#find @root.cart}}
        {{#isEqual this.stock}}true{{/isEqual}}
    {{/find}}
{{/get}}
// Output: 61d38c4b63f59bb2af02cf4d
```
{% endcode %}

{% hint style="info" %}
For more information on the use of <mark style="color:purple;">`@root`</mark> or <mark style="color:purple;">`this`</mark> [click here](../sintaxis.md#contents-of-a-helper).
{% endhint %}