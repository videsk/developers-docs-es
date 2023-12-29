---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #lower

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores ingresados.

Habitualmente `#lower` lo utilizarás en conjunto con otros helpers.

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

{% hint style="warning" %}
`#lower` es un tipo de **comparación excluyente**. Ejemplo: `100 es menor a 101` . **No es posible condicionar de forma incluyente** `100 es menor o igual a 101`.
{% endhint %}

```handlebars
{{#lower number}}100{{/greater}}
// Output: true

{{#lower number}}1{{/greater}}
// Output: false
```

{% hint style="info" %}
`#lower` automáticamente hará `parsing` a ambos valores de comparación como números.
{% endhint %}
