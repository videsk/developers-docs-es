# Methods

## `connect`

You must use this asynchronous method[^1] to connect to another `BeamPort`, by providing an `accessToken` that you can obtain from the `beamport:create` event of `Phone SDK`.

```javascript
await port.connect(accessToken);
```

## `send`

This asynchronous method allows you to automatically send files to the other `BeamPort`. The arguments received by this method are:

1. `input`: File as `File`, `ArrayBuffer` or `Blob`.
2. `mimeType`: MIME of the file, optional if `input` is of type `File`.
3. `id`: File ID, optional.

```javascript
// File
await port.send(myFile);
// ArrayBuffer or Blob
await port.send(myBuffer, 'application/msword');
```

We recommend using our file transfer web component, or you can use a `input` of type `file`, listening for the `change` event](#user-content-fn-2)[^2].

#### `send` method considerations

If you want to attach multiple files, you will need to iterate over the files:

```javascript
files.forEach(file => port.send(file));
```

In case you send a `ArrayBuffer` or `Blob`, you must specify the `id` and `mimeType`.

```javascript
await port.send(myBlob, 'image/png', 'my-unique-id');
```

{% hint style="warning" %}
If you **don't** specify a MIME type for a file as `ArrayBuffer` or `Blob`, it will not be readable for the agent.
{% endhint %}

## `cancel`

This method allows you to cancel the sending of the current file or remove the file access to the remote `BeamPort`.

You must provide the same file sent as `File`, `ArrayBuffer` or `Blob` as the only argument.

```javascript
await port.cancel(myFile);
```

## `disconnect`

With this method you will stop the BeamPort connection entirely, so you will need to create a new one if you need it.

```javascript
port.disconnect();
```

## `addEventListener`

You can listen to the events through an attached listener. You can add all the events you need for the same or different.

```javascript
port.addEventListener('eventName', event => {
const eventData = event.detail;
// Do something
});
```

## `getFile`

With this method you will be able to get the file using the CRC-32 value as a unique argument and `String`. The returned value will be a `BeamPortFile`.

```javascript
port.getFile(crc32);
```

{% hint style="info" %}
`BeamPort` **doesn't** store the files sent, only the ones received. You can get the list of received files from the `store` property.
{% endhint %}

[^1]: This method is asynchronous

[^2]: [https://developer.mozilla.org/en-US/docs/Web/API/File\_API/Using\_files\_from\_web\_applications](https://developer.mozilla.org/en-US/docs/Web/API/File\_API/Using\_files\_from\_web\_applications)
