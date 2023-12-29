---
description: >-
  A continuación verás sacar el máximo provecho a nuestro WebRTC como componente
  web.
---

# 📹 WebRTC

Un componente web permite que nuestro `WebRTC` opere como un elemento DOM nativo de los navegadores. De esta manera, podrás interactuar con el tal cual como con una etiqueta HTML.

Dentro de nuestro WebRTC podrás personalizar los botones disponibles, añadir elementos personalizados, cambiar el layout, escuchar eventos, definir tu propio CSS y mucho más.

Nuestro componente web pretende entregar una flexibilidad única al momento de personalizar la experiencias de tus clientes.

Para poder personalizar nuestro `WebRTC` como componente web, deberás definir la etiqueta en alguna parte de tu código HTML:

{% code lineNumbers="true" %}
```html
<videsk-webrtc></videsk-webrtc>
```
{% endcode %}

{% hint style="info" %}
Si defines el componente web, recuerda hacer [referencia en nuestro SDK](../../sdks/webrtc/metodos.md#create), de lo contrario se creará uno nuevo.
{% endhint %}

Puedes utilizar nuestro componente web independiente de nuestro SDK, pero deberás hacerte cargo de las conexiones `WebSocket` con nuestro servidor de señalización `wss://exchange.videsk.io`.
