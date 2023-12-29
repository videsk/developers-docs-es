# Propiedades

## `store`

Esta propiedad contiene el listado de archivos recibidos. Corresponde a un `Map`, por lo tanto podrás acceder a cada archivo con las [propiedades nativas de un constructor Map](#user-content-fn-1)[^1].

La tienda está construída con clave de `CRC-32` y como valor [`BeamPortFile`](beamportfile.md).

```javascript
port.store; // Map {}
// Listado de archivos
port.store.get(crc32); // Retorna un BeamPortFile
```

## `connected`

Esta propiedad devuelve un `Boolean` sobre estado de conexión.

```javascript
port.connected; // true o false
```

## `ports`

Esta propiedad devuelve la cantidad de pares `BeamPort` conectados como número entero. Habitualmente el valor siempre será `1`.

```javascript
port.ports;
```

## `connection`

Esta propiedad retorna la conexión de par activa como [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel).

```
port.connection;
```

{% hint style="info" %}
Sugerimos no utilizar la conexión para enviar datos sin conocimiento, ya que se envían en una nomenclatura binaria propietaria.
{% endhint %}

## `debug`

Esta propiedad retorna el acceso al modo debugger propietario. Para hacer uso del debugger deberás definir en `localStorage` la clave `debug` con el valor en `beamport`.

```javascript
localStorage.debug = 'beamport';
```

{% hint style="info" %}
Recuerda que activar el modo debug es ineficiente para entornos productivos.
{% endhint %}

## Propiedades estáticas

Todas las propiedades estáticas se pueden acceder directamente desde el constructor `BeamPort`, sin necesidad de instanciar.

```javascript
BeamPort.DESCRIPTION
BeamPort.RECEIVED
BeamPort.FAILED
```

### `DESCRIPTION`

Su valor es igual al número `1`.

### `CHUNK`

Su valor es igual al número `2`.

### `STATE`

Su valor es igual al número `3`.

### `EXCHANGED`

Su valor es igual al número `4`.

### `RECEIVED`

Su valor es igual al número `5`.

### `FAILED`

Su valor es igual al número `6`.

### `DELETED`

Su valor es igual al número `7`.

[^1]: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map)
