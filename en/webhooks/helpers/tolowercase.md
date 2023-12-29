---
description: >-
  Here you can find the usage documentation of this helper.
---

# toLowerCase

This helper allow you to mutate a `String` to all lowercase text.

{% hint style="info" %}
Consider that the value to mutate must be a `String`, otherwise a format error will be thrown.
{% endhint %}

#### Sample data

```json
{ "name": "John Doe" }
```

## Usage examples

```handlebars
{{toLowerCase name}}
// Output: john doe
```