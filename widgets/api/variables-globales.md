---
description: >-
  A continuación, te explicamos como acceder al widget mediante variables
  globales
---

# Variables globales

Actualmente para acceder al widget existen dos variables globales que puedes usar:

* `window.videsk`
* `videsk`

El problema de estas variables globales, es que están disponibles solo una vez que el widget está totalmente cargado, lo que podría provocar errores de variables globales indefinidas.

Para ellos disponemos de variables globales que el widget observa antes de cargar con el objetivo de modificar su comportamiento por defecto.

Estas son:

#### Iniciar oculto

```
window.__VIDESK_WIDGET_START_HIDE__
```

&#x20;Esta variable global al estar con el valor en `true`, permite que el widget inicio totalmente oculto.

#### Inicio diferido

```
window.__VIDESK_LOAD_DEFERER__
```

Esta variable global al estar con el valor en true, permite que el widget no se cargue hasta ejecutar el método `render`.

## ¿Cómo ocultar el widget?

Para ocultar el widget, durante la carga, debes añadir en tú sitio y antes del `script` de Videsk Widget la siguiente variable global:

{% hint style="warning" %}
Esta acción es para ocultar completamente el widget. Es decir, cuerpo y burbuja flotante.

**Se recomienda en caso de requerir accionar la visibilidad desde un componente del sitio.**
{% endhint %}

{% tabs %}
{% tab title="Global var" %}
```javascript
// This before script !!
window.__VIDESK_WIDGET_START_HIDE__ = true;

<script src="..." videsk-token="..." async></script>
```
{% endtab %}

{% tab title="Onload" %}
```javascript
// This before script !!

window.__VIDESK_WIDGET_ONLOAD__ = function() {
    videsk.toggleVisibility(true || false)
}

<script src="..." videsk-token="..." async></script>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Recuerda que para acceder a la API del Widget es mediante la variable global `videsk`
{% endhint %}

## Carga diferida

La carga diferida es recomendada para sitios web de alto tráfico o temporadas hot sales. Te sugerimos añadir este comportamiento basado en clics de elementos externos como botones personalizados, banners, etc.

{% hint style="warning" %}
El siguiente código **deberás añadirlo antes de cargar el widget**.
{% endhint %}

```javascript
window.__VIDESK_LOAD_DEFERER__ = true;

// Load widget script ....
// After widget script ...
document.querySelector('#my-button').addEventListener('click', async () => {
  if (!window.videsk) return;
  await videsk.render();
  videsk.toggle();
});
```

De esta manera cargarás solo el widget cuando un cliente interactúe mediante un clic con un elemento personalizado.

{% hint style="danger" %}
Por calidad de servicio, si detectamos altos picos de tráficos podemos bloquear la carga en tu sitio web hasta que apliques esta estrategia.
{% endhint %}
