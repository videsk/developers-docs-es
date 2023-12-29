---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #url-param

Este tipo de helper tiene como utilidad obtener el valor de los parámetros de una URL.

#### Datos de ejemplo

```json
{
    "url": "https://website.com?phone=12323848374&email=john@gmail.com"
}
```

## Ejemplos de uso

{% code title="Simple array with single conditional" %}
```handlebars
{{#url-param url}}{{phone}}{{/url-param}} 
// Output: 12323848374

{{#url-param url}}{{email}}{{/url-param}} 
// Output: john@gmail.com
```
{% endcode %}

Deberás escribir dentro del helper con la sintaxis `mustache` el nombre de la variable existente en la URL.

{% hint style="info" %}
Si la URL no posee parámetros, devolverá un valor vació como `String`.
{% endhint %}
