---
description: >-
  Below you can find the documentation on how to use this helper.
---

# #array

With `#array` you can mutate an array to the structure you want and/or return a valid `Array`.

{% hint style="info" %}
Use this helper mainly when the format must be `JSON`.
{% endhint %}

#### Original structure

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

### Without schema modification

By default, it is not possible to select an `Array` with mustache syntax, so you can use this helper to return a valid `Array`.

{% tabs %}
{% tab title="With #array" %}
#### Syntax

```handlebars
{{#arrray elements}}{{/array}}
```

#### Result

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

{% tab title="Without #array" %}
#### Syntax

```handlebars
{{elements}}
```

#### Result

```json
[object Object]
```
{% endtab %}
{% endtabs %}

### Modifying the schema

This helper not only helps to return a valid array, but also to modify its structure when its values are objects (`Object`). To do this, you must write inside the helper `#array`.

```handlebars
{{#array elements}} {{/array}}
-------------------^ (write inside the helper)
```

For example, if you need the result to be an `Array` of objects, where each object contains an `id` and `value` you must write the following:

{% tabs %}
{% tab title="Array of objects" %}
#### Syntax

{% code title="Using double quotes" %}
```handlebars
{{#array elements}}{ "id": "{{_id}}", "name": "{{value}}" }{{/array}}
```
{% endcode %}

#### Result

```json
[
  {
    "id": "60cbc69048f3bd7cc732e028",
    "name": "Customer Service"
  }
]
```

In this way the original object was transformed but the result is still an `Array` with objects.



{% hint style="info" %}
You can also complement helpers together like `#array` with `parser`.

**This way you make sure that the value is valid and does not happen that an `object`, `array`, `boolean`, etc. is between double quotes.**
{% endhint %}

{% code title="Using parser" %}
```handlebars
{{#array elements}}{ "id": {{parser _id}}, "name": {{parser value}} }{{/array}}
```
{% endcode %}
{% endtab %}

{% tab title="Simple array" %}
{% hint style="warning" %}
You can only define one `key` for each object if it is an `Array` of objects.
{% endhint %}

#### Syntax

```handlebars
{{#array fields}}name{{/array}}
```

#### Result

```json
["Customer Service"]
```

In this way it has become an `Array` simple without objects.
{% endtab %}
{% endtabs %}