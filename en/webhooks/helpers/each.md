---
description: >-
In the following section, you can find the documentation of how to use the
helper.
---

# #each

This helper allows iterating over an `Array` to generate a custom output.

{% hint style="success" %}
You can use this helper with any output, while [`#array`](array.md) is designed for `JSON` output.
{% endhint %}

#### Example data

```json
{
"users": [
{
"name": "John Doe",
"latestConnection": "2021-08-21T23:26:13.000Z"
},
{
"name": "Maria Doe",
"latestConnection": "2021-09-08T20:17:48.000Z"
}
]
}
```

## Usage examples

{% hint style="warning" %}
This helper will output the values as plain text, so be careful with values like `Arrays` and `Objects`.
{% endhint %}

{% tabs %}
{% tab title="XML" %}
#### Syntax

```handlebars
<users>
{{#each users}}
<user>
<name>{{name}}</name>
<lastConnection>{{latestConnection}}</lastConnection>
</user>
{{/each}}
</users>
```

#### Result

```xml
<users>
<user>
<name>John Doe</name>
<lastConnection>2021-08-21T23:26:13.000Z</lastConnection>
</user>
<user>
<name>Maria Doe</name>
<lastConnection>2021-09-08T20:17:48.000Z</lastConnection>
</user>
</users>
```
{% endtab %}

{% tab title="JSON" %}
{% hint style="info" %}
For the `JSON` output, we suggest using the [`#array`](array.md) helper.
{% endhint %}
{% endtab %}

{% tab title="Markdown" %}
#### Syntax

```handlebars
# Users
| Name | Last connection |
|----------|:-------------:|
{{#each users}}
| {{name}} | {{latestConnection}} |
{{/each}}
```

#### Result

```markdown
# Users
| Name | Last connection |
|----------|:-------------:|
| John Doe | 2021-08-21T23:26:13.000Z |
| Maria Doe | 2021-09-08T20:17:48.000Z |

```
{% endtab %}