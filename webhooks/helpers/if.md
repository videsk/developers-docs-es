---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #if

Este tipo de helper te permite generar una estructura basado en condiciones, esto es útil si la estructura debe variar dependiendo de algún valor de tipo `Boolean`.

#### Datos de ejemplo

```json
{
  "isOnline": true,
  "isAvailable": false,
  "data": [{ "id": "61d3905e6ee6a2321c88f7af" }, ...],
}
```

## Ejemplos de uso

{% hint style="info" %}
Ten en cuenta que el valor a comparar solo puede ser tipo `Boolean`.
{% endhint %}

{% tabs %}
{% tab title="if" %}
#### Sintaxis

```handlebars
{{#if isOnline}}
  {{parser data}}
{{/if}}
```

#### Resultado

```json
[{ "id": "61d3905e6ee6a2321c88f7af" }, ...]
```
{% endtab %}

{% tab title="if/else" %}
#### Sintaxis

```handlebars
{{#if isAvailable}}
  {{parser data}}
{{else}}
 { message: "The user is not available" }
{{/if}}
```

#### Resultado

```json
{ message: "The user is not available" }
```
{% endtab %}
{% endtabs %}

