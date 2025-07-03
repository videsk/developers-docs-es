---
description: >-
  A continuación te explicamos como funcionan los Webhooks personalizados para
  integraciones.
---

# 🦰 Sintaxis

Para utilizar los webhooks personalizados debes conocer acerca de la sintaxis que utilizamos, la cual está basada en [&#x4D;_&#x75;stache_](https://mustache.github.io/), una librería de código abierto que nos permite generar la estructura personalizada.

Básicamente deberás utilizar llaves <mark style="color:purple;">`{{ }}`</mark> o conocidos como "_curly braces"_. Esta sintaxis te permite acceder a valores que te entregamos para cada evento.

Como se menciona anteriormente en la sección de [variables](variables.md#variables-por-evento), cada evento posee sus propios valores. Todos estos valores provienen de un `JSON` que posteriormente son inyectados basado en las variables que hayas escrito.

Por ejemplo, un `JSON` igual a `{ "name": "John Doe" }` te permitirá usar su variable `name` en sintaxis _mustache_, por lo que si deseo solo obtener el nombre (`name`) como texto plano deberé escribir <mark style="color:purple;">`{{ name }}`</mark> , obteniendo como resultado `John Doe`.

{% hint style="info" %}
Podrás escribir sintaxis _mustache_ con o sin espacios entre las llaves o _curly braces_.
{% endhint %}

***

## Tipos de datos

Dependiendo del tipo de dato podrás acceder mediante una sintaxis específica.

### Object

Para acceder a los valores de un `Object` deberás utilizar un punto `.` al igual que en Javascript. Por ejemplo:

```handlebars
{{ order.total }}
```

```handlebars
{{ order.product.description.pricing }}
```

### Array

Para acceder particularmente a `Array` existen varias sintaxis. Por ejemplo para el valor del primer elemento deberás indicar el índice al igual que en Javascript, pero separado un punto `.`

```handlebars
{{ orders.0 }}
```

En el caso que el `Array` esté compuesto por `Object` podrás acceder a los valores de cada objeto mediante la separación de puntos `.` de la siguiente manera:

```handlebars
{{ orders.0.productId }}
```

{% hint style="info" %}
En el caso que el formato requerido sea un JSON te sugerimos utilizar helpers como [`#array`](helpers/array.md) u [`#object`](helpers/object.md), para que los valores de salida sean válidos.
{% endhint %}

***

## Helpers

Los helpers son funciones que te ayudarán con estructura, tipo de datos, iteración sobre listados, etc.

Estos se componen de una nomenclatura, la cual varía según su función. Existen dos tipos de helpers, algunos de ellos pueden ser simples o compuestos, y en algunos casos ambos al mismo tiempo.

### Simples

Estos tipos de helpers se componen de un nombre + variable que desees usar, por ejemplo:

```handlebars
{{parser myValue}}
```

Donde `parser` es el nombre del helper, mientras que `myValue` es la variable a utilizar.

### Compuestos

Estos tipos de helpers se componen de un nombre + variable + contenido, donde algunas veces el contenido puede ser opcional. Por ejemplo:

```handlebars
{{#if myValue}}{{/if}}
```

En este caso **`if`** es el nombre del helper, pero se debe anteponer un `hashtag` **#** y finalizar con el mismo nombre anteponiendo un `slash` **/**.

Por lo tanto, a modo de ficción si tenemos un helper compuesto llamado `mySuperHelper`, se deberá escribir de la siguiente forma:

```handlebars
{{#mySuperHelper myValue}}{{/mySuperHelper}}
```

Dentro del helper es posible añadir contenido, el cual como se mencionó es opcional. Dependiendo de cada helper podrás generar contenido dinámico. Para conocer las funciones de cada uno dirígete a la siguiente sección de [helpers](helpers/).

Existen casos como el helper parser, que es simple y compuesto, por lo tanto lo puedes usar de la siguiente manera:

{% tabs %}
{% tab title="Simple" %}
```handlebars
{{parser myValue}}
```
{% endtab %}

{% tab title="Compuesto" %}
```handlebars
{{#parser}}
    {{myValue}}
{{/parser}}
```
{% endtab %}
{% endtabs %}

### Contenido

Dentro del contenido podrás acceder a variables dependiendo de los helpers, pero existen dos los cuales son nativos y haran referencia a diferentes valores dependiendo del contexto.

<mark style="color:purple;">`this`</mark> el cual hace referencia al valor de iteración o a la raíz del `JSON`. Por ejemplo:

```handlebars
{{#each orders}}
  Order number {{this}} <--- referencia a cada valor del array "orders" 
{{/each}}
```

```handlebars
{{this}}
```

<mark style="color:purple;">`@root`</mark> el cual accede a todo el JSON, es muy útil si deseas acceder a la raíz. Por ejemplo:

```handlebars
[
 {{#each orders}}
  { 
   "order": {{this}}, <------ referencia a cada valor del array "orders"
   "date": {{@root.createdAt}} <------ referencia a "createdAt" del JSON raíz
  } 
 {{/each}}
]
```

Adicionalmente, dentro de un helper compuesto es posible usar helpers anidados, es decir:

```handlebars
{{#array}}
    {{#if}}...{{/if}}
{{/array}}
```

{% hint style="info" %}
No existe un límite de anidación, pero sugerimos mantener la simplicidad en orden de mantenibilidad.
{% endhint %}

***

Ahora que ya conoces como utilizar la sintaxis `{{ mustache }}` y `helpers` te invitamos a continuar con el listado de [helpers disponibles](helpers/).
