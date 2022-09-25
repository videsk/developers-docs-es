---
description: >-
  A continuación, podrás encontrar la documentación de como utilizar este
  helper.
---

# parser

Con `parser` permite que cualquier dato sea transformado a su tipo de dato correspondiente, por ejemplo:

{% hint style="info" %}
Utiliza este helper principalmente cuando el formato debe ser `JSON`.
{% endhint %}

La forma de utilizarlo es `{{parser`` `<mark style="color:blue;">**`value`**</mark>`}}` donde <mark style="color:blue;">**value**</mark> es la clave que vas a utilizar. <mark style="color:red;"></mark>&#x20;

#### Estructura original

```handlebars
{
    "users": ["John", "Maria"]
}
```

{% tabs %}
{% tab title="Con parser" %}
#### Sintaxis

```handlebars
{
    "name": {{parser users.0}},
    "listado": {{parser users}}
}
```

#### Resultado

```handlebars
{
    "name": "John",
      ------^ (válido es string)
    "listado": ["John", "Maria"]
      --------- (válido es array)
}
```
{% endtab %}

{% tab title="Sin parser" %}
#### Sintaxis

```handlebars
{
    "name": {{users.0}},
    "listado": {{users}}
}
```

#### Resultado

```handlebars
{
    "name": John,
     ------^ Error: Parser.... (no es string)
    "listado": John, Maria
         ----- Error: Parser.... (no es array)
}
```
{% endtab %}
{% endtabs %}
