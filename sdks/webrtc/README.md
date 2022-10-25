---
description: SDK para crear una instancia de conexión de videollamada WebRTC.
---

# 📹 WebRTC

Con este SDK podrás una instancia de conexión de videollamada WebRTC de una manera muy simple.

{% hint style="warning" %}
Este SDK lo deberás utilizar con nuestro [Phone SDK](../phone.md).
{% endhint %}

## Instalación

Para comenzar deberás instalar nuestro SDK en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
{% code lineNumbers="true" %}
```html
<script src="https://cdn.videsk.io/sdk/webrtc.min.js"></script>
```
{% endcode %}
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/webrtc.min.js";
document.body.appendChild('body'); // O reemplaza con el nodo DOM que desees
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
No almacenes el contenido de nuestro SDK en tu servidor, **esto infringe nuestros términos de uso**.
{% endhint %}

## Uso

Nuestro SDK es un componente web, lo que permite que accedas como cualquier elemento HTML o nodo DOM que estás acostumbrado.

{% code lineNumbers="true" %}
```html
<videsk-webrtc></videsk-webrtc>
```
{% endcode %}

Puedes ver más información de nuestro componente web en el siguiente link:

{% content-ref url="../../componentes-web/webrtc/" %}
[webrtc](../../componentes-web/webrtc/)
{% endcontent-ref %}

{% hint style="info" %}
Deberás cargar el script de nuestro CDN, de lo contrario será un tag vacío.
{% endhint %}

Posteriormente, deberás crear una instancia `WebRTC` la cual **te permitirá realizar la conexión**.

{% code lineNumbers="true" %}
```javascript
const webrtc = new WebRTC();
await webrtc.create(accessToken, constraints);
```
{% endcode %}

Puedes ver los métodos disponibles en la siguiente página:

{% content-ref url="metodos.md" %}
[metodos.md](metodos.md)
{% endcontent-ref %}

### Argumentos

La clase `WebRTC` recibe tres argumentos:

#### `component` (opcional)

Corresponde a la referencia DOM del componente web, ejemplo:

{% code lineNumbers="true" %}
```javascript
const element = document.querySelector('videsk-webrtc');
new WebRTC(element);
```
{% endcode %}

Si el valor es `undefined`, `null` o inválido por defecto creará un nodo `videsk-webrtc` en el nodo `parent` que por defecto es `body`.

#### `parent` (opcional)

Corresponde a la referencia DOM donde se adjuntará (`append`) el componente web `videsk-webrtc`.

{% code lineNumbers="true" %}
```javascript
const parent = document.querySelector('#custom-div');
new WebRTC(null, parent);
```
{% endcode %}

#### `options` (opcional)

Corresponde a opciones que se le entregan a la instancia WebRTC para modificar los valores por defecto.

{% code lineNumbers="true" %}
```javascript
const options = {
    websocket: { hostname: 'wss://exchange.videsk.io' }
};
```
{% endcode %}

### Crear instancia

Para crear una instancia deberás usar solo dos líneas de código:

{% code lineNumbers="true" %}
```javascript
const webrtc = new WebRTC();
await webrtc.create(accessToken);
```
{% endcode %}
