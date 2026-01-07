# Eventos

Nuestro widget emite un evento al momento de cargar llamado `videsk-load`, el cual puede ser usado para comenzar a interactuar con el widget, esto debido a que posee una carga diferida y asíncrona:

```javascript
document.addEventListener('videsk-load', () => {
    // Puedes usar la variable global videsk
});
```

Para poder asignar las funciones personalizadas debes utilizar nuestra función global `videsk` de la siguiente forma:

```javascript
document.addEventListener('videsk-load', () => {
    videsk.events = {
        onToggle: function (){},
        onQueued: function (){},
    };
});
```

{% hint style="info" %}
Puedes acceder a nuestra variable global mediante `window.videsk` o `videsk`.
{% endhint %}

* [onToggle](eventos.md#ontoggle) $$f$$&#x20;
* [onFullToggle](eventos.md#onfulltoggle) $$f$$&#x20;
* [onSelected](eventos.md#onselected) $$f$$
* [onUnavailable](eventos.md#onunavailable) $$f$$
* [onQueued](eventos.md#onqueued) $$f$$
* [onQueueUpdated](eventos.md#onqueueupdated) $$f$$
* [onQueueAbandoned](eventos.md#onqueueabandoned) $$f$$
* [onDismissed](eventos.md#ondismissed) $$f$$
* [onStart](eventos.md#onstart) $$f$$&#x20;
* [onEnd](eventos.md#onend) $$f$$&#x20;
* [onSurvey](eventos.md#onsurvey) $$f$$&#x20;
* [onReconnected](eventos.md#onreconnected) $$f$$
* [onConnectionError](eventos.md#onconnectionerror) $$f$$&#x20;
* [onFormSubmission](eventos.md#onformsubmission)  $$f$$&#x20;
* [onDateSelected](eventos.md#ondateselected)  $$f$$&#x20;
* [onScheduled](eventos.md#onscheduled)  $$f$$&#x20;

{% hint style="info" %}
Mantenemos compatibilidad con versiones anteriores para definir eventos mediante `videsk.events.onEventName = () => {}`.
{% endhint %}

## onToggle

Este evento permite escuchar cuando se dispara el evento de visibilidad de Videsk ya sea por que un cliente hizo clic en la burbuja flotante o se ejecutó mediante la función API `videsk.toggle()`

El evento retornará el estado de visibilidad del widget como `booleano` `true` o `false` y la fecha en la cual se disparó en formato `datetime`.

```javascript
videsk.addEventListener('onToggle', ({ status, date }) => {
    // Do something here with status and date
});
```

## onFullToggle

Este evento permite escuchar cuando se dispara el evento de visibilidad tanto burbuja como cuerpo del widget.

{% hint style="info" %}
Habitualmente este evento se gatilla por parámeteros presentes en la URL. Y es diferente del evento `onToggle` el cual solo indica cuando se abre, a diferencia de este el cual indica la apertura y visibilidad.
{% endhint %}

```javascript
videsk.addEventListener('onFullToggle', ({ status, date }) => {
    // Do something here with status and date
});
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
videsk.addEventListener('onSelected', ({ name, available, date }) => {
    // Do something here with name of segment, availability and date
});
```

## onUnavailable

Este evento permite escuchar cuando se intentó llamar y no hay ejecutivos conectados.

```javascript
videsk.addEventListener('onUnavailable', () => {
    // Do something
});
```

## onQueued

Este evento permite escuchar cuando el cliente ha sido añadido a la fila virtual.

El evento retornará la posición del cliente en la fila de espera como `number` , la fecha como `datetime` `audio` y `video` como boolean para indicar el estado de cada dispositivo de entrada.

```javascript
videsk.addEventListener('onQueued', ({ position, date, audio, video }) => {
    // Do something here with position and date
});
```

## onQueueUpdated

Este evento permite escuchar cuando la posición del cliente ha sido actualizada.

El evento retornará la posición actualizada del cliente en la fila como `number` y la fecha como `datetime`.

```javascript
videsk.addEventListener('onQueueUpdated', ({ position, date }) => {
    // Do something here with position and date
});
```

## onQueueAbandoned

Este evento permite escuchar cuando el cliente ha abandonado la llamada durante la fila virtual.

{% hint style="danger" %}
Este evento no tiene relación cuando la llamada termina o inicia. Esto evento solo sucede si el cliente hace clic en el botón cancelar o se ejecuta la función de abandonar la espera.
{% endhint %}

El evento retornará la fecha en el cual se ejecutó la acción de abandonar la fila como `datetime`.

```javascript
videsk.addEventListener('onQueueAbandoned', ({ date }) => {
    // Do something with date
});
```

## onDismissed

Este evento permite escuchar cuando un agente rechaza una llamada.

El evento retornará la fecha en el cual se ejecutó la acción de rechazo como `datetime`.

```javascript
videsk.addEventListener('onDismissed', ({ date }) => {
    // Do something with date
});
```

## onStart

Este evento permite escuchar cuando el cliente ingresa a la videollamada, es decir, un agente ha contestado la llamada y el cliente ingresa a la videollamada.

El evento retornará la fecha como `datetime` en el cual sucedió.

```javascript
videsk.addEventListener('onStart', ({ date }) => {
    // Do something with date
});
```

## onEnd

Este evento permite escuchar cuando el cliente termina la videollamada, es decir, finaliza al hacer clic en colgar o el agente finaliza la llamada.

El evento retornará la fecha como `datetime` en el cual sucedió.

```javascript
videsk.addEventListener('onEnd', ({ date }) => {
    // Do someting with date
});
```

## onSurvey

Este evento permite escuchar cuando el cliente envía la encuesta tras terminar una llamada.

{% hint style="info" %}
Este evento dependerá si tiene activada la opción de encuesta al final de una llamada.
{% endhint %}

El evento retornará dos argumentos, el primer corresponde un `object` con la encuesta y el segundo con la fecha en la cual se envió como `datetime`.

```javascript
videsk.addEventListener('onSurvey', ({ survey, date }) => {
    // Do something with survey and date
});
```



## onReconnected

Este evento permite escuchar cuando se ha reconectado a una llamada activa, ya sea porque se recargó o cerró la ventana del navegador/app móvil.

{% hint style="info" %}
Este evento dependerá si el widget carga junto con tu sitio.
{% endhint %}

El evento retornará la fecha en la cual se se ha reconectado como `datetime`.

```javascript
videsk.addEventListener('onReconnected', ({ date }) => {
    // Do something with survey and date
});
```

## onConnectionError

Este evento permite escuchar cuando existe errores en la conexión antes de la llamada.

{% hint style="info" %}
Puede ocurrir que nuestros servidores detecten que un usuario se está conectando desde una red o equipo sospechoso, realizando un bloqueo.
{% endhint %}

El evento retornará la fecha en la cual se se ha generad el error de conexión como `datetime`.

```javascript
videsk.addEventListener('onConnectionError', ({ date }) => {
    // Do something with survey and date
});
```

## onFormSubmission

Este evento permite escuchar cuando se envía un formulario ya sea previo a llamada, agendamiento o no disponible (contacto). Los argumentos son:

Llamada en vivo:

* `values`: valores del formulario
* `type`: tipo de formulario (`pre-call` o `contact`)
* `segment`: id del segmento
* `id`: id único del envío

Agendamiento:

* `values`: valores del formulario
* `startAt`: fecha y hora seleccionada
* `timezone`: zona horaria del usuario
* `service`: id del calendario
* `id`: id único del envío

```javascript
videsk.addEventListener('onFormSubmission', event => {
    // Do something with submission
});
```

## onDateSelected

Este evento permite escuchar cuando se selecciona una fecha y hora a agendar. Los argumentos son:

* `startAt`: fecha y hora seleccionada
* `timezone`: zona horaria del usuario

```javascript
videsk.addEventListener('onDateSelected', event => {
    // Do something with the selection
});
```

## onScheduled

Este evento permite escuchar cuando se agenda una hora en un calendario. Los argumentos son:

* `title`: título del evento
* `description`: descripción del evento
* `start`: fecha en la que inicia el evento
* `end`: fecha en la que finaliza el evento
* `duration`: duración del evento en minutos
* `url`: enlace desde donde se agendó
* `location`: ubicación
* `guests`: emails de invitados incluyendo usuario que agendó

```javascript
videsk.addEventListener('onScheduled', event => {
    // Do something with the appointment
});
```

## custom-event

Este evento se dispara cuando se ha configurado un segmento como evento, el cual contiene un payload como `Array` que dependerá de los valores ingresados, los cuales siempre serán `String`.

```javascript
document.addEventListener('custom-event', event => {
    const args = event.detail;
    // Do something with values as String
})
```
