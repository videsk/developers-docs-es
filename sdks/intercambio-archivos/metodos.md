# Métodos

## `connect`

Debes usar este método[^1] asíncrono para realizar la conexión con otro par `BeamPort`, entregando un `accessToken` que podrás obtener desde el evento `beamport:connect` de `Phone SDK`.

```javascript
await port.connect(accessToken);
```

## `send`

Este método asíncrono te permite enviar los archivos automáticamente al otro par `BeamPort`. Los argumentos que recibe este método son:

1. `input`: Archivo como `File`, `ArrayBuffer` o `Blob`.
2. `mimeType`: MIME del archivo, opcional si `input` es de tipo `File`.
3. `id`: ID del archivo, opcional.

```javascript
// File
await port.send(myFile);
// ArrayBuffer o Blob
await port.send(myBuffer, 'application/msword');
```

Recomendamos el uso de nuestro componente web de transferencia de archivos, o bien [puedes usar un `input` de tipo `file`, escuchando el evento `change`](#user-content-fn-2)[^2].

#### Consideraciones método `send`

En caso que desees adjuntar varios archivos deberás ejecutar una iteración sobre los archivos:

```javascript
files.forEach(file => port.send(file));
```

En el caso que envíes un `ArrayBuffer` o `Blob`, deberás indicar de manera obligatoria el `id` y `mimeType`.

```javascript
await port.send(myBlob, 'image/png', 'my-unique-id');
```

{% hint style="warning" %}
Si **no** indicas un MIME type para un archivo como `ArrayBuffer` o `Blob` , no será legible para el agente.
{% endhint %}

## `cancel`

Este método permite cancelar el envío del archivo en curso o eliminar el acceso del archivo en el par `BeamPort` remoto.

Deberás entregar como único argumento el mismo archivo envíado como `File`, `ArrayBuffer` o `Blob`.

```javascript
await port.cancel(myFile);
```

## `disconnect`

Con este método detendrás la conexión BeamPort en su totalidad, por lo deberás crear una nueva si lo necesitas.

```javascript
port.disconnect();
```

## `addEventListener`

Podrás escuchar los eventos a través de un oyente adjunto. Puedes añadir todos los eventos que necesites para el mismo o diferente.

```javascript
port.addEventListener('eventName', event => {
    const eventData = event.detail;
    // Do something
});
```

## `getFile`

Con este método podrás obtener el archivo usando el valor CRC-32 como único argumento y `String`. El valor retornado será un `BeamPortFile`.

```javascript
port.getFile(crc32);
```

{% hint style="info" %}
`BeamPort` **no** almacena los archivos enviados, solo recibidos. Puedes obtener el listado de archivos recibidos desde la propiedad `store`.
{% endhint %}

[^1]: Este método es asíncrono

[^2]: [https://developer.mozilla.org/en-US/docs/Web/API/File\_API/Using\_files\_from\_web\_applications](https://developer.mozilla.org/en-US/docs/Web/API/File\_API/Using\_files\_from\_web\_applications)
