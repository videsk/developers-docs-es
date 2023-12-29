---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #greater

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores ingresados.

Habitualmente `#greater` lo utilizarás en conjunto con otros helpers.

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
`#greater` es un tipo de **comparación excluyente**. Ejemplo: `101 es mayor a 100` . **No es posible condicionar de forma incluyente** `101 es mayor o igual a 100`.
{% endhint %}

```handlebars
{{#greater number}}99{{/greater}}
// Output: false

{{#greater number}}1{{/greater}}
// Output: true
```

{% hint style="info" %}
`#greater` automáticamente hará `parsing` a ambos valores de comparación como números.
{% endhint %}
