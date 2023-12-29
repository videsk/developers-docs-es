---
description: >-
  Below, you will be able to find the documentation on how to use this
  helper.
---

# parser

With `parser` it allows any data to be transformed to its corresponding data type, for example:

{% hint style="info" %}
Use this helper mainly when the format must be `JSON`.
{% endhint %}

The way to use it is `{{parser`` `<mark style="color:blue;">**`value`**</mark>`}}` where <mark style="color:blue;">**value**</mark> is the key you are going to use.<mark style="color:red;"></mark>&#x20;

#### Original Structure

```handlebars
{
"users": ["John", "Maria"]
}
```

{% tabs %}
{% tab title="With parser" %}
#### Syntax

```handlebars
{
"name": {{parser users.0}},
"listado": {{parser users}}
}
```

#### Result

```handlebars
{
"name": "John",
------^ (string is valid)
"listado": ["John", "Maria"]
--------- (array is valid)
}
```
{% endtab %}

{% tab title="Without parser" %}
#### Syntax

```handlebars
{
"name": {{users.0}},
"listado": {{users}}
}
```

#### Result

```handlebars
{
"name": John,
------^ Error: Parser.... (not a string)
"listado": John, Maria
----- Error: Parser.... (not an array)
}
```
{% endtab %}
{% endtabs %}