# Eventos

Los siguientes eventos te permiten detectar ciertos comportamientos para realizar cambios en interfaz u otros comportamientos.

Como regla general, todos los eventos retornan un evento como `CustomEvent.`

```javascript
webrtc.addEventListener('hangup', event => {
    const { ... } = event.detail;
});
```

{% hint style="info" %}
Te sugerimos desectructurar cada evento desde `event.detail`.
{% endhint %}

## `media:status`

Este evento emite el estado del video y audio de cada uno de los participantes cada vez que sea modificado.

```javascript
webrtc.addEventListener('media:status', event => {
    const { video, audio, remote, stream, node, participant, peer } = event.detail;
    // Do something
});
```

Los valores disponibles son:

| Nombre        | Tipo          | Descripción                               |
| ------------- | ------------- | ----------------------------------------- |
| `video`       | `Boolean`     | Estado del video                          |
| `audio`       | `Boolean`     | Estado del audio                          |
| `remote`      | `Boolean`     | Si corresponde a un estado remoto o local |
| `stream`      | `MediaStream` | Stream del medio remoto o local           |
| `node`        | `HTMLNode`    | Nodo HTML del participante                |
| `participant` | `String`      | ID del participante remoto o llocal       |
| `peer`        | `Peer`        | Constructor `Peer`                        |

## `media:error`

Este evento se emite cuando ocurre un error al intentar obtener acceso a la cámara, micrófono o pantalla.

{% hint style="info" %}
Los errores comúnmente ocurren cuando se deniega el acceso a la cámara, micrófono o al compartir pantalla.
{% endhint %}

```javascript
webrtc.addEventListener('media:error', event => {
    const { error, camera, screen } = event.detail;
    // Do something
});
```

Los valores disponibles son:

| Nombre   | Tipo      | Descripción                              |
| -------- | --------- | ---------------------------------------- |
| `error`  | `Error`   | Corresponde al error                     |
| `camera` | `Boolean` | Indica si es error de cámara             |
| `screen` | `Boolean` | Indica si es error al compartir pantalla |

## `participant`

Este evento se emite cuando se añade o elimina un participante del componente web.

```javascript
webrtc.addEventListener('participant', event => {
    const { action, participant, peer, stream } = event.detail;
    // Do something
});
```

| Nombre        | Tipo          | Descripción                                          |
| ------------- | ------------- | ---------------------------------------------------- |
| `action`      | `String`      | Indica acción el cual puede ser `added` o `removed`. |
| `participant` | `HTMLNode`    | Nodo HTML del participante                           |
| `peer`        | `Peer`        | Constructor `Peer`                                   |
| `stream`      | `MediaStream` | Stream de participante                               |
