# Methods

With the methods of our `WebRTC` component, you can change the behavior of certain elements and connections.

## `join`

{% hint style="info" %}
This method is asynchronous.
{% endhint %}

This method gets access to the camera and/or microphone and then adds the tracks as a participant.

It receives a single optional argument, which corresponds to the restrictions (`constraints`):

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').join(constraints);
```

## `camera`

This method gets access to the camera and microphone and returns a stream (`MediaStream`).

Receives a single optional argument corresponding to the restrictions (`constraints`). By default, the value is `{ audio: true, video: true }`.

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').camera(constraints);
```

## `display`

This method gets access to the screen sharing feature and returns a stream (`MediaStream`).

Receives a single argument corresponding to the restrictions (`constraints`):

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').display(constraints);
```

## `devices`

This method gets the list of available devices such as camera, microphone, and speaker.

Doesn't receive any arguments.

{% hint style="info" %}
You can use this method to find a particular device or create a selectable list.
{% endhint %}

```javascript
await document.querySelector('videsk-webrtc').devices();
```

## `changeStream`

This method changes the current stream for a new one, replacing the existing one. It receives a single argument corresponding to a `MediaStream`. Additionally, it will do the work of changing the track locally and over the network.

{% hint style="danger" %}
You cannot use this method to change the local stream if there are no participants connected yet.
{% endhint %}

{% hint style="info" %}
We suggest that you use the [`camera`](methods.md#camera) or [`display`](methods.md#display) methods to get a new `MediaStream`.
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').changeStream(stream);
```