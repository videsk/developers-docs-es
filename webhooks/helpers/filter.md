---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #filter

Este tipo de helper tiene como utilidad filtrar valores de un `Array`, basado en comparaciones utilizando helpers de comparación.

{% hint style="info" %}
Este helper está diseñado para ser utilizado solamente con `Array.`
{% endhint %}

#### Datos de ejemplo

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

## Ejemplos de uso

{% hint style="info" %}
Te recomendamos utilizar `#filter` en conjunto con otros helpers de comparación como [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#filter fields}}{{#includes name}}Doe{{/includes}}{{/filter}}
// Output: [{ "id": "61d389418a63e556a14d704d", ... }]
```
