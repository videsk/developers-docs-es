# Events

Our widget emits a `videsk-load` event when loaded, which can be used to start interacting with the widget, since it has a diferred, async load:

```javascript
document.addEventListener('videsk-load', () => {
    // You can use the global variable videsk now
});
```

In order to assign custom functions, you need to use the global function `videsk` as follows:

```javascript
document.addEventListener('videsk-load', () => {
  videsk.events = {
    onToggle: function (){},
    onQueued: function (){},
  };
});
```

{% hint style="info" %}
You can access the global variable either with `window.videsk` or `videsk`.
{% endhint %}

* onToggle $$f$$&#x20;
* onFullToggle $$f$$&#x20;
* onSelected $$f$$
* onUnavailable $$f$$
* onQueued $$f$$
* onQueueUpdated $$f$$
* onQueueAbandoned $$f$$
* onDismissed $$f$$
* onStart $$f$$&#x20;
* onEnd $$f$$&#x20;
* onSurvey $$f$$&#x20;
* onReconnected $$f$$
* onConnectionError $$f$$&#x20;

{% hint style="info" %}
We keep backward compatibility for setting events with `videsk.events.onEventName = () => {}`.
{% endhint %}

## onToggle

This event allows you to listen when the Videsk visibility event is triggered, either because a customer clicked the floating bubble or it was executed using the API function `videsk.toggle()`.

The event will return the visibility state of the widget as a `boolean` `true` or `false` and the date it was triggered in `datetime` format.

```javascript
videsk.addEventListener('onToggle', ({ status, date }) => {
    // Do something here with status and date
});
```

## onFullToggle

This event allows you to listen when the visibility event is triggered for both the bubble and the body of the widget.

{% hint style="info" %}
This event is usually triggered by parameters present in the URL. It is different from the `onToggle` event which only indicates when it opens, unlike this one which indicates the opening and visibility.
{% endhint %}

```javascript
videsk.addEventListener('onToggle', ({ status, date }) => {
    // Do something here with status and date
});
```

## onSelected

This event allows you to listen when the customer has selected a segment.

The event will return the name of the segment as a `string`, the availability of agents in the segment as a `boolean`, and the date it was made as `datetime`.

{% hint style="info" %}
This event can be used to redirect to a message by WhatsApp or another channel if **no** agents are available.
{% endhint %}

{% hint style="warning" %}
You will need to choose between a contact form or performing an action with this event.
{% endhint %}

```javascript
videsk.addEventListener('onSelected', ({ name, available, date }) => {
    // Do something here with name of segment, availability and date
});
```

## onUnavailable

This event allows you to listen when someone tried to make a call and there are no agents connected.

```javascript
videsk.addEventListener('onUnavailable', () => {
    // Do something
});
```

## onQueued

This event allows you to listen when the customer has been added to the virtual queue.

The event will return the customer's position in the waiting line as a `number` and the date as `datetime`.

```javascript
videsk.addEventListener('onQueued', ({ position, date }) => {
    // Do something here with position and date
});
```

## onQueueUpdated

This event allows you to listen when the customer's position has been updated.

The event will return the customer's updated position in the line as a `number` and the date as `datetime`.

```javascript
videsk.addEventListener('onQueueUpdated', ({ position, date }) => {
    // Do something here with position and date
});
```

## onQueueAbandoned

This event allows you to listen when the customer has abandoned the call during the virtual queue.

{% hint style="danger" %}
This event is not related to when the call ends or starts. This event only happens if the customer clicks the cancel button or executes the function to abandon the waiting.
{% endhint %}

The event will return the date the action to abandon the queue was executed as `datetime`.

```javascript
videsk.addEventListener('onQueueAbandoned', ({ date }) => {
    // Do something with date
});
```

## onDismissed

This event allows you to listen when an agent rejects a call.

The event will return the date the action to reject was executed as `datetime`.

```javascript
videsk.addEventListener('onDismissed', ({ date }) => {
    // Do something with date
});
```

## onStart

This event allows you to listen when the customer enters the video call, that is, an agent has answered the call and the customer enters the video call.

The event will return the date as `datetime` when it happened.

```javascript
videsk.addEventListener('onStart', ({ date }) => {
    // Do something with date
});
```

## onEnd

This event allows you to listen when the customer ends the video call, that is, it ends when clicking on hang up or the agent ends the call.

The event will return the date as `datetime` when it happened.

```javascript
videsk.addEventListener('onEnd', ({ date }) => {
    // Do someting with date
});
```

## onSurvey

This event allows you to listen when the customer sends the survey after finishing a call.

{% hint style="info" %}
This event will depend on whether you have enabled the survey option at the end of a call.
{% endhint %}

The event will return two arguments, the first one corresponds to an `object` with the survey and the second one with the date it was sent as `datetime`.

```javascript
videsk.addEventListener('onSurvey', ({ survey, date }) => {
    // Do something with survey and date
});
```

## onReconnected

This event allows you to listen when it has reconnected to an active call, either because the browser/mobile app window was reloaded or closed.

{% hint style="info" %}
This event will depend on whether the widget loads with your site.
{% endhint %}

The event will return the date it reconnected as `datetime`.

```javascript
videsk.addEventListener('onReconnected', ({ date }) => {
    // Do something with survey and date
});
```

## onConnectionError

This event allows you to listen when there are connection errors before the call.

{% hint style="info" %}
It may happen that our servers detect that a user is connecting from a suspicious network or equipment, performing a block.
{% endhint %}

The event will return the date the connection error was generated as `datetime`.

```javascript
videsk.addEventListener('onConnectionError', ({ date }) => {
    // Do something with survey and date
});
```

## custom-event

This event is triggered when a segment has been configured as an event, which contains a payload as `Array` that will depend on the values entered, which will always be `String`.

```javascript
document.addEventListener('custom-event', event => {
    const args = event.detail;
    // Do something with values as String
})
```