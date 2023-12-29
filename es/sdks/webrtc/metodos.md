# Métodos

A continuación, exponemos los métodos disponibles con sus descripciones y argumentos disponibles.

### `create`

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

Este método permite crear una instancia de conexión `WebRTC` mediante un `accessToken`.

{% code lineNumbers="true" %}
```javascript
phone.addEventListener('answered', async event => {
    const { accessToken } = event;
    await webrtc.create(accessToken);
    // Do something
});
```
{% endcode %}

Este método recibe tres argumentos en el siguiente orden, siendo solo el primero obligatorio:

#### `accessToken`

Corresponde al token de conexión, el cual lo puedes obtener desde el evento [`answered`](../phone/#answered) de Phone SDK.

#### `constraints` (opcional)

Estas son las restricciones que se aplicarán al momento de obtener acceso a la cámara y/o micrófono.

{% code lineNumbers="true" %}
```javascript
const constraints = { audio: true, video: false }; // Only mic
await webrtc.create(accessToken, constraints);
```
{% endcode %}

#### `stream` (opcional)

Este argumento corresponde a un stream ([`MediaStream`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)) de cámara y/o micrófono activo. Si el stream es válido omitirá el argumento `constraints`.

{% code lineNumbers="true" %}
```javascript
const camera = await navigator.mediaDevices.getUserMedia(...);
await webrtc.create(accessToken, null, camera);
```
{% endcode %}

### `destroy`

Este método permite destruir una instancia `WebRTC`. Deberás utilizar este método en eventos que requieran crear una nueva instancia o terminada una llamada.

{% code lineNumbers="true" %}
```javascript
webrtc.destroy();
```
{% endcode %}

Este método recibe dos argumentos opcionales de tipo `boolean` donde el primero permite definir si detiene las pistas de cámara y micrófono, mientras que el segundo elimina el elemento DOM. Por defecto el valor del primer argumento es `true`, en el caso del segundo es `false`.

#### `stopCamera`

Este argumento es útil si deseas evitar detener el acceso a la cámara para disminuir el tiempo de carga en la siguiente instanciación.

{% hint style="info" %}
Este método no destruye o elimina nodo DOM `videsk-webrtc`.
{% endhint %}

### `sendMessage`

Este método permite enviar mensajes mediante el chat.

#### `message`

Recibe solo un argumento como `String` el cual será el cuerpo del mensaje.

{% code lineNumbers="true" %}
```javascript
webrtc.sendMessage('Hola, necesito ayuda!');
```
{% endcode %}

{% hint style="info" %}
Los enlaces serán resaltados automáticamente.
{% endhint %}

{% hint style="warning" %}
Por seguridad, todo texto enviado será sanitizado, por lo que caracteres HTML serán escapados de forma automática.
{% endhint %}

### `addEventListener`

Este método permite definir oyentes de eventos.

{% code lineNumbers="true" %}
```javascript
webrtc.addEventListener('hangup', () => {
    // Do something
});
```
{% endcode %}
