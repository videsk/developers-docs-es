# Methods

Below, we expose the available methods with their descriptions and arguments available.

### `create`

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

This method allow you to create a `WebRTC` connection instance by using `accessToken`.

{% code lineNumbers="true" %}
```javascript
phone.addEventListener('answered', async event => {
const { accessToken } = event;
await webrtc.create(accessToken);
// Do something
});
```
{% endcode %}

This method receives three arguments in the following order, being only the first one mandatory:

#### `accessToken`

Corresponds to the connection token, which you can get from the Phone SDK [`answered`](../phone/#answered) event.

#### `constraints` (optional)

These are the constraints that will be applied when getting access to the camera and/or microphone.

{% code lineNumbers="true" %}
```javascript
const constraints = { audio: true, video: false }; // Only mic
await webrtc.create(accessToken, constraints);
```
{% endcode %}

#### `stream` (optional)

This argument corresponds to an active camera and/or microphone stream ([`MediaStream`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)). If the stream is valid, it will ignore the `constraints` argument.

{% code lineNumbers="true" %}
```javascript
const camera = await navigator.mediaDevices.getUserMedia(...);
await webrtc.create(accessToken, null, camera);
```
{% endcode %}

### `destroy`

This method allows to destroy a `WebRTC` instance. You should use this method in events that require creating a new instance or ending a call.

{% code lineNumbers="true" %}
```javascript
webrtc.destroy();
```
{% endcode %}

This method receives two optional arguments of type `boolean` where the first one allows to define if it stops the camera and microphone tracks, while the second one removes the DOM element. By default the value of the first argument is `true`, in the case of the second one is `false`.

#### `stopCamera`

This argument is useful if you want to avoid stopping the access to the camera to reduce the load time in the next instantiation.

{% hint style="info" %}
This method does not destroy or delete DOM node `videsk-webrtc`.
{% endhint %}

### `sendMessage`

This method allows to send messages through the chat.

#### `message`

Receive only one argument as a `String` which will be the body of the message.

{% code lineNumbers="true" %}
```javascript
webrtc.sendMessage('Hi, I need help!');
```
{% endcode %}

{% hint style="info" %}
Links will be highlighted automatically.
{% endhint %}

{% hint style="warning" %}
For security, all text sent will be sanitized, so HTML characters will be automatically escaped.
{% endhint %}

### `addEventListener`

This method allows to define event listeners.

{% code lineNumbers="true" %}
```javascript
webrtc.addEventListener('hangup', () => {
// Do something
});
```
{% endcode %}