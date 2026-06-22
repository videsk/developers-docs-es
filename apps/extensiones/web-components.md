---
description: >-
  Como crear extensiones de tipo web component para la Consola de Videsk.
---

# Web Components

Las extensiones de tipo `web-component` cargan un modulo JavaScript que registra un Custom Element. El elemento se monta directamente en el DOM de la consola.

{% hint style="warning" %}
A diferencia de los iframes, los web components **comparten el contexto de ejecucion** con la consola. Esto implica mayor responsabilidad sobre la seguridad y estabilidad del codigo.
{% endhint %}

## Requisitos

1. El script debe servirse sobre **HTTPS**.
2. El script debe ser un **modulo ES** (`type="module"`).
3. Debe registrar un Custom Element con `customElements.define()`.
4. El `tagName` debe contener al menos un guion (ej. `my-app`, `acme-widget`).

## Esquema de configuracion

```json
{
  "name": "Mi Componente",
  "kind": "web-component",
  "placement": "call-panel",
  "segments": [],
  "webComponent": {
    "scriptUrl": "https://cdn.example.com/my-app.js",
    "tagName": "my-app",
    "integrity": "sha384-abc123..."
  },
  "contextScopes": ["user", "segment"]
}
```

### Campos de `webComponent`

| Campo | Tipo | Requerido | Descripcion |
| --- | --- | --- | --- |
| `scriptUrl` | String | Si | URL HTTPS del modulo JS |
| `tagName` | String | Si | Nombre del custom element (debe contener `-`) |
| `integrity` | String | No | Hash SRI para verificar integridad del script |

## Ciclo de vida

1. La consola crea un `<script type="module" src="...">` para cargar el bundle.
2. Espera a que `customElements.whenDefined(tagName)` resuelva.
3. Monta el elemento: `<my-app data-extension-id="..."></my-app>`.
4. Setea las propiedades de contexto como JS properties en el elemento.
5. Despacha un `CustomEvent('videsk:init', { detail: context })`.

## Contrato del Custom Element

El componente debe aceptar:

### Propiedades (JS)

El host intentara setear las propiedades de contexto directamente:

```js
element.user = { id: '...', email: '...' };
element.segment = { _id: '...', name: '...' };
element.call = { id: '...' };
```

Si la property no existe, se pasa como atributo HTML (JSON stringified).

### Evento `videsk:init`

```js
element.addEventListener('videsk:init', (event) => {
  const { user, segment, call } = event.detail;
  // Inicializar con el contexto del host
});
```

## Ejemplo minimo

```js
class MyApp extends HTMLElement {
  connectedCallback() {
    this.innerHTML = '<p>Cargando...</p>';
    this.addEventListener('videsk:init', (e) => {
      const { user, segment } = e.detail;
      this.innerHTML = `<p>Hola ${user.email} en ${segment.name}</p>`;
    });
  }
}

customElements.define('my-app', MyApp);
```

{% hint style="info" %}
El script se carga una sola vez aunque haya multiples extensiones con la misma `scriptUrl`. El cache es por URL.
{% endhint %}
