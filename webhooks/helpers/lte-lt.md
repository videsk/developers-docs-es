---
description: >-
  A continuación, podrás encontrar la documentación de cómo utilizar este
  helper.
---

# #lte/lt

Este tipo de helper tiene como utilidad realizar una comparación de tipo verdadero o falso, basada en los valores ingresados.

Habitualmente `#lte` y `#lt` los utilizarás en conjunto con otros helpers.

{% hint style="success" %}
Te recomendamos utilizar estos helpers especialmente para generar condicionales.
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

## Sintaxis

La sintaxis es:

```handlebars
{{#lte UMBRAL}}VALOR{{/lte}}
```

Donde:

* `UMBRAL`: El número contra el cual comparar
* `VALOR`: El valor que proviene de los datos

En cualquier caso, puedes introducir números variables (desde los datos) o fijos de esta manera puedes comparar un valor dinámico con uno fijo.

#### Ejemplos de uso

{% hint style="info" %}
`#lte` y `#lt` automáticamente hará `parsing` a ambos valores de comparación como números.&#x20;
{% endhint %}

## `#lte`

```handlebars
{{#lte number}}99{{/lte}}
{{! Output: true }}

{{#lte number}}1{{/lte}}
{{! Output: true }}

{{#lte 500}}{{@root.number}}{{/lte}}
{{! Output: true }}
```

## `#lt`&#x20;

```handlebars
{{#lt number}}99{{/lt}}
{{! Output: false }}

{{#lt number}}1{{/lt}}
{{! Output: true }}

{{#lt 500}}{{@root.number}}{{/lt}}
{{! Output: true }}
```

{% hint style="warning" %}
El helper `#lower` sigue disponible como retrocompatibilidad, prefiera utilizar `#lt`.&#x20;
{% endhint %}
