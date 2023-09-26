# Slots

Los slots son espacios que contienen elementos por defecto, pero que podrás reemplazar con tus propios elementos. Por ejemplo, para reemplazar los botones de nuestro `WebRTC` deberás añadir:

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
    <div slot="slot-name">cuxtom content</div>
</videsk-webrtc>
```
{% endcode %}

Los `slots` disponibles son:

## Botones

El listado de botones accionables como compartir pantalla, micrófono, cámara, colgar, pantalla completa, rotar cámara y chat se puede personalizar o incluso eliminar.

* `button-screen`: botón de compartir pantalla
* `button-mic`: botón de micrófono
* `button-cam`: botón de cámara
* `button-hangup`: botón de colgar
* `button-toggle-camera`: botón de rotar cámara
* `button-chat`: botón de chat
* `button-fullscreen`: botón de pantalla completa

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Botones disponibles por defecto</p></figcaption></figure>

{% hint style="info" %}
Los botones de cambio de cámara y compartir pantalla automáticamente se mostrarán si la función está disponible en el navegador, de lo contrario no se mostrará.
{% endhint %}

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
    <button slot="button-screen">Compartir pantalla</button>
    <button slot="button-mic">Micrófono</button>
    <button slot="button-cam">Cámara</button>
    <button slot="button-hangup">Colgar</button>
    <button slot="button-toggle-camera">Rotar cámara</button>
    <button slot="button-chat">Chat</button>
    <button slot="button-fullscreen">Pantalla completa</button>
</videsk-webrtc>
```
{% endcode %}

Puedes utilizar cualquier elemento HTML dentro de la etiqueta `videsk-webrtc` incluso elementos complejos como:

{% code lineNumbers="true" %}
```html
<videsk-webrtc>
    <div slot="button-hangup">
        <i class="phone" />
        <span class="tooltip">Colgar</span>
    </div>
</videsk-webrtc>
```
{% endcode %}

## Iconos

Puedes personalizar los íconos:

* `participants-toggle-icons`

```html
<videsk-webrtc>
  <div slot="participants-toggle-icons">
     <!-- Custom icons -->
  </div>
</videsk-webrtc>
```
