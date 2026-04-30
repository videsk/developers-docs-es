---
description: >-
  Campos que defines al registrar una app en Videsk y cómo afectan la forma
  en que se renderiza tu web embebida.
---

# Configuración

Cada app se define con un objeto JSON con la siguiente forma:

```jsonc
{
  "name": "Ticket lookup",
  "kind": "iframe",
  "placement": "sidebar",
  "icon": "appstore-o",
  "iframe": {
    "url": "https://apps.example.com/lookup?call={{call.id}}&email={{encode form.email}}",
    "width": 40,
    "allow": ["camera", "microphone"],
    "sandbox": ["allow-scripts", "allow-same-origin"]
  },
  "contextScopes": ["user", "segment", "call", "form"]
}
```

## Campos generales

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `name` | `string` | Nombre visible en el launcher de la consola. |
| `kind` | `"iframe"` | Tipo de app. Esta documentación cubre `iframe`. |
| `placement` | `"call-panel" \| "sidebar" \| "standalone"` | Dónde se renderiza. Ver [Introducción](introduccion.md#tipos-de-app-y-donde-se-renderizan). |
| `icon` | `string` | Nombre del icono o URL de imagen para el launcher. |
| `contextScopes` | `string[]` | Qué partes del contexto se envían a la app (ver más abajo). |

## Bloque `iframe`

Aplica cuando `kind: "iframe"`.

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `iframe.url` | `string` | URL de tu app. Admite variables [Handlebars](plantillas.md). |
| `iframe.width` | `number` | Solo para `placement: "sidebar"`. Ancho del drawer en porcentaje del viewport (rango permitido `35`–`100`). |
| `iframe.allow` | `string[]` | Lista de permisos que se aplican al atributo `allow` del iframe. Ver defaults abajo. |
| `iframe.sandbox` | `string[]` | Lista de tokens del atributo `sandbox`. Ver defaults abajo. |

### Defaults

Si no defines `allow` o `sandbox`, la consola usa estos valores:

```html
<iframe
  src="https://tu-app.com/embed"
  allow="camera; microphone; display-capture; clipboard-write; autoplay"
  sandbox="allow-scripts allow-same-origin allow-forms allow-popups allow-popups-to-escape-sandbox allow-downloads"
  referrerpolicy="no-referrer"
  loading="lazy"
></iframe>
```

Solo declara `allow`/`sandbox` cuando necesites un set distinto al default. Si lo declaras, **reemplaza** al default; no se mezcla.

{% hint style="warning" %}
Tu URL **debe** servirse por HTTPS. Contenido sobre `http://` será bloqueado por el navegador.
{% endhint %}

## `contextScopes`

Determina qué bloques del contexto recibe tu app, tanto en las variables Handlebars de la URL como en el payload del broker.

```json
"contextScopes": ["user", "segment", "call", "form"]
```

Si no defines `contextScopes`, el valor por defecto es `["user", "segment"]`. Pide solo los scopes que realmente uses: lo que no declaras, no viaja.

| Scope | Incluye |
| --- | --- |
| `user` | Datos del agente autenticado (`id`, `email`, metadata). |
| `account` | `account.id` del tenant. |
| `segment` | Segmento de la llamada. |
| `branch`, `poc` | Datos de QMS si aplican. |
| `call` | Datos de la llamada (`id`, `startedAt`, etc.). |
| `appointment`, `service` | Datos de la reunión, cuando aplica. |
| `form` | Respuestas del formulario del cliente. |
| `agentForm` | Respuestas del formulario del agente. |
| `tags`, `selectedTags` | Etiquetas configuradas / seleccionadas. |
| `extraData`, `integrationData` | Datos extra del widget o de integraciones. |

El detalle de cada campo está en [Plantillas y contexto](plantillas.md).

## Requisitos de la URL

Tu URL debe cumplir, además de HTTPS:

* Permitir ser embebida desde los dominios de Videsk vía `Content-Security-Policy: frame-ancestors`. Detalles en [Iframes](integraciones/iframes.md).
* Si tu app requiere cookies de sesión, configurarlas con `SameSite=None; Secure`.
