# Eventos

Para poder asignar las funciones personalizadas debes utilizar nuestra función global de la siguiente forma:

```javascript
// Use window.__VIDESK_WIDGET_ONLOAD__ only for load events not for functions
window.__VIDESK_WIDGET_ONLOAD__ = function() {
    videsk.events = {
        onToggle: function (){},
        onQueued: function (){},
    };
}
```

* onToggle $$f$$&#x20;
* onFullToggle $$f$$&#x20;
* onSelected $$f$$
* onQueued $$f$$
* onQueueUpdated $$f$$
* onQueueAbandoned $$f$$
* onDismissed $$f$$
* onStart $$f$$&#x20;
* onEnd $$f$$&#x20;
* onSurvey $$f$$&#x20;
* onReconnected $$f$$
* onConnectionError $$f$$&#x20;

## onToggle

Este evento permite escuchar cuando se dispara el evento de visibilidad de Videsk ya sea por que un cliente hizo clic en la burbuja flotante o se ejecutó mediante la función API `videsk.toggle()`

El evento retornará el estado de visibilidad del widget como `booleano` `true` o `false` y la fecha en la cual se disparó en formato `datetime`.

```javascript
videsk.events.onToggle = function ({ status, date }) {
    // Do something here with status and date
}
```

## onFullToggle

Este evento permite escuchar cuando se dispara el evento de visibilidad tanto burbuja como cuerpo del widget.

{% hint style="info" %}
Habitualmente este evento se gatilla por parámeteros presentes en la URL. Y es diferente del evento `onToggle` el cual solo indica cuando se abre, a diferencia de este el cual indica la apertura y visibilidad.
{% endhint %}

```javascript
videsk.events.onToggle = function ({ status, date }) {
    // Do something here with status and date
}
```

## onSelected

Este evento permite escuchar cuando el cliente seleccionó un segmento.

El evento retornará el nombre del segmento como `string`, la disponibilidad de agentes en el segmento como `boolean` y la fecha en el cual se realizó como `datetime`.

{% hint style="info" %}
Este evento puede ser utilizado para redirigir a un mensaje por WhatsApp u otro canal, en caso que **no** se estén disponible.
{% endhint %}

{% hint style="warning" %}
Deberás escoger entre formulario de contacto o realizar una acción mediante este evento.
{% endhint %}

```javascript
videsk.events.onSelected = function ({ name, available, date }) {
    // Do something here with name of segment, availability and date
}
```

## onQueued

Este evento permite escuchar cuando el cliente ha sido añadido a la fila virtual.

El evento retornará la posición del cliente en la fila de espera como `number` y la fecha como `datetime`.

```javascript
videsk.events.onQueued = function ({ position, date }) {
    // Do something here with position and date
}
```

## onQueueUpdated

Este evento permite escuchar cuando la posición del cliente ha sido actualizada.

El evento retornará la posición actualizada del cliente en la fila como `number` y la fecha como `datetime`.

```javascript
videsk.events.onQueueUpdated = function ({ position, date }) {
    // Do something here with position and date
}
```

## onQueueAbandoned

Este evento permite escuchar cuando el cliente ha abandonado la llamada durante la fila virtual.

{% hint style="danger" %}
Este evento no tiene relación cuando la llamada termina o inicia. Esto evento solo sucede si el cliente hace clic en el botón cancelar o se ejecuta la función de abandonar la espera.
{% endhint %}

El evento retornará la fecha en el cual se ejecutó la acción de abandonar la fila como `datetime`.

```javascript
videsk.events.onQueueAbandoned = function ({ date }) {
    // Do something with date
}
```

## onDismissed

Este evento permite escuchar cuando un agente rechaza una llamada.

El evento retornará la fecha en el cual se ejecutó la acción de rechazo como `datetime`.

```javascript
videsk.events.onDismissed = function ({ date }) {
    // Do something with date
}
```

## onStart

Este evento permite escuchar cuando el cliente ingresa a la videollamada, es decir, un agente ha contestado la llamada y el cliente ingresa a la videollamada.

El evento retornará la fecha como `datetime` en el cual sucedió.

```javascript
videsk.events.onStart = function ({ date }) {
    // Do something with date
}
```

## onEnd

Este evento permite escuchar cuando el cliente termina la videollamada, es decir, finaliza al hacer clic en colgar o el agente finaliza la llamada.

El evento retornará la fecha como `datetime` en el cual sucedió.

```javascript
videsk.events.onEnd = function ({ date }) {
    // Do someting with date
}
```

## onSurvey

Este evento permite escuchar cuando el cliente envía la encuesta tras terminar una llamada.

{% hint style="info" %}
Este evento dependerá si tiene activada la opción de encuesta al final de una llamada.
{% endhint %}

El evento retornará dos argumentos, el primer corresponde un `object` con la encuesta y el segundo con la fecha en la cual se envió como `datetime`.

```javascript
videsk.events.onSurvey = function ({ survey, date }) {
    // Do something with survey and date
}
```



## onReconnected

Este evento permite escuchar cuando se ha reconectado a una llamada activa, ya sea porque se recargó o cerró la ventana del navegador/app móvil.

{% hint style="info" %}
Este evento dependerá si el widget carga junto con tu sitio.
{% endhint %}

El evento retornará la fecha en la cual se se ha reconectado como `datetime`.

```javascript
videsk.events.onReconnected = function ({ date }) {
    // Do something with survey and date
}
```



## onConnectionError

Este evento permite escuchar cuando existe errores en la conexión antes de la llamada.

{% hint style="info" %}
Puede ocurrir que nuestros servidores detecten que un usuario se está conectando desde una red o equipo sospechoso, realizando un bloqueo.
{% endhint %}

El evento retornará la fecha en la cual se se ha generad el error de conexión como `datetime`.

```javascript
videsk.events.onConnectionError = function ({ date }) {
    // Do something with survey and date
}
```
