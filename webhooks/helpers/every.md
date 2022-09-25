---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #every

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores de `Array`.

{% hint style="info" %}
Este helper está diseñado para ser utilizado solamente con `Array.`
{% endhint %}

Habitualmente `#every` lo utilizarás en conjunto con otros helpers.

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

## Ejemplos de uso

{% hint style="info" %}
Te recomendamos utilizar `#every` en conjunto con otros helpers de comparación como [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#every fields}}{{properties.required}}{{/every}}
// Output: true

{{#every fields}}{{#isEqual properties.minlength}}5{{/isEqual}}{{/every}}
// Output: true
```
