---
description: >-
  Auto-resize del iframe y emisión de eventos de negocio al host usando el
  broker como canal continuo.
---

# Eventos en vivo

Este ejemplo cubre el [Patrón B](../broker.md#patron-b-broker-como-canal-continuo): la app conversa con el host durante toda la atención.

Casos típicos:

* La altura de tu UI cambia (un acordeón se abre, llega un resultado de búsqueda) y quieres que el iframe se ajuste.
* Tu app realiza una acción que el agente o un sistema externo quiere registrar como parte de la llamada (por ejemplo, "se creó un ticket"; "se actualizó el contacto").

## Auto-resize

Reporta la nueva altura cada vez que el contenido cambia, **no** en un setInterval.

```js
const sendHeight = () => {
  window.parent.postMessage({
    type: 'videsk:resize',
    height: document.documentElement.scrollHeight,
  }, '*');
};

new ResizeObserver(sendHeight).observe(document.documentElement);
window.addEventListener('load', sendHeight);
```

## Emitir un evento de negocio

```js
function onTicketCreated(ticket) {
  window.parent.postMessage({
    type: 'videsk:emit',
    event: 'ticket.created',
    payload: {
      id: ticket.id,
      url: ticket.url,
      priority: ticket.priority,
    },
  }, '*');
}
```

Reglas para `videsk:emit`:

* `event` es un string libre que tú defines. Usa nombres con namespace (`ticket.created`, `lead.updated`) para no chocar con futuros eventos del propio Videsk.
* `payload` debe ser serializable a JSON.
* No esperes respuesta del host: `videsk:emit` es _fire-and-forget_.

## Ejemplo completo

```html
<!doctype html>
<html>
<body>
  <button id="create">Crear ticket</button>
  <ul id="log"></ul>

  <script>
    const TRUSTED = ['https://console.videsk.io', 'https://app.videsk.io'];
    let ctx = null;

    const post = (msg) => window.parent.postMessage(msg, '*');

    const sendHeight = () => post({
      type: 'videsk:resize',
      height: document.documentElement.scrollHeight,
    });

    new ResizeObserver(sendHeight).observe(document.documentElement);

    document.getElementById('create').addEventListener('click', async () => {
      const ticket = await fakeCreateTicket(ctx);
      const li = document.createElement('li');
      li.textContent = `Ticket ${ticket.id}`;
      document.getElementById('log').appendChild(li);

      post({
        type: 'videsk:emit',
        event: 'ticket.created',
        payload: { id: ticket.id, callId: ctx.call?.id },
      });
    });

    window.addEventListener('message', (event) => {
      if (!TRUSTED.includes(event.origin)) return;
      if (event.data?.type !== 'videsk:init') return;
      ctx = event.data.context;
    });

    post({ type: 'videsk:ready' });

    async function fakeCreateTicket(ctx) {
      return { id: 'TCK-' + Math.random().toString(36).slice(2, 8) };
    }
  </script>
</body>
</html>
```
