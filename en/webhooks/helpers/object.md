---
description: >-
  Below, you can find the documentation on how to use this
  helper.
---

## #object

With `#object`, as with the helper `#array` you can return a valid value, but it also allows you to select or filter `keys` within the object.

#### Original Structure

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

### Without modifying the schema

By default, it is not possible to select an `Object` with mustache syntax, so you can use this helper to return a valid `Object`.

{% tabs %}
{% tab title="With #object" %}
#### Syntax

```handlebars
{{#object user}}{{/object}}
```

#### Result

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

{% tab title="Without #object" %}
#### Syntax

```handlebars
{{user}}
```

#### Result

```javascript
[object Object]
```
{% endtab %}
{% endtabs %}

### Modifying the schema

This helper not only helps to return a valid `Object`, but also to select or filter certain `keys` or fields of the `Object`.

{% tabs %}
{% tab title="Individual selection" %}
#### Syntax

```handlebars
{{#object user}}id{{/object}}
```

#### Result

```json
{
  "id": "60cbc69048f3bd7cc732e028"
}
```
{% endtab %}

{% tab title="Multiple selection" %}
#### Syntax

```handlebars
{{#object user}}id,email,enabled{{/object}}
```

#### Result

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
Do not write key names or `keys` inside the `#object` helper as `String`, that is, with double or single quotes.
{% endhint %}