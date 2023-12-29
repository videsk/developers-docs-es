# Events

The Phone SDK has a list of events that will help you run actions on the HTML. You will need to listen to them using functions to make interface changes.

{% @figma/embed fileId="ZgAVJ4UIU5hHN9F0sXWNG7" nodeId="0:1" url="https://www.figma.com/file/ZgAVJ4UIU5hHN9F0sXWNG7/Widget-workflow?node-id=0%3A1" %}

To use the events, you will need to do the following:

{% tabs %}
{% tab title="Listener (Recommended)" %}
```javascript
const phone = new VideskPhone(APIToken);
phone.listen('no-agents', () => {});
```
{% endtab %}

{% tab title="Alternative 1" %}
```javascript
const events = { ... };
const phone = new VideskPhone(APIToken, events);
```
{% endtab %}

{% tab title="Alternative 2" %}
```javascript
const phone = new VideskPhone(APIToken);
phone.on['no-agents'] = () => {};
```
{% endtab %}

{% tab title="Alternative 3" %}
```javascript
onst phone = new VideskPhone(APIToken);
phone.on = { ... };
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
The following **events with \* (asterisk) are required and mandatory**, if you do not listen to them appropriately the behavior of the SDK will not be as expected.
{% endhint %}

## `token-error`

This event will be emitted when the provided token is incorrect, malformed, or invalid. This could eventually happen if an account administrator removes the integration from the account.

{% hint style="info" %}
This should be listened to, only in case of development environment.
{% endhint %}

```javascript
phone.on['token-error'] = () => {
// Verify token
};
```

## `no-agents`\*

This event will be emitted when there are no agents connected to your account after attempting the call using the `phone.call()` method.

```javascript
phone.on['no-agents'] = () => {
// Display a message that no agents are available
};
```

## `queued`\*

This event is emitted when the customer has been added to the waiting queue, after calling the `phone.call()` method.

```javascript
phone.on['queued'] = (event) => {
const { position, avgWait, segment } = event;
// Show an interface that allows visualizing the position and/or waiting time.
};
```

{% hint style="warning" %}
The position and/or waiting time may be disabled by the account administrator.
{% endhint %}

{% hint style="info" %}
The waiting time is in minutes, so we suggest you use [our open source library](https://github.com/videsk/humanize-date) that "humanizes" the time unit, to display it in seconds, minutes, hours, etc. depending on the value.

Example:

If the returned waiting time is 0.5 minutes, then our library will return 30 seconds.
{% endhint %}

## `queue-updated`\*

This event will be emitted when the position in the queue is updated, only after the `queued` event. **It is extremely important that you listen to this event.**

```javascript
phone.on['queue-updated'] = (event) = {
const { position } = event;
// Update position in queue
};
```

## `customer-leave`\*

This event will be emitted when the `phone.leave()` event is executed while in the waiting queue.

```javascript
phone.on['customer-leave'] = () => {
// Show a message of abandonment of row
};
```

## `dismissed`\*

This event will be emitted when an agent rejects the call.

```javascript
phone.on['dismissed'] = () => {
// Show a rejected call message
};
```

## `out-queue`

This event is emitted when the call has been answered by an agent. **It is optional to listen to this event**.

```javascript
phone.on['out-queue'] = () => {
// No need to modify anything
};
```

## `answered`\*

This event is emitted when the call has been answered by an agent.

```javascript
phone.on['answered'] = (event) => {
const { call } = event;
// You should use our WebRTC SDK
let webrtc = new VideskWebRTCSDK(call, events, options);
webrtc.create();
};
```

{% hint style="info" %}
Remember that you will need to load our WebRTC in advance. For more information visit the [WebRTC SDK](../webrtc/) documentation.
{% endhint %}

## `connected-call`

This event is emitted when the call has been successfully connected. **It is optional to listen to this event**.

```javascript
phone.on['connected-call'] = () => {
// No need to modify anything
};
```

## `agent-disconnect`

This event is emitted when the agent who answered the call eventually disconnects from the video call due to network problems. **It is optional to listen to this event**.

{% hint style="warning" %}
You should not end the call, as the agent will automatically reconnect. In case of exceeding several minutes, our API will automatically end the call.
{% endhint %}

```javascript
phone.on['agent-disconnect'] = () => {
// Show a disconnected agent message
};
```

## `customer-hangup`

This event is emitted when the `phone.hangup()` method is executed. **It is optional to listen to this event.**

```javascript
phone.on['customer-hangup'] = () => {
// Display a call ended message
};
```

## `ended`\*

This event is emitted when the call ends, either on the agent's side or when executing the `phone.hangup()` method.

```javascript
phone.on['ended'] = () => {
// Display a call ended message
webrtc.destroy();
};
```

{% hint style="warning" %}
You must delete the created WebRTC instance, using the `destroy()` method.
{% endhint %}

## `transferred-segment`\*

This event will be emitted when an agent has transferred the customer to a new segment.

```javascript
phone.on['transferred-segment'] = (event) => {
const { queue } = event;
// Display a message, you should not do anything with the connections
};
```

{% hint style="info" %}
The SDK will make the connections automatically, starting the cycle from the `queued` event, therefore, you only need to make sure it is being listened to.
{% endhint %}

## `transferred-agent`\*

This event will be emitted when an agent has transferred the customer to a specific agent.

```javascript
phone.on['transferred-agent']= (event) => {
const { call } = event;
// You will need to create a new instance of WebRTC SDK and destroy the old one
webrtc.destroy();
webrtc = new new VideskWebRTCSDK(call, events, options);
webrtc.create();
};
```

## `connection-error`

This event will be emitted when there is any error in the network or malformed parameters that were sent to the API. **It is optional to listen to this event**.

```javascript
phone.on['connection-error'] = (event) => {
const { event, code, name, message, date, errors } = event;
}
```

## `network-issues`\*

This event will be emitted when there are network problems, such as disconnection from the Internet or too many reconnections due to an unreliable network.

```javascript
phone.on['network-issues'] = () => {
// Display unstable network message
};
```

{% hint style="info" %}
Our API has an algorithm that will identify a potential client with an unstable network, which will cause a connection to be rejected in the waiting queue.

This is because the network required for the connection in the waiting queue is minimal, it concludes that the customer's network will not support a stable video call connection.

**The evaluated parameter is not the speed, but the stability of the network.**
{% endhint %}

## `http-block`

This event will be emitted when our API detects suspicious activity such as a bot or a call from an untrusted network. **It is optional to listen to this event**.

{% hint style="info" %}
This type of behavior is not configurable, which allows us to deliver a better quality of service to all our customers by blocking potential attackers or bots.
{% endhint %}

```javascript
phone.on['http-block'] = () => {
// Display an insecure network message
};
```

## `transport-disconnect`

This event is emitted when our API automatically disconnects the connection either in the waiting queue or when the call ends. In other words, this event will naturally be emitted twice in a normal call. **It is optional to listen to this event**.

```javascript
phone.on['transport-disconnect'] = () => {
// Internal use
};
```

## Limits and uses

{% hint style="danger" %}
Do not create more than one instance of `VideskPhone`, as you could generate multiple calls. This will affect the reports and you could have your account suspended for suspicious behavior.
{% endhint %}

This SDK will allow you to integrate Videsk in multiple environments, whether it's a website, mobile application using web frameworks, kiosks, IoT, etc.

**For integrations on iOS and Android apps**, we suggest using [Custom Tabs](https://developer.chrome.com/docs/android/custom-tabs/) for Android and [Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) for iOS.

These web frameworks (Custom Tabs and Safari View Controller) will offer maximum compatibility for video calls. Other frameworks such as WebView for Android and iOS are supported but you could experience certain active bugs in this type of integration.

{% hint style="info" %}
In case of bugs you can send us an email at [developers@videsk.io](mailto:developers@videsk.io) or from your dashboard.
{% endhint %}
