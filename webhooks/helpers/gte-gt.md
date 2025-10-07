---
description: >-
  A continuación, podrás encontrar la documentación de cómo utilizar este
  helper.
---

# #gte/gt

Este tipo de helper tiene como utilidad realizar una comparación de tipo verdadero o falso, basada en los valores ingresados.

Habitualmente `#gte` o `#gt` los utilizarás en conjunto con otros helpers.

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
{{#gte UMBRAL}}VALOR{{/lte}}
```

Donde:

* `UMBRAL`: El número contra el cual comparar
* `VALOR`: El valor que proviene de los datos

En cualquier caso, puedes introducir números variables (desde los datos) o fijos de esta manera puedes comparar un valor dinámico con uno fijo.

### Ejemplos de uso

{% hint style="info" %}
`#gte` y `#gt` automáticamente hará `parsing` a ambos valores de comparación como números.
{% endhint %}

## `#gte`

```handlebars
{{#gte number}}99{{/gte}}
{{! Output: true }}

{{#gte number}}1{{/gte}}
{{! Output: false }}

{{#gte 99}}{{@root.number}}{{/gte}}
{{! Output: true }}
```

## `#gt`

```handlebars
{{#gt number}}99{{/gt}}
{{! Output: false }}

{{#gt number}}1{{/gt}}
/{{! Output: false }}

{{#gt 99}}{{@root.number}}{{/gt}}
{{! Output: false }}
```

{% hint style="warning" %}
El helper `#greater` sigue disponible como retrocompatibilidad, prefiera utilizar `#gt`.&#x20;
{% endhint %}
