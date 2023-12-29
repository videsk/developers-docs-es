# Properties

With our `WebRTC` properties you can change the behavior of certain elements and connections.

### `video`

This read and write property allows you to modify the local video state, on `true` or off `false`.

{% hint style="info" %}
If you start with no camera track (only microphone), and then change the value to `true` it will trigger a new stream (camera and microphone).
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').video = true;
document.querySelector('videsk-webrtc').video // true
```

### `audio`

This read and write property allows you to modify the local audio status, on `true` or off `false`.

```javascript
document.querySelector('videsk-webrtc').audio = true;
document.querySelector('videsk-webrtc').audio // true
```

### `layout`

This read and write property allows you to modify the design of the WebRTC. Accepted values are `sidebar` and `grid`.

```javascript
document.querySelector('videsk-webrtc').layout = 'sidebar';
```

This property can also be set using attributes in the element. By default, if the `sidebar` attribute is not present, the value of the `layout` property will be `grid`. Any change made using the `layout` property will be reflected as an attribute and vice versa.

```html
<videsk-webrtc sidebar></videsk-webrtc>
```

### `chat`

This read and write property allows you to show `true` and hide `false` the chat.

```javascript
document.querySelector('videsk-webrtc').chat = true;
document.querySelector('videsk-webrtc').chat; // true
```

### `peers`

This property is read-only, returns a list of peer connections as a [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map).

{% hint style="warning" %}
If you use our SDK, do not override the `Map` value, by default.
{% endhint %}

{% hint style="info" %}
Interacting with peer connections requires advanced knowledge of WebRTC.
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').peers
```

### `isConnectedWithPeer`

This read-only property returns a `boolean` if there is at least one active peer connection.

```javascript
document.querySelector('videsk-webrtc').isConnectedWithPeer
```

### `sharingScreen`

This read-only property returns a `boolean` with the screen sharing status.

```javascript
document.querySelector('videsk-webrtc').sharingScreen
```

### `defaultConstraints`

This read-only property returns an `object` with the default camera constraints.

```javascript
{
  video: { facingMode: { ideal: 'user' } },
  audio: true,
}
```