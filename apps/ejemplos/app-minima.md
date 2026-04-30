---
description: >-
  Una app embebida en menos de 30 líneas: handshake con el broker y render
  del contexto recibido.
---

# App mínima

Este ejemplo es el "Hello World" de una app Videsk. Hace tres cosas:

1. Anuncia al host que está lista.
2. Recibe el contexto inicial.
3. Lo renderiza.

Servi este HTML desde `https://tu-app.com/embed` (HTTPS obligatorio) y confíguralo como `iframe.url` en tu app.

```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <title>Mi app Videsk</title>
  <style>
    body { font-family: system-ui, sans-serif; padding: 1rem; margin: 0; }
    pre  { background: #f4f4f5; padding: .75rem; border-radius: 6px; }
  </style>
</head>
<body>
  <h1>Contexto de la llamada</h1>
  <div id="status">Esperando contexto…</div>
  <pre id="ctx"></pre>

  <script>
    const TRUSTED_ORIGINS = [
      'https://console.videsk.io',
      'https://app.videsk.io',
    ];

    window.addEventListener('message', (event) => {
      if (!TRUSTED_ORIGINS.includes(event.origin)) return;
      if (event.data?.type !== 'videsk:init') return;

      const { context } = event.data;
      document.getElementById('status').textContent =
        `Hola ${context.user?.email ?? 'agente'}, segmento ${context.segment?.name ?? '-'}`;
      document.getElementById('ctx').textContent =
        JSON.stringify(context, null, 2);
    });

    // Anuncia al host que estamos listos para recibir el init.
    window.parent.postMessage({ type: 'videsk:ready' }, '*');
  </script>
</body>
</html>
```

## Configuración mínima en Videsk

```jsonc
{
  "name": "Mi app",
  "kind": "iframe",
  "placement": "sidebar",
  "iframe": { "url": "https://tu-app.com/embed" },
  "contextScopes": ["user", "segment", "call", "form"]
}
```

## Qué probar

* Verifica en la consola del navegador del agente que se imprime el `videsk:init`.
* Cambia `contextScopes` y recarga: solo deberían aparecer los bloques que declaraste.
* Cierra la llamada: el iframe debe destruirse.
