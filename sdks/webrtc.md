---
description: SDK para crear una instancia de conexión de videollamada WebRTC.
---

# 📹 WebRTC

Con este SDK podrás una instancia de conexión de videollamada WebRTC de una manera muy simple.

{% hint style="warning" %}
Este SDK lo deberás utilizar con nuestro [Phone SDK](phone/).
{% endhint %}

## Instalación

Para comenzar deberás instalar nuestro recurso en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/videsk-webrtc-sdk.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://assets.videsk.io/js/videsk-webrtc-sdk.min.js";
document.body.appendChild('body'); // O reemplaza con el nodo DOM que desees
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
No almacenes el contenido del script en tu servidor, **esto infringe nuestros términos de uso**.
{% endhint %}

## Instanciación

Primero deberás instanciar `VideskWebRTCSDK` como un [constructor](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Classes/constructor).

```javascript
const webrtc = new VideskWebRTCSDK(callId, events, options);
```

### Parámetros

`VideskWebRTCSDK` es una clase que recibe lo siguientes parámetros. Los parámetros con \* (asterisco) son obligatorios.

#### call\*

Corresponde al id como `string` de la videollamada, obtenido mediante una conexión previa. Ejemplo, usando nuestro [Phone SDK](phone/#answered).

#### events

Corresponde a un `object` que deberá contener el listado de los eventos. Revisa la [sección de eventos](webrtc.md#eventos) para más información.

Existen dos laternativas de definir los eventos:

{% tabs %}
{% tab title="Alternativa 1" %}
```javascript
const events = { ... };
const webrtc = new VideskWebRTCSDK(callId, events, options);
```
{% endtab %}

{% tab title="Alternativa 2" %}
```javascript
const webrtc = new VideskWebRTCSDK(callId, {}, options);
webrtc.on('eventName', () => {});
```
{% endtab %}
{% endtabs %}

#### options\*

Corresponde a un `object` que deberá contener el nodo donde deberá renderizarse la videollamada, cámara y/o micrófono, opción de modo `debug`.

{% tabs %}
{% tab title="Nodo como string" %}
```javascript
const options = {
    el: '#webrtc',
    devices: { audio: true, video: true },
    debug: false,
};
```
{% endtab %}

{% tab title="Nodo como objeto" %}
```javascript
const options = {
    el: document.querySelector('#webrtc'),
    devices: { audio: true, video: true },
    debug: false,
};
```
{% endtab %}
{% endtabs %}

## Métodos

Los siguientes métodos te permitirán tener control sobre la instancia de WebRTC.

### create

Este método creará y renderizará un `iframe` con la videollamada automáticamente.

```javascript
webrtc.create();
```

### destroy

```javascript
webrtc.destroy();
```

Este método eliminará el nodo HTML que la videollamada.

{% hint style="info" %}
Solo se eliminará el nodo `iframe`, es decir, que el nodo padre y su contenido quedará vacío.
{% endhint %}

## Eventos

Este SDK emitirá eventos para que puedas controlar el comportamiento de la aplicación.

### hangup

Este evento se emitirá cuando el cliente haga clic en el botón de colgar en la videollamada.

```javascript
webrtc.on('hangup', function (){
    // Deberás cortar la llamada
});
```

{% hint style="info" %}
Visita la documentación de nuestro [Phone SDK](phone/#colgar) para conocer como colgar una llamada
{% endhint %}

### denied-permissions

Este evento se emitirá cuando se niegen los permisos de acceso a la cámara y micrófono.

```javascript
webrtc.on('denied-permissions', function () {
    // Mostrar un mensaje que los permisos fueron denegados
});
```
