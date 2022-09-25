---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #object

Con `#object` al igual que con el helper `#array` podrás retornar el valor válido, pero también permite seleccionar o filtrar `keys` dentro del objeto.

#### Estructura original

```json
{
    "user": {
        "id": "60cbc69048f3bd7cc732e028",
        "email": "john.doe@example.com",
        "roles": ["61d361eb90ed8cb03f9f8315", "61d361f8025599da830659ff"],
        "enabled": true,
        "createdAt": "2020-01-07T02:47:40.289+00:00",
    }
}
```

### Sin modificación del esquema

Por defecto, no es posible seleccionar un `Object` con sintaxis mustache, por lo que puedes usar este helper para retornar un `Object` válido.

{% tabs %}
{% tab title="Con #object" %}
#### Sintaxis

```handlebars
{{#object user}}{{/object}}
```

#### Resultado

```json
{
   "id": "60cbc69048f3bd7cc732e028",
   "email": "john.doe@example.com",
   "roles": ["61d361eb90ed8cb03f9f8315", "61d361f8025599da830659ff"],
   "enabled": true,
   "createdAt": "2020-01-07T02:47:40.289+00:00",
 }
```
{% endtab %}

{% tab title="Sin #object" %}
#### Sintaxis

```handlebars
{{user}}
```

#### Resultado

```javascript
[object Object]
```
{% endtab %}
{% endtabs %}

### Modificando el esquema

Este helper no solo ayuda a retonar un `Object` válido, si no que también seleccionar o filtrar ciertos `keys` o campos del `Object`.

{% tabs %}
{% tab title="Selección individual" %}
#### Sintaxis

```handlebars
{{#object user}}id{{/object}}
```

#### Resultado

```json
{
    "id": "60cbc69048f3bd7cc732e028"
}
```
{% endtab %}

{% tab title="Selección multiple" %}
#### Sintaxis

```handlebars
{{#object user}}id,email,enabled{{/object}}
```

#### Resultado

```json
{
    "id": "60cbc69048f3bd7cc732e028",
    "email": "john.doe@example.com",
    "enabled": true
}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
No escribas nombre de claves o `keys` dentro del helper `#object` como `String`, es decir, con comillas dobles o simples.
{% endhint %}
