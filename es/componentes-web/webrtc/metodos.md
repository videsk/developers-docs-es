# Métodos

Con los métodos de nuestro componente `WebRTC` podrás cambiar el comportamiento de ciertos elementos y conexiones.

## `join`

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

Este método obtiene acceso a la cámara y/o micrófono para posteriormente añadir las pistas como participante.

Recibe un solo argumento opcional, que corresponde a las restricciones (`constraints`):

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').join(constraints);
```

## `camera`

Este método obtiene acceso a la cámara y micrófono y retorna un stream (`MediaStream`).

Recibe un solo argumento opcional que corresponde a las restricciones (`constraints`). Por defecto el valor es `{ audio: true, video: true }`.

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').camera(constraints);
```

## `display`

Este método obtiene acceso a la función de compartir pantalla y retorna un stream (`MediaStream`).

Recibe un solo argumento que corresponde a las restricciones (`constraints`):

```javascript
const constraints = { audio: true, video: true };
await document.querySelector('videsk-webrtc').display(constraints);
```

## `devices`

Este método obtiene el listado de dispositivos disponibles como cámara, micrófono y altavoz.

No recibe ningún argumento.

{% hint style="info" %}
Podrás usar este método para encontrar un dispositivo en particular o crear una lista seleccionable.
{% endhint %}

```javascript
await document.querySelector('videsk-webrtc').devices();
```

## `changeStream`

Este método cambia el stream actual por uno nuevo reemplazando el existente. Recibe un único argumento el cual corresponde a un `MediaStream`. Adicionalmente, realizará el trabajo de cambiar la pista a nivel local y de red.

{% hint style="danger" %}
No puedes usar este método para cambiar el stream local si aún no hay participantes conectados.
{% endhint %}

{% hint style="info" %}
Te sugerimos utilizar el método [`camera`](metodos.md#camera) o [`display`](metodos.md#display) para obtener un nuevo `MediaStream`.
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').changeStream(stream);
```
