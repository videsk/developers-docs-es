---
description: Te explicamos cómo usar nuestro SDK de intercambio de archivos.
---

# 📂 Intercambio archivos

{% hint style="warning" %}
La documentación y recursos necesarios para utilizar FileShare SDK está estrictamente restringido para uso de clientes de Videsk. Nos reservamos el derecho de restringir su acceso y uso, si detectamos un uso inadecuado.
{% endhint %}

Este SDK te permite utilizar la función de intercambio de archivos de forma sencilla, pero te permite definir tu propia interfaz o flujos.

El sistema de intercambio de archivos opera como una bandeja de envío, que posee a su vez una lista de archivos por enviar o ya enviados.

## Instalación

Para utilizar el intercambio de archivo necesitas cargar:

{% tabs %}
{% tab title="HTML" %}
```html
<script src="https://cdn.videsk.io/sdk/filesharing.min.js" async></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/filesharing.min.js";
script.setAttribute('async', true);
document.appendChild(script);
```
{% endtab %}
{% endtabs %}

Este SDK **no** requiere de una instancia manual, es decir, `new FileSharing()`. Actualmente, debes utilizarlo en conjunto con nuestro otro [SDK Phone](../phone.md).

Esto lo podrás hacer usando un método llamado `addExtension`, la cual permite añadir extensiones o características extras.

```javascript
const phone new Phone();
phone.addExtension({ name: 'fileshare', extension: FileShare });
```

En el caso de la clave (key) `extension`, corresponde a la clase `FileShare`. Por lo tanto, debes cargar el `script` desde nuestro CDN previamente a este código para poder referenciarlo.

Una vez que hagas esto, automáticamente [Phone](../phone.md) SDK se hará cargo del intercambio a nivel de red y deberás escuchar los diferentes eventos.

## Instancia FileShare

Para obtener acceso a la instancia `FileShare` deberás usar el método `extensionGetModule`.

```javascript
const fileshare = phone.extensionGetModule('fileshare');
```

Esto devuelve una instancia de la clase `FileShare` con sus métodos y propiedades.

## Listado de archivos

Para acceder al listado de archivos debes usar la propiedad `queue`.

```javascript
const fileshare = phone.extensionGetModule('fileshare');
const files = fileshare.queue;
```

Para obtener un listado actualizado puedes usar los eventos usando la propiedad de la instancia `fileshare.queue`.

{% content-ref url="metodos.md" %}
[metodos.md](metodos.md)
{% endcontent-ref %}

{% content-ref url="eventos.md" %}
[eventos.md](eventos.md)
{% endcontent-ref %}
