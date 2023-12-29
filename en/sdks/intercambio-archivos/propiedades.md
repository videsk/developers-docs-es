# Properties

## `store`

This property contains the array of received files. It corresponds to a `Map`, therefore you will be able to access each file with the [native properties of a constructor Map](#user-content-fn-1)[^1].

The store is built using the `CRC-32` checksum as a key and the [`BeamPortFile`](beamportfile.md) as a value.

```javascript
port.store; // Map {}
// List of files
port.store.get(crc32); // Returns a BeamPortFile
```

## `connected`

This property returns a `Boolean` on the connection status.

```javascript
port.connected; // true or false
```

## `ports`

This property returns the number of connected `BeamPort` pairs as an integer. The value will usually always be `1`.

```javascript
port.ports;
```

## `connection`

This property returns the active peer connection as [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel).

```
port.connection;
```

{% hint style="info" %}
We recommend that you do not use the connection to send data without knowing as it is sent in a proprietary binary nomenclature.
{% endhint %}

## `debug`

This property returns access to the proprietary debugger mode. To use the debugger, you must set the `debug` in `localStorage` to the value `beamport`.

```javascript
localStorage.debug = 'beamport';
```

{% hint style="info" %}
Remember that activating debug mode is inefficient for production environments.
{% endhint %}

## Static properties

All static properties can be accessed directly from the `BeamPort` constructor, without the need to instantiate.

```javascript
BeamPort.DESCRIPTION
BeamPort.RECEIVED
BeamPort.FAILED
```

### `DESCRIPTION`

Its value is equal to the number `1`.

### `CHUNK`

Its value is equal to the number `2`.

### `STATE`

Its value is equal to the number `3`.

### `EXCHANGED`

Its value is equal to the number `4`.

### `RECEIVED`

Its value is equal to the number `5`.

### `FAILED`

Its value is equal to the number `6`.

### `DELETED`

Its value is equal to the number `7`.

[^1]: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map)