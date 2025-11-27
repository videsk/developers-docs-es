# Subcomponentes

A continuación, podrás encontrar detalles de nuestros subcomponentes utilizados dentro de nuestro componente web WebRTC.

## Chat

El componente web `videsk-chat` está presente dentro del shadow root de `videsk-webrtc`. Si deseas utilizar un posicionamiento exterior o similar, puedes utilizar la siguiente técnica:

#### 1. Ocultar chat

```css
videsk-webrtc::part(chart) {
    display: none !important;
}
```

#### 2. Añadir chat personalizado

```html
<body>
    <videsk-webrtc></videsk-webrtc>
    <videsk-chat></videsk-chat>
</body>
```

***

### Propiedades

Estas propiedades permiten cambiar el comportamiento de la UI y/o el lógico.

#### `active`

Esta propiedad permite determinar si el chat está activo o no, a partir de la clase active del mismo componente.

```html
<videsk-chat class="active"></videsk-chat>
<script>
  chat.active // true
</script>
```

***

### Métodos

Considera que todos los ejemplos asumen que `chat` es una variable que hace referencia al DOM `videsk-chat`.

```javascript
const chat = document.querySelector('videsk-chat');
```

#### `add`

Podrás añadir un mensaje en la interfaz de chat indicando los siguientes argumentos.

```javascript
webrtc.addEventListener('new-message', event => {
    const { message } = event.detail;
    chat.add(message, false);
});
```

| Argumento   | Tipo    | Descripción                                                   |
| ----------- | ------- | ------------------------------------------------------------- |
| `message`   | string  | Mensaje a enviar                                              |
| `local`     | boolean | Indica si el mensaje es local o remoto. (izquierda o derecha) |
| `emitEvent` | boolean | Indica si emite el evento de nuevo mensaje.                   |

***

### Eventos

Los siguientes eventos se disparan según el comportamiento de los mensajes y la interacción con la UI.&#x20;

#### `new-message`

Con este evento podrás escuchar cuando un nuevo mensaje es renderizado en el chat, ya sea manualmente o programáticamente.

```javascript
chat.addEventListener('new-message', event => {
    const { message, date, remote } = event.detail;
    // Do something
});
```

| Variable  | Tipo    | Descripción                                         |
| --------- | ------- | --------------------------------------------------- |
| `message` | string  | Mensaje en texto plano                              |
| `remote`  | boolean | Indica si el mensaje es remoto o local              |
| `date`    | date    | Indica la fecha en que se recibió/envió el mensaje. |

#### `unread-message`

Con este evento podrás escuchar cuando un nuevo mensaje se renderiza en el chat, pero no está visible para el participante, lo que indica la cantidad de mensajes sin leer.

{% hint style="info" %}
Este evento se emite ya sea que haya mensajes sin leer y, posteriormente, de leer, quedando en 0.
{% endhint %}

```javascript
chat.addEventListener('unread-message', event => {
    const { total } = event.detail;
    // Do something
});
```

| Variable | Tipo   | Descripción               |
| -------- | ------ | ------------------------- |
| `total`  | number | Total de mensaje sin leer |
