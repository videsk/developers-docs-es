---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #each

Este helper permite iterar sobre un `Array` para generar un formato con cada valor descrito.

{% hint style="success" %}
Puedes utilizar este helper con cualquier formato, a diferencia de [`#array`](array.md) que es específicamente para formato `JSON`.
{% endhint %}

#### Datos de ejemplo

```json
{
    "users": [
        {
            "name": "John Doe",
            "latestConnection": "2021-08-21T23:26:13.000Z"
        },
        {
            "name": "Maria Doe",
            "latestConnection": "2021-09-08T20:17:48.000Z"
        }
    ]
}
```

## Ejemplos de uso

{% hint style="warning" %}
Este helper retornará los valores como texto plano, por lo que debes tener cuidado con valores como `Array` y `Object`.
{% endhint %}

{% tabs %}
{% tab title="XML" %}
#### Sintaxis

```handlebars
<users>
    {{#each users}}
        <user>
            <name>{{name}}</name>
            <lastConnection>{{latestConnection}}</lastConnection>
        </user>
    {{/each}}
</users>
```

#### Resultado

```xml
<users>
    <user>
        <name>John Doe</name>
        <lastConnection>2021-08-21T23:26:13.000Z</lastConnection>
    </user>
    <user>
        <name>Maria Doe</name>
        <lastConnection>2021-09-08T20:17:48.000Z</lastConnection>
    </user>
</users>
```
{% endtab %}

{% tab title="JSON" %}
{% hint style="info" %}
Para el caso de formato `JSON` te sugerimos utilizar el helper [`#array`](array.md).
{% endhint %}
{% endtab %}

{% tab title="Markdown" %}
#### Sintaxis

```handlebars
# Usuarios
| Nombre   | Última conexión |
|----------|:-------------:|
{{#each users}}
| {{name}} | {{latestConnection}} |
{{/each}}
```

#### Resultado

```markdown
# Usuarios
| Nombre   | Última conexión |
|----------|:-------------:|
| John Doe | 2021-08-21T23:26:13.000Z |
| Maria Doe | 2021-09-08T20:17:48.000Z |

```
{% endtab %}
{% endtabs %}
