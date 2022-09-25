---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #get

Este tipo de helper tiene como utilidad obtener valores de un `Object` como resultado del uso de un helper de búsqueda.

#### Datos de ejemplo

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

## Ejemplos de uso

{% hint style="info" %}
Te recomendamos utilizar `#get` en conjunto con el helper [`#find`](find.md).
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
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
