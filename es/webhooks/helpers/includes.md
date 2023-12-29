---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #includes

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores ingresados.

Habitualmente `#includes` lo utilizarás en conjunto con otros helpers.

{% hint style="success" %}
Te recomendamos utilizar este helper especialmente para generar un condicional.
{% endhint %}

#### Datos de ejemplo

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

### Ejemplos de uso

```handlebars
{{#includes list}}ABC{{/includes}}
// Output: true

{{#includes list}}{ "name": "ABC" }{{/includes}}
// Output: false
```
