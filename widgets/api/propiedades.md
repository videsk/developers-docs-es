---
description: Propiedades disponibles para realizar acciones de forma 100% programática
---

# Propiedades

Nuestro widget contiene propiedades que permiten cambiar o sobreescribir el comportamiento por defecto.

{% hint style="info" %}
Te sugerimos utilizar estas propiedades solo una vez que el evento `videsk-load` sea disparado.

```javascript
document.addEventListener('videsk-load', () => {
    // Puedes usar aquí las propiedades
    videsk.xyz = '...';
});
```
{% endhint %}

## `customer`

{% hint style="info" %}
Esta propiedad rellenará el formulario automáticamente con los datos que proporciones, no los envía automáticamente. Esto debido a que formularios tiene una protección anti-bot que se activa con 1 clic en el botón inferior del formulario.
{% endhint %}

Esta propiedad de solo escritura permite definir los valores que se inyectarán por defecto en los formularios que tengas configurado para segmentos y calendarios. Estos valores dependerán de la propiedad `name` de cada campo de formulario, por ejemplo:

```javascript
videsk.customer = {
    firstname: 'John',
    lastname: 'Doe',
    dni: 'ABC123456'
}
```

El nombre de cada key dependerá de cómo está configurado la propiedad `name` de cada campo en el editor de formulario. Si la key no coincide el campo quedará vacío para que el cliente lo rellene manualmente.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## `constraints`

Esta propiedad de lectura y escritura permite sobreescribir los valores por defecto de cámara y/o micrófono.

Este valor sobreescribirá la opción de micrófono y cámara, independientemente si tu cliente selecciona `solo micrófono` o `micrófono + cámara`.

{% hint style="warning" %}
La autorización explícita del cliente mediante el navegador no se sobreescribira, por lo que si deniega el acceso a cámara y/o micrófono no accederá a la videollamada.
{% endhint %}

{% hint style="info" %}
Por defecto, este valor es indefinido.
{% endhint %}

{% tabs %}
{% tab title="Básico" %}
{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
    video: false, // sin cámara
    audio: true,
};
videsk.constraints // undefined
```
{% endcode %}


{% endtab %}

{% tab title="Micrófono fijo" %}
{% hint style="info" %}
Te sugerimos utilizar el método [device](https://developers.videsk.io/widgets/api/metodos#device) para obtener el ID del dispositivo.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
    video: true,
    audio: {
        deviceId: {
            ideal: 'REPLACE_DEVICE_ID'
        }
    },
};
```
{% endcode %}
{% endtab %}

{% tab title="Cámara fija" %}
{% hint style="info" %}
Te sugerimos utilizar el método [device](https://developers.videsk.io/widgets/api/metodos#device) para obtener el ID del dispositivo.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
    audio: true,
    video: {
        deviceId: {
            ideal: 'REPLACE_DEVICE_ID'
        }
    },
};
```
{% endcode %}
{% endtab %}

{% tab title="Cámara trasera" %}
{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
    audio: true,
    video: {
        facingMode: 'environment'
    }
};
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Te sugerimos utilizar esta propiedad en tótems o kioskos interactivos, ya que podrás definir los permisos con anterioridad sin percibir problemas técnicos.
{% endhint %}

## `fullscreen`

Con esta propiedad podrás configurar el widget para que cubra todo el sitio sin necesidad de añadir CSS personalizado.

```javascript
videsk.fullscreen = true;
```

{% code lineNumbers="true" %}
```javascript
document.addEventListener('videsk-load', () => {
    videsk.fullscreen = true;
    videsk.toggle(true);
});
```
{% endcode %}

{% hint style="warning" %}
Al usar el widget en modo `fullscreen` la burbuja desaparece, por lo tanto, deberás usar `videsk.toggle(true)` para forzar la visibilidad.
{% endhint %}

## `width`

Con esta propiedad podrás configurar el ancho del widget sin necesidad de añadir CSS personalizado. El valor debe ser un `Integer`, el cual se configurará en pixeles.

{% code lineNumbers="true" %}
```javascript
videsk.width // Obtendrás el ancho
videsk.width = 360;
```
{% endcode %}

Si deseas mantener la responsibidad sugerimos cambiar el ancho del elemento `.videsk-top-container` mediante CSS, para la propiedad `width`.

## `height`

Con esta propiedad podrás configurar la altura del widget sin necesidad de añadir CSS personalizado. El valor debe ser un `Integer`, el cual se configurará en pixeles.

```javascript
videsk.height // Obtendrás el ancho
videsk.height = 650;
```

Si deseas mantener la responsibidad sugerimos cambiar la altura del elemento `.videsk-home-iframe` mediante CSS, para las propiedades `height` y `max-height`.

{% hint style="warning" %}
**Usar `width` o `height` mediante sus propiedades romperá con la responsividad**, sugerimos utilizar solo estas propiedades basado en compartamientos, no para fijar el estilo.
{% endhint %}

## `referrer`

Con esta propiedad podrás configurar la URL del sitio web de referencia el cual almacenaremos para indicar desde donde se realizó la llamada o agendamiento. Debes considera que debe ser una url válida que debe incluir el protocolo `https://` .

{% hint style="warning" %}
Ten en consideración que la URL para el **caso de agendamiento** debe si o si tener integrado el widget o SDK, de lo contrario tus clientes no se podrán unir a la reunión.
{% endhint %}

```javascript
videsk.referrer = 'https://myportal.videsk.io';
```

{% hint style="info" %}
Recuerda que desde el dashboard puede personalizar la plantilla de correo para agendamiento donde también puedes sobrescribir la URL de destino.\`
{% endhint %}

## `totem`&#x20;

Esta propiedad permite deshabilitar comportamientos del widget en modo web para que en un kiosco o totem no interrumpan una experiencia continua. Esto deshabilita:

1. Redirección "Usamos Videsk"

```javascript
videsk.totem = true;
```
