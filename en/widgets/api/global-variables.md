---
description: >-
  Next, we explain how to access the widget using global
  variables
---

# Global variables

There are currently two global variables that you can use to access the widget:

* `window.videsk`
* `videsk`

The problem with these global variables is that they are available only once the widget is fully loaded, which could cause undefined global variable errors.

For this, we have global variables that the widget observes before loading in order to modify its default behavior.

These are:

#### Start hidden

```
window.__VIDESK_WIDGET_START_HIDE__
```

&#x20; This global variable by setting its value to `true` allows the widget to start completely hidden.

#### Deferred start

```
window.__VIDESK_LOAD_DEFERER__
```

This global variable, when set to `true`, prevents the widget from loading until the `render` method is executed.

## How to hide the widget?

To hide the widget while it is loading, you must add the following global variable to your site before the Videsk Widget `script`:

{% hint style="warning" %}
This action is meant to hide the widget entirely. In other words, both the body and the floating bubble.

**Recommended if you need to toggle visibility from a site component.**
{% endhint %}

{% tabs %}
{% tab title="Global var" %}
```javascript
// This before script !!
window.__VIDESK_WIDGET_START_HIDE__ = true;

<script src="..." videsk-token="..." async></script>
```
{% endtab %}

{% tab title="Onload" %}
```javascript
// This before script !!

window.__VIDESK_WIDGET_ONLOAD__ = function() {
  videsk.toggleVisibility(true || false)
}

<script src="..." videsk-token="..." async></script>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Remember that you can access the Widget API through the `videsk` global variable.
{% endhint %}

## Deferred load

Deferred loading is recommended for high-traffic websites or during hot sales seasons. We suggest adding this behavior based on clicks on external elements such as custom buttons, banners, etc.

{% hint style="warning" %}
You **must add** the following code **before loading the widget**.
{% endhint %}

```javascript
window.__VIDESK_LOAD_DEFERER__ = true;

// Load widget script ....
// After widget script ...
document.querySelector('#my-button').addEventListener('click', async () => {
  if (!window.videsk) return;
  await videsk.render();
  videsk.toggle();
});
```

This way, you will only load the widget when a customer interacts with a custom element by clicking on it.

{% hint style="danger" %}
In the interests of quality of service, if we detect high traffic peaks, we may block loading on your website until you apply this strategy.
{% endhint %}