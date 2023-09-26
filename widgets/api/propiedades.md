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

