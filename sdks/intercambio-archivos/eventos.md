# Eventos

## `connected`

Este evento se dispara cuando se ha conectado `BeamPort` a nuestra API WebSocket.&#x20;

{% hint style="warning" %}
Esto **no significa que esté listo para enviar archivos**, por lo que siempre deberás verificar que `BeamPort.ports` tenga un valor mayor a cero antes de usar el método [`send`](metodos.md#send).
{% endhint %}

```javascript
port.addEventListener('connected', () => {
    console.log('Listo para transferir?', port.ports > 0);
});
```

## `disconnected`

Este evento se dispara cuando `BeamPort` se ha desconectado de nuestra API WebSocket, lo que es equivalente a perder conexión con los pares `BeamPort`.

{% hint style="info" %}
No requiere una reconexión manual, ya que `BeamPort` intentará reconectarse automáticamente solo si no se ha desconectado usando el método [`disconnect`](metodos.md#disconnect).
{% endhint %}

```javascript
port.addEventListener('disconnected', () => {
    // Do something
});
```

## `user:disconnected`

Este evento se dispara cuando un par `BeamPort` se desconecta, no así la conexión local.

```javascript
port.addEventListener('user:disconnected', () => {
    console.log('Ports conectados', port.ports);
});
```

## `ports`

Este evento se dispara cuando un nuevo par `BeamPort` se ha conectado.

```javascript
port.addEventListener('ports', () => {
    console.log('Ports conectados', port.ports);
});
```

## `description`

Este evento se dispara cuando se recibe la información de un nuevo archivo que se enviará a continuación. En valor a recibir es un [`BeamPortFile`](beamportfile.md).&#x20;

{% hint style="info" %}
Considera que el contenido en bytes es 0, ya que aún no se ha recibido información.
{% endhint %}

```javascript
port.addEventListener('description', event => {
    const file = event.detail;
});
```

## `attached`

Este evento se dispara cuando se llama al método [`send`](metodos.md#send).

```javascript
port.addEventListener('attached', event => {
    const { crc32 } = event.detail;
});
```

## `progress`

Este evento se dispara cuando se está transfieren bytes del archivo durante el envío o recepción.

En el caso de **envío** recibirás en `event.detail` un `Object` con:

* `percentage`: porcentaje como `Number` del envío.
* `crc32`: CRC-32 del chunk envíado, **no del archivo**.

Para el caso de [**recepción**](#user-content-fn-1)[^1] recibirás en `event.detail` un [`BeamPortFile`](beamportfile.md).

```javascript
port.addEventListener('progress', event => {
    const data = event.detail;
    // Envío: { percentage: Number, crc32: Number }
    // Recepción: BeamPortFile
});
```

## `canceled`

Este evento se dispara cuando un archivo se ha cancelado[^2], ya sea durante o después del envío/recepción.

```javascript
port.addEventListener('canceled', event => {
    const { crc32 } = event.detail;
    // Do something
});
```

## `received`

Este evento se dispara cuando se recibe un archivo [**en su totalidad**](#user-content-fn-3)[^3] enviado por el par remoto. El valor recibido corresponde a un [`BeamPortFile`](beamportfile.md).

```javascript
port.addEventListener('received', event => {
    const file = event.detail;
});
```

## `sent`

Este evento se dispara cuando se envió un archivo [en su totalidad](#user-content-fn-4)[^4], confirmado por el par remoto. Los valores son:

* `crc32`: valor de integridad total del archivo
* `filename`: nombre del archivo incluyendo extensión
* `file`: archivo de tipo [File](https://developer.mozilla.org/en-US/docs/Web/API/File)

```javascript
port.addEventListener('sent', event => {
    const { crc32, filename, file } = event.detail;
    // Do something
});
```

## `state`

Este evento se dispara cuando se recibe un estado del archivo que se está enviando. Los valores son:

* `state`: corresponde al valor de alguna de las propiedades estáticas de `BeamPort`.
* `crc32`: valor de integridad total del archivo.

```javascript
port.addEventListener('state', event => {
    const { state, crc32 } = event.detail;
});
```

## `state:*:*`

Este evento con nombre dinámico se dispara cuando se ha recibido información del estado del archivo, ya sea durante o después del envío.

Este evento se debe construir junto con los eventos [`description`](eventos.md#description) o [`attached`](eventos.md#attached), y las [propiedades estáticas de `BeamPort`](propiedades.md#propiedades-estaticas).

```javascript
port.addEventListener(`state:${BeamPort.DELETED}:${crc32}`, () => {
    // Do something
});
```

## `state:*:*:*`

Este evento con nombre dinámico se dispara cuando se recibido la información del estado de un chunk del archivo mientras se envía.

Este evento se debe construir junto con el evento [`progress`](eventos.md#progress), y las [propiedades estáticas de `BeamPort`](propiedades.md#propiedades-estaticas).

```javascript
const eventName = `state:${BeamPort.RECEIVED}:${crc32File}:${crc32Chunk}`;
port.addEventListener(eventName, () => {
    // Do something
});
```

[^1]: 

[^2]: Ya sea cancelado local o remotamente.

[^3]: Ya se han recibido todos los bytes del archivo. El porcentaje será 100%.

[^4]: Ya se han enviado todos los bytes del archivo. El porcentaje será 100%.
