# Events

## `connected`

This event is triggered when `BeamPort` has connected to our WebSocket API.

{% hint style="warning" %}
This **does not mean it's ready to send files**, so you should always check that `BeamPort.ports` is greater than zero before using the [`send`](methods.md#send) method.
{% endhint %}

```javascript
port.addEventListener('connected', () => {
    console.log('Ready to transfer?', port.ports > 0);
});
```

## `disconnected`

This event is triggered when `BeamPort` has disconnected from our WebSocket API, which is equivalent to losing connection with the `BeamPort` peers.

{% hint style="info" %}
It does not require manual reconnection since `BeamPort` will attempt to reconnect automatically only if it has not been disconnected using the [`disconnect`](methods.md#disconnect) method.
{% endhint %}

```javascript
port.addEventListener('disconnected', () => {
    // Do something
});
```

## `user:disconnected`

This event is triggered when a `BeamPort` peer disconnects, but the local connection remains intact.

```javascript
port.addEventListener('user:disconnected', () => {
    console.log('Connected Ports', port.ports);
});
```

## `ports`

This event is triggered when a new `BeamPort` peer has connected.

```javascript
port.addEventListener('ports', () => {
    console.log('Connected Ports', port.ports);
});
```

## `description`

This event is triggered when the information about a new file to be sent is received. The received value is a [`BeamPortFile`](beamportfile.md).

{% hint style="info" %}
Note that the content in bytes is 0 since no information has been received yet.
{% endhint %}

```javascript
port.addEventListener('description', event => {
    const file = event.detail;
});
```

## `attached`

This event is triggered when the [`send`](methods.md#send) method is called.

```javascript
port.addEventListener('attached', event => {
    const { crc32 } = event.detail;
});
```

## `progress`

This event is triggered when bytes of the file are being transferred during sending or receiving.

For **sending**, you will receive an `Object` in `event.detail` with:

* `percentage`: the percentage as a `Number` of the sending progress.
* `crc32`: CRC-32 of the sent chunk, **not of the entire file**.

For **receiving**[^1], you will receive a [`BeamPortFile`](beamportfile.md) in `event.detail`.

```javascript
port.addEventListener('progress', event => {
    const data = event.detail;
    // Sending: { percentage: Number, crc32: Number }
    // Receiving: BeamPortFile
});
```

## `canceled`

This event is triggered when a file is canceled[^2], either during or after sending/receiving.

```javascript
port.addEventListener('canceled', event => {
    const { crc32 } = event.detail;
    // Do something
});
```

## `received`

This event is triggered when a file has been received [**in its entirety**](#user-content-fn-3)[^3] from the remote peer. The received value corresponds to a [`BeamPortFile`](beamportfile.md).

```javascript
port.addEventListener('received', event => {
    const file = event.detail;
});
```

## `state`

This event is triggered when a state of the file being sent is received. The values are:

* `state`: corresponds to one of the static properties of `BeamPort`.
* `crc32`: the total integrity value of the file.

```javascript
port.addEventListener('state', event => {
    const { state, crc32 } = event.detail;
});
```

## `state:*:*`

This dynamic named event is triggered when information about the file's state is received, either during or after sending. This event should be constructed along with the [`description`](events.md#description) or [`attached`](events.md#attached) events and the [static properties of `BeamPort`](properties.md#static-properties).

```javascript
port.addEventListener(`state:${BeamPort.DELETED}:${crc32}`, () => {
    // Do something
});
```

## `state:*:*:*`

This dynamic named event is triggered when information about the state of a file chunk being sent is received. This event should be constructed along with the [`progress`](events.md#progress) event and the [static properties of `BeamPort`](properties.md#static-properties).

```javascript
const eventName = `state:${BeamPort.RECEIVED}:${crc32File}:${crc32Chunk}`;
port.addEventListener(eventName, () => {
    // Do something
});
```

[^1]: 

[^2]: Whether canceled locally or remotely.

[^3]: All bytes of the file have been received. The percentage will be 100%.