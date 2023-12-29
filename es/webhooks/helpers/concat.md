---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #concat

Este tipo de helper tiene como utilidad combinar dos `Array` en uno.

{% hint style="info" %}
Este helper está diseñado para ser utilizado solamente con `Array.`
{% endhint %}

#### Datos de ejemplo

```json
{
    "users": [
        {
            "id": "61d389418a63e556a14d704d",
            "name": "John Doe",
            "org": "61d389800464df1d4ea02c7b"
        },
        {
            "id": "61d3895e3f52541cf9709398",
            "name": "Maria Doe",
            "org": "61d389800464df1d4ea02c7b"
        }
    ],
    "customers": [
        {
            "id": "61d38a3a49cfea276739506f",
            "email": "john.doe@business.com",
        },
        {
            "id": "61d38a3e1a257213607919bc",
            "email": "ma.doe@business.com",
        }
    ]
}
```

## Ejemplos de uso

{% hint style="warning" %}
Deberás usar este helper en conjunto con [parser](parser.md), de lo contrario obtendrás un error.
{% endhint %}

```handlebars
{{#concat users}}{{parser @root.customers}}{{/concat}}
// Output: [{ "name": "John Doe", ... }, { "email": "john.doe@business.com", ... }]
```

{% hint style="info" %}
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
