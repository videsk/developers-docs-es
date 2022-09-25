---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #isEqual

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores ingresados.

Habitualmente `#isEqual` lo utilizarás en conjunto con otros helpers.

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
{{#isEqual number}}99{{/isEqual}}
// Output: true

{{#isEqual number}}{{/isEqual}}
// Output: false
        
{{#isEqual list}}["ABC", "DEF"]{{/isEqual}}
// Output: false

{{#isEqual named}}{{/isEqual}}
// Output: true ("named" no existe en json y el valor de comparación no está definido)
```
