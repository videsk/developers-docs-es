---
description: >-
  A continuación podrás ver como realizar llamadas directamente mediante
  parámetros en la URL.
---

# 🔗 Acciones por URL

## Llamada a segmento

Con esta función podrás lograr que tus clientes puedan realizar una llamada de forma directa a un segmento uniéndose de forma automática sin clics. Esto provocará que el widget integrado en tu web, se gatille de forma automática.

{% hint style="info" %}
También puedes disparar una llamada de forma diferida mediante [acción programática](api/metodos.md#segment).
{% endhint %}

Para ello podrás hacerlo de dos maneras:

## Manualmente

Simplemente deberás escribir el enlace de tu sitio web ya sea `tusitioweb.com` o un una página en específico `tusitioweb.com/contact` y añadir un parámetro al final.

La nomenclatura es `videsk-segment=ID_SEGMENTO`, donde el `ID_SEGMENTO` lo deberás reemplazar con el que necesites y lo podrás obtener desde tu dashboard.

```
https://tusitioweb.com/?videsk-segment=ID_DEL_SEGMENTO
https://tusitioweb.com/?videsk-segment=617729f58103e30802b89e7f
```

Si envías este enlace a un cliente ya sea por correo electrónico, SMS, WhatsApp, etc. ingresará a la fila de ese segmento de forma automática.

{% hint style="warning" %}
La unión automática a la fila dependerá del estado de disponibilidad de tus agentes.
{% endhint %}

{% hint style="info" %}
Si necesitas añadir más parámetros utiliza el carácter `&` para concatenar más parámetros. **El orden de los parámetros no influye!**

Es útil cuando utilizas plataformas de analíticas como Google analytics que requieren parámetros en la URL.
{% endhint %}

Ejemplo:

```
https://tusitioweb.com?videsk-segment=ID_SEGMENTO&utm_campaign=cyber&utm_source=email
```

## Programática

{% hint style="info" %}
Hemos añadido la función de llamada programática, la cual puedes [ver aquí](api/metodos.md#segment).
{% endhint %}

Para lograr que tus clientes ingresen a la fila utilizando una acción programática, requiere que tu widget cargue de forma diferida, es decir, solo cargue luego de configurar el/los parámetros en la URL.

```javascript
function setVideskParameters(segmentId) {
    const params = new URLSearchParams(window.location.search)
    params.set("videsk-segment", segmentId); // Here goes segment ID
    const fullURL = window.location.pathname + '?' + params.toString();
    history.pushState(null, '', fullURL);
}
setVideskParameters("617729f58103e30802b89e7f");
```

{% hint style="success" %}
El código anterior no elimina parámetros existentes solo añadirá `videsk-segment`
{% endhint %}

Luego de este extracto de código podrás cargar tu widget con Javascript, [como se indica acá](integration/#script-de-integracion).
