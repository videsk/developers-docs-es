# Browser SDK

Para utilizar las salas deberás hacer uso de nuestro [webrtc](../sdks/webrtc/ "mention") SDK. Este SDK está compuesto de nuestro componente web [webrtc](../componentes-web/webrtc/ "mention").

Ambos elementos funcionan bajo el SDK, que controla las conexiones e intercambio de mensajes, mientras el componente web renderiza la interfaz de videollamada, controla medios locales y remotos.

Están diseñados para requerir la menor cantidad de código posible, pero al mismo tiempo te entregan la flexibilidad de modificar UI y comportamiento a tus necesidades.

## Cómo usar

Podrás encontrar más detalles de métodos, eventos y propiedades de cada elemento en el [SDK](../sdks/webrtc/) y el [componente web](../componentes-web/webrtc/).



1. Deberás [cargar nuestro SDK](../sdks/webrtc/#instalacion) (el cual contiene el componente web)
2. Obtener un accessToken creando una sala ([#post-vpaas-rooms](rooms-api.md#post-vpaas-rooms "mention")) u obteniendo uno nuevo ([#post-vpaas-rooms-roomid-join](rooms-api.md#post-vpaas-rooms-roomid-join "mention")).
3. Instanciar WebRTC

```javascript
const response = await fetch('https://mybackend.com/rooms/me');
const { accessToken } = response.json();

const webrtc = new WebRTC();
await webrtc.create(accessToken);
```

{% hint style="info" %}
Por defecto, nuestro SDK insertará el componente `<videsk-webrtc>` en `body`. Puedes encontrar más detalles de este comportamiento acá: [#argumentos](../sdks/webrtc/#argumentos "mention").
{% endhint %}

