---
description: >-
  How to work with custom webhooks for integrations.
---

# 🦰 Syntax

To use custom webhooks, you need to know about the syntax we use, which is based on [M_ustache_](https://mustache.github.io/), an open-source library that lets us generate custom structures.

Basically, you'll use curly braces `{{ }}`. This syntax allows you to access values that we provide for each event.

As mentioned before in the section on [variables](variables.md#variables-by-events), each event has its own values. All these values come from a JSON which is then injected based on the variables you have written.

For example, a JSON equal to `{ "name": "John Doe" }` will allow you to use its `name` variable in mustache syntax, so if I want to get only the name as plain text I will write {{ name }}, getting `John Doe` as a result.

{% hint style="info" %}
You can write mustache syntax with or without spaces between the curly braces.
{% endhint %}

## Data Types

Depending on the data type, you can access it using a specific syntax.

### Object

To access the values of an Object, you have to use a dot `.` just like in Javascript. For example:

```handlebars
{{ order.total }}
```

```handlebars
{{ order.product.description.pricing }}
```

### Array

There are several syntaxes to access an Array in particular. For example, for the value of the first element you must indicate the index just like in Javascript, but separated by a dot `.`.

```handlebars
{{ orders.0 }}
```

In the case that the Array is composed of Objects, you can access the values of each object by separating dots `.` in the following way:

```handlebars
{{ orders.0.productId }}
```

{% hint style="info" %}
If the required format is JSON, we suggest you use helpers like [`#array`](helpers/array.md) or [`#object`](helpers/object.md) so that the output values are valid.
{% endhint %}

## Helpers

Helpers are functions that will help you with structure, data type, iteration over lists, etc.

These are made up of a nomenclature which varies according to their function.

### Simple

These types of helpers are made up of a name + the variable that you wish to use, for example:

```handlebars
{{parser myValue}}
```

Where `parser` is the name of the helper while `myValue` is the variable to be used.

### Compound

These types of helpers are made up of a name + variable + content, where sometimes the content can be optional. For example:

```handlebars
{{#if myValue}}{{/if}}
```

In this case **`if`** is the name of the helper, but a `hashtag` **#** must be prefixed to it and finalised with the same name prefixed with a `slash` **/**.

Therefore, as a fiction if we had a compound helper called `mySuperHelper` it should be written in the following way:

```handlebars
{{#mySuperHelper myValue}}{{/mySuperHelper}}
```

It is possible to add content in the helper, which as mentioned is optional. Depending on each helper, you will be able to generate dynamic content. To find out the functions of each one, go to the following section [helpers](helpers/).

## Content of a helper

Within the content you can access variables depending on the helpers, but there are two which are native and refer to different values depending on the context.

<mark style="color:purple;">`this`</mark> which references the iteration value or the root of the JSON. For example:

```handlebars
{{#each orders}}
    Order number {{this}} <--- reference to each value of the "orders" array
{{/each}}
```

```handlebars
{{this}}
```

<mark style="color:purple;">`@root`</mark> which accesses the entire JSON, it is very useful if you wish to access the root. For example:

```handlebars
[
{{#each orders}}
    {
    "order": {{this}}, <------ reference to each value of the "orders" array
    "date": {{@root.createdAt}} <------ reference to "createdAt" from the root JSON
    }
{{/each}}
]
```

Now that you know how to use the `{{ mustache }}` syntax and `helpers` we invite you to continue with the list of [helpers available](helpers/).