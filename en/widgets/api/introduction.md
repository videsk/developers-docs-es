# Introduction

Our Widget product has the ability to be interacted with using its own API. This enables developers to customize its behavior based on events or functions available to them.

To access the API, you must use the global variable:

```javascript
videsk
// Or
window.videsk

// Example
videsk.toggle();
// Or
window.videsk.toggle();
```

### Enable debug mode

To enable debug mode, you will need to assign the value `true` to the global variable `__VIDESK_WIDGET_DEBUG__` before loading the `script`.

```javascript
window.__VIDESK_WIDGET_DEBUG__ = true;
```

This will allow displaying information about the state of the events and the status of the functions in the console, each with their corresponding return values.

{% hint style="danger" %}
**Don't forget to remove debug mode in production mode.**
{% endhint %}

The following describes the use of the events and functions available as an API.

{% hint style="info" %}
Before you begin, remember to use the global variable `videsk` to access the Widget API.
{% endhint %}

{% content-ref url="global-variables.md" %}
[global-variables.md](global-variables.md)
{% endcontent-ref %}

{% content-ref url="methods.md" %}
[methods.md](methods.md)
{% endcontent-ref %}

{% content-ref url="events.md" %}
[events.md](events.md)
{% endcontent-ref %}

{% content-ref url="design.md" %}
[design.md](design.md)
{% endcontent-ref %}