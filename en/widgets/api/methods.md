---
description: Methods available to perform actions in a 100% programmatic way
---

# Methods

{% hint style="warning" %}
Remember that to access any method you must use the global `videsk` variable.

\
This is available as `window.videsk` or `videsk`.
{% endhint %}

## `home`

This method allows you to go to the initial view of the widget. It does not receive any arguments.

{% code lineNumbers="true" %}
```javascript
videsk.home();
```
{% endcode %}

{% hint style="warning" %}
Executing this method when you are on a call may result in unexpected behaviors.
{% endhint %}

## `segment`

This method allows you to call a segment by its ID programmatically. It receives an argument which is the ID of the segment to call.

{% code lineNumbers="true" %}
```javascript
videsk.segment(segmentId);
```
{% endcode %}

{% hint style="info" %}
This method simulates a user click on the segment, therefore the next view could be a not available message, form or microphone/camera selection.



The above depends on your account configuration.
{% endhint %}

## `calendar`

This method allows you to enter a calendar of a particular service or agent programmatically. It receives two arguments which are:

* `service`: corresponds to the service id (mandatory)
* `agent`: corresponds to the agent id

{% hint style="warning" %}
The ID of the `service` is mandatory, while `agent` is optional and will depend on the service configuration in question.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.calendar(serviceId); // Will select the service

videsk.calendar(serviceId, agentId); // Will select service and agent
```
{% endcode %}

{% hint style="info" %}
If the service was configured as manual selection and the `agent` argument is not passed, the widget view will remain in the list of agents associated with the service.
{% endhint %}

## `getByStatus`

This method allows you to get the number of executives that are connected to a particular segment. It receives two arguments, the first mandatory one corresponds to the segment ID as `String` and the second optional one as `String` that corresponds to the status to look for, which can be `online` (by default) or `available`.

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

```javascript
await videsk.getByStatus(segmentId); // By default it looks for online

await videsk.getByStatus(segmentId, 'available'); // It will search for available
```

{% hint style="warning" %}
You must check that the return value is not an error instance, that is:

```
const response = await videsk.getByStatus(segmentId);
if (response instanceof Error) return console.error('Error', response.message);
const total = response;
```
{% endhint %}

## `toggle`

This is the function to toggle the widget view, which triggers the same event when a customer clicks the floating button.

It receives an argument which is a `boolean` indicating the state. If no argument is provided, it will toggle its state `true/false`.

{% tabs %}
{% tab title="Toggle" %}
```javascript
// To show
videsk.toggle(true);

// To hide
videsk.toggle(false);

// Auto
videsk.toggle();
```
{% endtab %}

{% tab title="On load web" %}
<pre class="language-javascript"><code class="lang-javascript">// Use window.__VIDESK_WIDGET_ONLOAD__ only for load events not for functions
<strong>window.__VIDESK_WIDGET_ONLOAD__ = function() {
</strong> videsk.toggle();
}
</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Do not use `window.onload` or `window.addEventListener("onload")` to use the `toggle` function.
{% endhint %}

## `toggleVisibility`

This method allows you to show or hide the widget completely.

It receives an argument which is a `boolean` indicating the state. If no argument is provided, it will toggle its state `true/false`.

```javascript
videsk.toggleVisibility();
// or
videsk.toggleVisibility(false);
```

## `render`

This method allows you to render the widget when it has been requested to load lazily.

{% hint style="warning" %}
This method is asynchronous, so you should use `async/await` or `promises` to continue interacting with the widget.
{% endhint %}

```javascript
await videsk.render();
// Or
videsk.render().then(...)
```

{% hint style="info" %}
If you execute this method more than 1 time, the widget will throw a `warning` in the console.
{% endhint %}

## `devices`

This method allows you to get the list of devices available on the computer.

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
await videsk.devices();
```
{% endcode %}

## `device`

This method allows you to get a particular device by searching for its ID or name. It receives two arguments:

* `name`: Device name
* `type`: device type. Available `audioinput` and `videoinput`. By default: `audioinput`.

{% hint style="info" %}
The value you indicate as the first argument will be searched for by match, not strict equality.
{% endhint %}

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
await videsk.device('Sound BlasterX', 'audioinput'); // 4c59e1553b44981af704f3778bc75c8bfbeabf0849b4357c4e9222104f1a794
```
{% endcode %}

In case the device is not found it will return `undefined`.