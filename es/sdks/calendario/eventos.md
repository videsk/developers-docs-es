---
description: >-
  Te explicamos cómo funcionan los eventos y qué hacer cuando estos son
  disparados.
---

# Eventos

## `days`

Este evento se dispara cuando se ha llamado al método `getDays`. El evento contiene los mismos valores de retorno que el método `getDays`.

```javascript
calendar.addEventListener('days', event => {
    const days = event.detail;
});
```

## `hours`

Este evento se dispara cuando se ha llamado al método `getHours`. El evento contiene los mismos valores de retorno que el método `getHours`.

```javascript
calendar.addEventListener('hours', event => {
    const hours = event.detail;
});
```

## `created`

Este evento se dispara cuando se ha llamado al método `create`. El evento contiene los mismos valores de retorno que el método `create`.

```javascript
calendar.addEventListener('created', event => {
    const response = event.detail;
});
```

## `canceled`

Este evento se dispara cuando se ha llamado al método `cancel`. El evento contiene los mismos valores de retorno que el método `cancel`.

```javascript
calendar.addEventListener('canceled', event => {
    const response = event.detail;
});
```

## `rescheduled`

Este evento se dispara cuando se ha llamado al método `reschedule`. El evento contiene los mismos valores de retorno que el método `reschedule`.

```javascript
calendar.addEventListener('rescheduled', event => {
    const response = event.detail;
});
```

## `join`

Este evento se dispara cuando se ha llamado al método `join`. El evento contiene el `accessToken` necesario para comenzar la videollamada.

{% hint style="info" %}
Con este evento deberás hacer uso de nuestro SDK de [WebRTC](../webrtc/#uso).
{% endhint %}

{% hint style="danger" %}
Recuerda que deberás escuchar el evento [hangup](../webrtc/metodos.md#addeventlistener) de WebRTC para terminar el llamado, usando el método [destroy](../webrtc/metodos.md#destroy). De lo contrario, la llamada seguirá activa.
{% endhint %}

```javascript
calendar.addEventListener('join', event => {
    const { accessToken } = event.detail;
    const webrtc = new WebRTC();
    await webrtc.create(accessToken);
});
```

{% content-ref url="../webrtc/" %}
[webrtc](../webrtc/)
{% endcontent-ref %}

## `modify`

Este evento se dispara cuando se ha llamado al método `modify`. El evento contiene la acción a realizar `action` y el token de aceso `accessToken`.

{% hint style="warning" %}
Es importante mantener siempre disponible `v-schedule-action` y `v-schedule-auth` en la URL, o bien las mismas keys pero en `localStorage`. De lo contrario no podremos detactar y emitir este evento.
{% endhint %}

```javascript
calendar.addEventListener('modify', event => {
    const { action, accessToken } = event;
});
```

En base a la acción, deberás mostrar la opción de cancelar o reagendar. La key `action` puede ser:

* `join`: Indica que se desea unir a la reunión
* `modify`: Indica que se desea modificar la cita

{% hint style="info" %}
Aquí deberás hacer uso del método `cancel` y `reschedule`.
{% endhint %}

