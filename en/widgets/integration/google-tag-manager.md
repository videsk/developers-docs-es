---
description: >-
  You'll see how to quickly integrate our widgets on your website.
---

# 🔌 Installation

The basic way to integrate is through a script. This script loads resources needed to render the widget, which consists on HTML, CSS, and Javascript.

## Integration Script

{% hint style="info" %}
We are not compatible with [SRI (Subresource Integrity)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource\_Integrity), otherwise, we could not provide constant updates and improvements that are every week.
{% endhint %}

{% embed url="https://www.loom.com/share/68ea3f599d9f4c7cad50f126cd5b37cd?sid=cb16d1fa-f5c2-4cc1-b206-5d5477afc017" %}

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/videsk-widget.min.js" videsk-token="REPLACE_TOKEN" async></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement("script");
script.src = "https://assets.videsk.io/js/videsk-widget.min.js";
script.setAttribute("videsk-token", "REPLACE_TOKEN");
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

You can access the documentation of our API at the following link:

{% content-ref url="../api/" %}
[api](../api/)
{% endcontent-ref %}