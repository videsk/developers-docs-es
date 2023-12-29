# Events

The following events let you listen for specific behaviors in order to change your UI or other behavior.

As a general rule, every event returns an event like `CustomEvent.`

```javascript
webrtc.addEventListener('hangup', event => {
const { ... } = event.detail;
});
```

{% hint style="info" %}
We suggest you to destructure every event from `event.detail`.
{% endhint %}

Additionally, some of the following events are cancelable, which means that you can override the default behavior by using `event.preventDefault()`.

## `media:status`

This event emits the status of the video and audio of every participant every time it gets modified.

```javascript
webrtc.addEventListener('media:status', event => {
const { video, audio, remote, stream, node, participant, peer } = event.detail;
// Do something
});
```

The available values are:

| Name          | Type           | Description                                  |
|---------------|----------------|----------------------------------------------|
| `video`       | `Boolean`      | State of the video                           |
| `audio`       | `Boolean`      | State of the audio                           |
| `remote`      | `Boolean`      | If it corresponds to a remote or local state |
| `stream`      | `MediaStream`  | Stream of the remote or local media          |
| `node`        | `HTMLNode`     | HTML node of the participant                 |
| `participant` | `String`       | ID of the remote or local participant        |
| `peer`        | `Peer`         | `Peer` constructor                           |

## `media:error`

This event is emitted when an error occurs while trying to access the camera, microphone, or screen.

{% hint style="info" %}
Errors commonly happen when camera, microphone or screen sharing are denied.
{% endhint %}

```javascript
webrtc.addEventListener('media:error', event => {
const { error, camera, screen } = event.detail;
// Do something
});
```

The available values are:

| Name      | Type      | Description                            |
|-----------|-----------|----------------------------------------|
| `error`   | `Error`   | The error itself                       |
| `camera`  | `Boolean` | Indicates if it's a camera error       |
| `screen`  | `Boolean` | Indicates if it's a screen share error |

## `participant`

This event is emitted when a participant is added or removed from the webrtc component.

```javascript
webrtc.addEventListener('participant', event => {
const { action, participant, peer, stream } = event.detail;
// Do something
});
```

| Name          | Type          | Description                                                    |
|---------------|---------------|----------------------------------------------------------------|
| `action`      | `String`      | Indicates the action which can be either `added` or `removed`. |
| `participant` | `HTMLNode`    | HTML Node of the participant                                   |
| `peer`        | `Peer`        | `Peer` constructor                                             |
| `stream`      | `MediaStream` | Stream of the participant                                      |

## `participants-toggle`

This event is emitted when the participants are going to be visible or not in the `sidebar` mode.

{% hint style="info" %}
This event is cancelable.
{% endhint %}

```javascript
webrtc.addEventListener('participants-toggle', event => {
const { status } = event.detail;
// Custom code
});
```

| Name     | Type      | Description                                         |
|----------|-----------|-----------------------------------------------------|
| `status` | `Boolean` | Current status of the participants (visible or not) |