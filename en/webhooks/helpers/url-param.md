---
description: >-
  Below you can find the documentation on using this
  helper.
---

# #url-param

This type of helper is useful for obtaining the value of a URL's parameters.

#### Sample data

```json
{
  "url": "https://website.com?phone=12323848374&email=john@gmail.com"
}
```

## Usage examples

{% code title="Simple array with single conditional" %}
```handlebars
{{#url-param url}}{{phone}}{{/url-param}}
// Output: 12323848374

{{#url-param url}}{{email}}{{/url-param}}
// Output: john@gmail.com
```
{% endcode %}

You must write the name of the variable in the URL using the mustache syntax in the helper.

{% hint style="info" %}
If the URL does not have parameters, it will return an empty string.
{% endhint %}