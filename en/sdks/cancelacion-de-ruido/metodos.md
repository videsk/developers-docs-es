# Methods

## `enable`

This method enables noise cancellation. You should provide a single argument, which corresponds to the media (`MediaStream`) containing at least one audio track, unless you have previously disabled it.

[REPLACE_CODE_FORMAT hint style="info" [REPLACE_CODE_FORMAT]
To obtain a MediaStream, we recommend using the [`camera`](../../components-web/webrtc/methods.md#camera) method of our WebRTC component.
[REPLACE_CODE_FORMAT endhint [REPLACE_CODE_FORMAT]

[REPLACE_CODE_FORMAT hint style="warning" [REPLACE_CODE_FORMAT]
This method is asynchronous.
[REPLACE_CODE_FORMAT endhint [REPLACE_CODE_FORMAT]

```javascript
const streamFiltered = await suppression.enable(stream);
```

The return value corresponds to a `MediaStream` with the audio track activated with noise cancellation.

Subsequently, you should use our WebRTC. For example, when [creating an instance](../webrtc/methods.md#create) of WebRTC, you should provide as the last argument the MediaStream with noise cancellation.

```javascript
const streamFiltered = await suppression.enable(stream);
webrtc.create(accessToken, null, streamFiltered);
```

## `disable`

This method deactivates noise cancellation.

```javascript
suppression.disable();
```

If you want to re-enable noise cancellation, you only need to use the [`enable`](methods.md#enable) method again, without the need to provide the `MediaStream` argument.