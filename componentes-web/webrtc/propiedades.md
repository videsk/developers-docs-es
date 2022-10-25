# Propiedades

Con las propiedades de nuestro componente `WebRTC` podrás cambiar el comportamiento de ciertos elementos y conexiones.

### `video`

Esta propiedad de lectura y escritura, permite modificar el estado del video local, encendido `true` o apagado `false`.

{% hint style="info" %}
Si inicias sin pista de cámara (solo micrófono), y luego cambias el valor a `true` desencadenará obtener un nuevo flujo (stream) de cámara y micrófono.
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').video = true;
document.querySelector('videsk-webrtc').video // true
```

### `audio`

Esta propiedad de lectura y escritura, permite modificar e estado del audio local, encendido `true` o apagado `false`.

```javascript
document.querySelector('videsk-webrtc').audio = true;
document.querySelector('videsk-webrtc').audio // true
```

### `layout`

Esta propiedad de lectura y escritura, permite modifica el diseño del WebRTC. Los valores aceptados son `sidebar` y `grid`.

```javascript
document.querySelector('videsk-webrtc').layout = 'sidebar';
```

Esta propiedad también puede ser definida mediante atributos en el elemento. Por defecto, si no está presente el atributo `sidebar` es valor de la propiedad `layout` será `grid`. Cualquier cambio mediante la propiedad `layout` será reflejado como atributo y viceversa.

```html
<videsk-webrtc sidebar></videsk-webrtc>
```

### `chat`

Esta propiedad de lectura y escritura, permite mostrar `true` y ocultar `false` el chat.

```javascript
document.querySelector('videsk-webrtc').chat = true;
document.querySelector('videsk-webrtc').chat; // true
```

### `peers`

Esta propiedad de lectura y escritura, retorna el listado de conexiones pares como un [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map).

{% hint style="warning" %}
Si utilizas nuestro SDK, no deberás sobrescribir el valor `Map`, por defecto.
{% endhint %}

{% hint style="info" %}
Interactuar con las conexiones pares requiere de conocimiento avanzado en WebRTC.
{% endhint %}

```javascript
document.querySelector('videsk-webrtc').peers
```

### `isConnectedWithPeer`

Esta propiedad de solo lectura, retorna un `boolean` si existe al menos una conexión de pares activa.

```javascript
document.querySelector('videsk-webrtc').isConnectedWithPeer
```

### `sharingScreen`

Esta propiedad de solo lectura, retorna un `boolean` con el estado de compartir pantalla.

```javascript
document.querySelector('videsk-webrtc').sharingScreen
```

### `defaultConstraints`

Esta propiedad de solo lectura, retorna un `object` con las restricciones por defecto de la cámara.

```javascript
{
    video: { facingMode: { ideal: 'user' } },
    audio: true,
}
```
