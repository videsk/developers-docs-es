---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #some

Este tipo de helper tiene como utilidad realizar comparación de tipo verdadero o falso, basado en los valores de `Array`.

{% hint style="info" %}
Este helper está diseñado para ser utilizado solamente con `Array.`
{% endhint %}

Habitualmente `#some` lo utilizarás en conjunto con otros helpers.

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

{% hint style="info" %}
Te recomendamos utilizar `#some` en conjunto con otros helpers de comparación como [`#isEqual`](isequal.md), [`#isNot`](isnot.md), [`#includes`](includes.md), etc.
{% endhint %}

```handlebars
{{#some list}}{{#includes @root.list}}ABC{{/includes}}{{/some}}
// Output: true

{{#some object}}{{#isEqual name}}ABC{{/isEqual}}{{/some}}
// Output: true
```

{% hint style="info" %}
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
