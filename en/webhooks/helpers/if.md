---
description: >-
  Below you will find the documentation on how to use this
  helper.
---

# #if

This type of helper allows you to generate a structure based on conditions, this is useful if the structure must vary depending on a value of type `Boolean`.

#### Sample data

```json
{
  "isOnline": true,
  "isAvailable": false,
  "data": [{ "id": "61d3905e6ee6a2321c88f7af" }, ...],
}
```

## Usage examples

{% hint style="info" %}
Keep in mind that the value to be compared can only be type `Boolean`.
{% endhint %}

{% tabs %}
{% tab title="if" %}
#### Syntax

```handlebars
{{#if isOnline}}
    {{parser data}}
{{/if}}
```

#### Result

```json
[{ "id": "61d3905e6ee6a2321c88f7af" }, ...]
```
{% endtab %}

{% tab title="if/else" %}
#### Syntax

```handlebars
{{#if isAvailable}}
    {{parser data}}
{{else}}
    { message: "The user is not available" }
{{/if}}
```

#### Result

```json
{ message: "The user is not available" }
```
{% endtab %}
{% endtabs %}