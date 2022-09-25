# Burbuja personalizable

Para cambiar la burbuja por defecto es necesario que codifiques un par de elementos HTML y añadir código Javascript que interactuará con la API del mismo widget.

## Ejemplo

{% hint style="success" %}
El contenido es un ejemplo, puedes reutilizarlo o bien crear por tu propio código. Es decir, la estructura, color, contenido, texto, icono, etc. es completamente personalizable.
{% endhint %}

{% embed url="https://codesandbox.io/s/playground-widget-custom-bubble-ejt85" %}

## ¿Cómo funciona?

Existen elementos relevantes a la hora de modificar la burbuja por defecto. Para ello deberás considerar lo siguiente:

### Estilos CSS

```css
.videsk-top-container {
  z-index: 9999 !important;
}

.videsk-button-iframe {
  visibility: hidden;
}
```

Con el código CSS anterior sobre escribirás los estilos por defecto, para dar paso a tu propia burbuja.

### Widget API

Lo segundo más relevantes es que conozcas sobre la API de nuestro widget que además de permitir aperturar o cerrar el widget, cuenta con `listener`que te ayudarán a escuchar acciones sobre el mismo.

Lo revelante es adjuntar un escucha al evento `click` para ejecutar el método `toggle` del mismo widget.

```javascript
function myToggleFunction () {
 if (window.videsk) videsk.toggle();
}

yourOwnBubble.addEventListener('click', myToggleFunction);
```

{% hint style="info" %}
Recuerda que `yourOwnBubble` es tu elemento DOM que podrás referenciar mediante querySelector.
{% endhint %}
