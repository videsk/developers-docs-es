---
description: Customize your users experience with Phone.
---

# 📞 Phone

With `Phone` you can create calls programmatically, without worrying about connections, parameters, exceptions, etc.

Phone is compatible with any environment and framework, whether native, Svelte, Vue, React, Angular, etc.

## Installation

To get started, you will need to install our resource on your website or mobile application. You have the following alternatives.

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/sdk/phone.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://assets.videsk.io/js/sdk/phone.min.js";
document.body.appendChild('body'); // Or replace with the DOM node of your choice
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Do not store the script content on your server, **this violates our terms of use**.
{% endhint %}

{% hint style="danger" %}
For security and quality of service reasons, we have a limit of requests per second per IP/Token, which consists of 20 requests in 1 second. Avoid exceeding this limit, as our Rest API will block your clients' requests.
{% endhint %}

## Instantiation

First you must instantiate `VideskPhone` as a [constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor).

```javascript
const phone = new VideskPhone(APIToken);
```

In the variable `phone` you will be able to access the methods and properties.

{% hint style="info" %}
If you instantiate `VideskPhone` without a token, it will automatically try to extract it from the URL, so you can use `token`, `videsk-token` or `api-key` as a parameter in the URL.&#x20;
{% endhint %}

```
https://example.com?api-key=eyJhbGciOiJIUzI1NiIsI...
```

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Methods</strong></td><td>List of methods available on Phone.</td><td></td><td><a href="methods.md">methods.md</a></td></tr><tr><td><strong>Events</strong></td><td>List of events available on Phone.</td><td></td><td><a href="events.md">events.md</a></td></tr></tbody></table>
