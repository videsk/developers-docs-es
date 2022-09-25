---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #isNot

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores ingresados.

Habitualmente `#isNot` lo utilizarás en conjunto con otros helpers.

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
{{#isNot number}}99{{/isNot}}
// Output: false

{{#isNot number}}{{/isNot}}
// Output: true
        
{{#isNot list}}["ABC", "DEF"]{{/isNot}}
// Output: true

{{#isNot named}}{{/isNot}}
// Output: false ("named" no existe en json y el valor de comparación no está definido)
```
