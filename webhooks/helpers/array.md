---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #array

Con `#array` podrás mutar una matriz (`Array`) a la estructura que desees y/o devolver un `Array` válido.

{% hint style="info" %}
Utiliza este helper principalmente cuando el formato debe ser `JSON`.
{% endhint %}

#### Estructura original

```javascript
{
    "elements": [
        {
            "_id": "60cbc69048f3bd7cc732e028",
            "name": "Segment",
            "value": "Customer Service"
        }
    ]
}
```

### Sin modificación del esquema

Por defecto, no es posible seleccionar un `Array` con sintaxis mustache, por lo que puedes usar este helper para retornar un `Array` válido.

{% tabs %}
{% tab title="Con #array" %}
#### Sintaxis

```handlebars
{{#arrray elements}}{{/array}}
```

#### Resultado

```javascript
[
    {
       "_id": "60cbc69048f3bd7cc732e028",
       "name": "Segment",
       "value": "Customer Service"
    }
]
```
{% endtab %}

{% tab title="Sin #array" %}
#### Sintaxis

```handlebars
{{elements}}
```

#### Resultado

```json
[object Object]
```
{% endtab %}
{% endtabs %}

### Modificando el esquema

Este helper no solo ayuda a retonar un Array válido, si no que también modificar su estructura cuando sus valores son objetos (`Object`). Para ello deberás escribir dentro del helper `#array`.

```handlebars
{{#array elements}}  {{/array}}
-------------------^ (escribe dentro del helper)
```

Por ejemplo, si necesitas que el resultado sea un `Array` de objetos, donde cada objeto contenga un `id` y `value` deberás escribir lo siguiente:

{% tabs %}
{% tab title="Array de objetos" %}
#### Sintaxis

{% code title="Usando comillas dobles" %}
```handlebars
{{#array elements}}{ "id": "{{_id}}", "name": "{{value}}" }{{/array}}
```
{% endcode %}

#### Resultado

```json
[
    {
        "id": "60cbc69048f3bd7cc732e028",
        "name": "Customer Service"
    }
]
```

De esta forma se transformó el objeto original pero el resultado sigue siendo un `Array` con objetos.



{% hint style="info" %}
También puedes complementar helpers en conjunto como `#array` con `parser`.



**De esta forma te aseguras que el valor sea válido y no ocurra que un `object`, `array`, `boolean`, etc. esté entre comillas dobles.**
{% endhint %}

{% code title="Usando parser" %}
```handlebars
{{#array elements}}{ "id": {{parser _id}}, "name": {{parser value}} }{{/array}}
```
{% endcode %}
{% endtab %}

{% tab title="Array simple" %}
{% hint style="warning" %}
Solo podrás definir una `key` de cada objeto si es un `Array` de objetos.
{% endhint %}

#### Sintaxis

```handlebars
{{#array fields}}name{{/array}}
```

#### Resultado

```json
["Customer Service"]
```

De esta forma se transformó consigue un `Array` simple sin objetos.
{% endtab %}
{% endtabs %}

## ``
