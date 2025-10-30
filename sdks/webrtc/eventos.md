# Eventos

A continuación, exponemos los eventos disponibles con sus descripciones y argumentos.



## `media-status`&#x20;

Este evento emite el estado de medios del participante remoto.

```javascript
webrtc.addEventListener('media-status', event => {
    const { screen, stream, audio, video, peer } = event.detail;
    // Do something
});
```

| Nombre   | Tipo      | Descripción                                          |
| -------- | --------- | ---------------------------------------------------- |
| `screen` | `Boolean` | Estado de compartir pantalla del participante remoto |
| `video`  | `Boolean` | Estado del video del participante remoto             |
| `audio`  | `Boolean` | Estado del audio del participante remoto             |
| `stream` | `String`  | ID del stream de la pantalla compartida              |
| `peer`   | `String`  | ID del participante                                  |

## `new-message`&#x20;

Este evento se emite al recibir un mensaje a través del chat o [sendMessage](metodos.md#sendmessage) en el participante remoto.

```javascript
webrtc.addEventListener('new-message', event => {
    const { audio, video, peer, direction, description, candidate } = event.detail;
    // Do something
});
```

| Nombre      | Tipo    | Descripción                                                                                                  |
| ----------- | ------- | ------------------------------------------------------------------------------------------------------------ |
| audio       | Boolean | Audio del participante remoto                                                                                |
| video       | Boolean | Video del participante remoto                                                                                |
| direction   | String  | [Dirección RTCRtpTransceiver ](https://developer.mozilla.org/en-US/docs/Web/API/RTCRtpTransceiver/direction) |
| peer        | String  | ID del participante                                                                                          |
| description | Object  | [RTCSessionDescription](https://developer.mozilla.org/en-US/docs/Web/API/RTCSessionDescription)              |
| candidate   | Object  | [RTCIceCandidate](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceCandidate)                          |

## `peer:disconnect`

Este evento se dispara cuando el participante remoto se ha desconectado.

```javascript
webrtc.addEventListener('peer:disconnect', event => {
    const { peer } = event.detail;
    // Do something
});
```

| Nombre | Tipo   | Descripción                |
| ------ | ------ | -------------------------- |
| peer   | String | ID del participante remoto |

## `disconnected`

Este evento se dispara cuando se ha desconectado localmente del servidor (no el participante remoto).

```javascript
webrtc.addEventListener('disconnected', () => {
    // Do something
});
```

## `stats`&#x20;

Este evento se dispara cada 5 segundos entregando información técnica sobre el estado de conexión WebRTC. Puedes ver más detalles a continuación:

```javascript
webrtc.addEventListener('stats', event => {
    const stats = event.detail;
    // Do something
});
```

{% content-ref url="stats.md" %}
[stats.md](stats.md)
{% endcontent-ref %}

## `error`

Este evento se dispara cuando se encuentra un error al establecer y durante la conexión.

```javascript
webrtc.addEventListener('error', event => {
    const { code, errors, message, name, originalEvent } = event.detail;
    // Do something
});
```

| Nombre        | Tipo   | Descripción                                               |
| ------------- | ------ | --------------------------------------------------------- |
| code          | Number | Código de error. Detalles aquí.                           |
| name          | String | Nombre del error                                          |
| message       | String | Detalles del error                                        |
| errors        | Array  | Listado de errores con detalles estructurados.            |
| originalEvent | String | Evento original (despachado desde cliente hacia servidor) |

## Errores

Los posibles errores se listan a continuación, identificados mediante códigos de estado.

{% hint style="info" %}
Se recomienda utilizar nuestros códigos numéricos para comportamientos condicionales.
{% endhint %}

### `4401`

Este error se debe a que el token de acceso presente un error de validación ya sea por:

```javascript
const tokenErrors = {
    'jwt malformed': 'Acceso no autorizado',
    'invalid signature': 'Acceso no autorizado',
    'jwt expired': 'Sesión ha expirado',
    'jwt not active': 'Acceso anticipado no autorizado'
};

webrtc.addEventListener('error', event => {
    const { message } = event.detail;
    showMessage(tokenErrors[message]);
});
```

| Mensaje           | Descripción                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| jwt malformed     | Token de acceso malformado                                              |
| invalid signature | Token utilizado no es válido                                            |
| jwt expired       | Token de acceso expirado                                                |
| jwt not active    | Se ha utilizado el token de acceso con anticipación a la fecha correcta |

## `4403`

Este error, poco común, solo se recibirá en caso de enviar mensajes nativos de WebSocket con un formato malformado o de intentos de inyección.
