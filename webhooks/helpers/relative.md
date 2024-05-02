---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# #relative

Este tipo de helper tiene como utilidad transformar un fecha `Date` a texto humanamente legible de forma relativa. Ej: `dentro 1 hora`.

{% hint style="info" %}
Te sugerimos utilizar este helper para enviar recordatorios con mensaje como "dentro 2 horas".
{% endhint %}

Los argumentos que recibe este helper son los siguientes:

* Fecha
* Formato ([BCP 47 language tag](../formatos-locales.md))**\***

Luego dentro del helper podrás ingresar como un JSON con las opciones disponibles en la API de Javascript [Intl.RelativeTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/RelativeTimeFormat/RelativeTimeFormat), opciones que darán el formato que necesites junto con el cambio de horario correspondiente a la zona horaria que ingreses.

{% hint style="info" %}
Recuerda que el formato de las opciones es en JSON, cada nombre de opción deberá tener comillas dobles.
{% endhint %}

## Ejemplos de uso

{% code title="Datos de ejemplo" %}
```json
{
    "startedAt": "2021-10-01T05:51:36.000Z"
}
```
{% endcode %}

{% code title="UTC a hora Santiago" %}
```handlebars
{{#relative startedAt 'es-CL'}}
    {
        "style": "long",
        "localeMatcher": "lookup",
    }
{{/relative}}
```
{% endcode %}

La salida de este helper será `hace 3 años`

***

## Valores por defecto

{% hint style="warning" %}
Lee con detención los valores por defecto, ya que la salida de la fecha podría variar.
{% endhint %}

Por defecto, al usar este helper **sin entregar opciones** el estilo (style) será **`long`** .

Adicionalmente, añadimos por defecto las opciones con los siguientes valores, los cuáles son reemplazados solo si están definidos en tus opciones ingresadas.

{% code title="Opciones por defecto" %}
```javascript
{
    "style": "long",
    "numeric": "auto",
    "localeMatcher": "best fit"
}
```
{% endcode %}

***

## Opciones

Lee las opciones a continuación, cada una de ellas te permitirá realizar modificaciones en el formato, cálculo en base a calendario, zona horaria, etc.

{% hint style="warning" %}
El nombre de la opción es sensible a mayúsculas y minúsculas.
{% endhint %}

{% hint style="success" %}
Recuerda que son **opciones**, puedes usar todas, algunas o ninguna.
{% endhint %}

{% hint style="info" %}
Las opciones disponibles actualizadas siempre las podrás encontrar [acá](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/RelativeTimeFormat/RelativeTimeFormat).
{% endhint %}

#### localeMatcher

Podrás definit el algoritmo de coincidencia regional que se utilizará. Los valores posibles son `lookup` y `best fit`, y el valor predeterminado es `best fit`.

```handlebars
{{#relative startedAt}}{ "localeMatcher": "best fit" }{{/relative}}
```

#### numberingSystem

Podrás definir el sistema de numeración que se utilizará para el formato de números, como `arab`, `hans`, `mathsans`, etc.

```handlebars
{{#relative startedAt}}{ "numberingSystem": "a" }{{/relative}}
```

#### style

Podrás escoger entre los siguientes formatos para la salida:

| style    | Ejemplo      |
| -------- | ------------ |
| `long`   | dentro 1 mes |
| `short`  | en 1 d.      |
| `narrow` | en 2 mes.    |

```handlebars
{{#relative startedAt}}{ "style": "long" }{{/relative}}
```

#### numeric

Podrás definir si se deben utilizar valores numéricos en la salida. Los valores posibles son `always` y `auto`, y el valor predeterminado es `always`.

```handlebars
{{#relative startedAt}}{ "numeric": "always" }{{/relative}}
```

{% hint style="info" %}
Para más información sobre el uso de <mark style="color:purple;">`@root`</mark> o <mark style="color:purple;">`this`</mark> [haz clic aquí](../sintaxis.md#contenido-de-un-helper).
{% endhint %}
