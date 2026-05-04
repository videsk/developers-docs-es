---
description: >-
  Protocolo de comunicacion entre el host (Consola Videsk) y las extensiones
  embebidas via iframe o web component.
---

# Protocolo postMessage

Las extensiones se comunican con la consola mediante un protocolo tipado. Para iframes se usa `window.postMessage`; para web components se usa `CustomEvent`.

## Handshake

Al cargar una extension, el host envia un mensaje de inicializacion:

### Host -> Extension

```json
{
  "type": "videsk:init",
  "context": {
    "user": { "id": "abc123", "email": "agent@company.com" },
    "segment": { "_id": "seg456", "name": "Ventas" },
    "call": { "id": "call789" }
  }
}
```

Los campos presentes en `context` dependen de los `contextScopes` configurados en la extension.

### Extension -> Host

La extension puede confirmar que esta lista:

```json
{
  "type": "videsk:ready"
}
```

Si la extension envia `videsk:ready` antes de recibir el init, el host reenviara el `videsk:init`.

## Mensajes de la extension al host

### `videsk:resize`

Solicita un cambio de altura del contenedor:

```json
{
  "type": "videsk:resize",
  "height": 450
}
```

`height` debe ser un numero (pixeles).

### `videsk:emit`

Envia un evento personalizado al host, que se reenvia al backend via socket:

```json
{
  "type": "videsk:emit",
  "event": "form:submitted",
  "payload": { "formId": "abc", "status": "success" }
}
```

En el backend, esto llega como `extension:message` por socket:

```json
{
  "extensionId": "ext_id",
  "event": "form:submitted",
  "payload": { "formId": "abc", "status": "success" }
}
```

## Seguridad

### Iframes

- El host **valida `event.origin`** contra la URL registrada de la extension. Mensajes de otros origenes son ignorados.
- Solo se procesan mensajes cuyo `type` empiece con `videsk:`.
- El iframe corre con `sandbox` y `allow` controlados por el backend.
- Se usa `referrerpolicy="no-referrer"` para no filtrar datos del host.

### Web Components

- Los eventos usan `bubbles: false` para no propagarse al DOM del host.
- El script se carga con `crossOrigin="anonymous"`.
- Opcionalmente se puede verificar integridad con SRI (`integrity`).

## Ejemplo: iframe escuchando el init

```html
<script>
window.addEventListener('message', (event) => {
  if (event.data && event.data.type === 'videsk:init') {
    const { user, segment, call } = event.data.context;
    document.getElementById('agent').textContent = user.email;
    // Confirmar que estamos listos
    event.source.postMessage({ type: 'videsk:ready' }, event.origin);
  }
});
</script>
```

## Ejemplo: iframe solicitando resize

```html
<script>
function notifyResize() {
  const height = document.body.scrollHeight;
  window.parent.postMessage({
    type: 'videsk:resize',
    height: height,
  }, 'https://console.videsk.io');
}

window.addEventListener('load', notifyResize);
new ResizeObserver(notifyResize).observe(document.body);
</script>
```
