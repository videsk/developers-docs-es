---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #find

Este tipo de helper tiene como utilidad filtrar valores de un `Array`, basado en comparaciones utilizando helpers de comparación y obtener un valor único que coincida con las comparaciones realizadas.

{% hint style="info" %}
Este helper está diseñado para ser utilizado solamente con `Array.`
{% endhint %}

#### Datos de ejemplo

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

## Ejemplos de uso

{% hint style="info" %}
Te recomendamos utilizar `#find` en conjunto con otros helpers de comparación como [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

{% code title="Simple array with single conditional" %}
```handlebars
{{#find orders}}
  {{#isEqual this}}61b1fbc001e98ee2f8c1f18f{{/isEqual}}
{{/find}}
// Output: "61b1fbc001e98ee2f8c1f18f"
```
{% endcode %}

{% code title="Object find with single conditionals" %}
```handlebars
{{#find cart}}
  {{#isEqual this.stock}}true{{/isEqual}}
{{/find}}
// Output: { id: "61d38c4b63f59bb2af02cf4d", status: true, ... }
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
El resultado final siempre será el valor de uno de los elementos del `Array`.
{% endhint %}

{% hint style="info" %}
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
