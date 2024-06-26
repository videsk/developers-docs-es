---
description: Métodos disponibles para realizar acciones de forma 100% programática
---

# Métodos

{% hint style="warning" %}
Recuerda que para acceder a cualquier método debes usar la variable global `videsk`.

\
Esta está disponible como `window.videsk` o `videsk`.
{% endhint %}

## `home`

Este método permite ir a la vista inicial del widget. No recibe ningún argumento.

{% code lineNumbers="true" %}
```javascript
videsk.home();
```
{% endcode %}

{% hint style="warning" %}
Ejecutar este método cuando se está en un llamado puede traer comportamientos inesperados.
{% endhint %}

## `segment`

Este método permite realizar un llamado a un segmento mediante su ID de forma programática. Recibe un argumento el cual es el ID del segmento a llamar.

{% code lineNumbers="true" %}
```javascript
videsk.segment(segmentId);
```
{% endcode %}

{% hint style="info" %}
Este método simula un clic de usuario en el segmento, por lo tanto la siguiente vista podría ser un mensaje de no disponibilidad, formulario o selección de micrófono/cámara.



Lo anterior depende de la configuración de tu cuenta.
{% endhint %}

## `calendar`

Este método permite ingresar a un calendario de un servicio o agente en particular de forma programática. Recibe dos argumentos los cuales son:

* `service`: corresponde al id del servicio (obligatorio)
* `agent`: corresponse al id del agente

{% hint style="warning" %}
El ID del `service` es obligatorio, mientras que `agent` es opcional y dependerá de la configuración del servicio en cuestión.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.calendar(serviceId); // Seleccionará el servicio

videsk.calendar(serviceId, agentId); // Seleccionará el servicio y agente
```
{% endcode %}

{% hint style="info" %}
Si el servicio se configuró como selección manual y no se entrega el argumento de `agent` la vista del widget quedará en el listado de agentes asociados al servicio.
{% endhint %}

## `getByStatus`

Este méodo permite obtener el número de ejecutivos que están conectados a un segmento en particular. Recibe dos argumentos el primero obligatorio corresponde al ID del segmento como `String` y el segundo opcional como `String` que corresponde al estado a buscar que puede ser `online` (por defecto) o `available`.

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

```javascript
await videsk.getByStatus(segmentId); // Por defecto se busca online

await videsk.getByStatus(segmentId, 'available'); // Se buscará por available
```

{% hint style="warning" %}
Debes verificar que el valor de retorno no sea una instancia de error, es decir:

```
const response = await videsk.getByStatus(segmentId);
if (response instanceof Error) return console.error('Error', response.message);
const total = response;
```
{% endhint %}

## `toggle`

Esta es la función para alternar la vista del widget, el cual acciona el mismo evento cuando un cliente hace clic en el botón flotante.

Recibe un argumento el cual es un `boolean` que indica el estado. En caso de no proporcionar un argumento alternará su estado `true/false`.

{% tabs %}
{% tab title="Toggle" %}
```javascript
// To show
videsk.toggle(true);

// To hide
videsk.toggle(false);

// Auto
videsk.toggle();
```
{% endtab %}

{% tab title="On web load" %}
```javascript
document.addEventListener('videsk-load', () => {
    const forceOpen = true;
    videsk.toggle(forceOpen);
});
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
No uses `window.onload` o `window.addEventListener("onload")`, para usar la función `toggle`.
{% endhint %}

## `toggleVisibility`

Este método permite mostrar u ocultar completamente el widget.

Recibe un argumento el cual es un `boolean` que indica el estado. En caso de no proporcionar un argumento alternará su estado `true/false`.

```javascript
videsk.toggleVisibility();
// or
videsk.toggleVisibility(false);
```

## `render`

Este método permite renderizar el widget cuando se le ha solicitado que cargue de forma diferida.

{% hint style="warning" %}
Este método es asíncrono, por lo que deberás usar `async/await` o `promises` para seguir interactuando con el widget.
{% endhint %}

```javascript
await videsk.render();
// O bien
videsk.render().then(...)
```

{% hint style="info" %}
Si ejecutas este método más de 1 vez, el widget lanzará un `warning` en consola.
{% endhint %}

## `devices`

Este método permite obtener el listado de dispositivos disponibles en el equipo.

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
await videsk.devices();
```
{% endcode %}

## `device`

Este método permite obtener un dispositivo en particular mediante la búsqueda de su ID o nombre. Recibe dos argumentos:

* `name`: Nombre de dispositivo
* `type`: tipo de dispositivo. Disponibles `audioinput` y `videoinput`. Por defecto: `audioinput`.

{% hint style="info" %}
El valor que indiques como primer argumento se buscará mediante coincidencia, no igualdad estricta.
{% endhint %}

{% hint style="info" %}
Este método es asíncrono.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
await videsk.device('Sound BlasterX', 'audioinput');  // 4c59e1553b44981af704f3778bc75c8bfbeabf0849b4357c4e9222104f1a794
```
{% endcode %}

En caso que el dispositivo no se encuentre retornará `undefined`.
