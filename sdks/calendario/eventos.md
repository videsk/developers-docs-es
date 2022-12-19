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

Este evento se dispara cuando se ha llamado al método `connect`. El evento contiene los&#x20;
