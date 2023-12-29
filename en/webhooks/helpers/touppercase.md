---
description: >-
  This documentation describes how to use this
  helper.
---

# toUpperCase

This type of helper allows you to mutate a `String`, converting all the text to uppercase.

{% hint style="info" %}
You should bear in mind that the value that is to be mutated must be a `String`, otherwise a format error will be returned.
{% endhint %}

#### Example data

```json
{ "name": "John Doe" }
```

## Usage examples

```handlebars
{{toUpperCase name}}
// Output: JOHN DOE
```