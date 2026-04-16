---
description: >-
  Como configurar extensiones de tipo iframe en la Consola de Videsk,
  incluyendo permisos, sandbox, templating dinamico de URL y requisitos de
  seguridad.
---

# Iframe

Las extensiones de tipo `iframe` cargan una pagina web externa dentro de un iframe aislado. Es el mecanismo recomendado para la mayoria de integraciones.

## Requisitos

### HTTPS obligatorio

La URL de la extension **debe** servirse sobre `https://`. Contenido HTTP sera bloqueado por el navegador.

### Content-Security-Policy

Tu aplicacion debe permitir ser embebida por los dominios de Videsk:

```
Content-Security-Policy: frame-ancestors 'self' https://*.videsk.io;
```

Si tu app usa `X-Frame-Options`, eliminalo a favor de CSP.

### Cookies

Si la app embebida requiere sesion con cookies:

```
Set-Cookie: session=xxx; SameSite=None; Secure; HttpOnly
```

Si usa `localStorage` o `sessionStorage`, no es necesario.

## Esquema de configuracion

Al crear una extension via `POST /extensions`:

```json
{
  "name": "Mi App",
  "kind": "iframe",
  "placement": "call-panel",
  "iframe": {
    "url": "https://app.example.com/embed?call={{encode call.id}}&agent={{encode user.email}}",
    "allow": ["camera", "microphone", "clipboard-write"],
    "sandbox": ["allow-scripts", "allow-same-origin", "allow-forms"],
    "width": "100%",
    "height": "500px"
  },
  "contextScopes": ["user", "segment", "call"]
}
```

Luego, asocia la extension al segmento o servicio (calendario) que corresponda:

```
PATCH /segments/:id
{ "extensions": ["<extension_id>"] }
```

```
PATCH /services/:id
{ "extensions": ["<extension_id>"] }
```

### Campos de `iframe`

| Campo | Tipo | Requerido | Descripcion |
| --- | --- | --- | --- |
| `url` | String | Si | URL HTTPS, admite templating handlebars |
| `allow` | String[] | No | Permisos del atributo `allow` del iframe |
| `sandbox` | String[] | No | Valores del atributo `sandbox` del iframe |
| `width` | String | No | Ancho CSS (default: `100%`) |
| `height` | String | No | Alto CSS (default: `100%`) |

## Templating dinamico de URL

El campo `iframe.url` admite expresiones [handlebars](https://handlebarsjs.com/) que se resuelven en la Consola justo antes de montar el iframe, usando el contexto de la llamada activa.

### Variables disponibles

| Variable | Descripcion |
| --- | --- |
| `user.id` | ID del agente que contesta |
| `user.email` | Email del agente |
| `user.firstname`, `user.lastname` | Nombre del agente |
| `segment._id`, `segment.name` | Segmento de la llamada |
| `call.id` | ID de la llamada |
| `account` | ID de la cuenta |
| `extraData.*` | Datos extra del cliente (IP, browser, location, etc.) |
| `form` | Valores del formulario base (completado por el cliente) |
| `agentForm` | Valores del formulario del agente |
| `tags` | Tags asociados a la llamada |

### Helpers

Se registran automaticamente todos los helpers del paquete `@videsk/handlebars-helpers` (los mismos que usan los webhooks: `#if`, `#each`, `#date`, `#phone`, `#jwt`, etc.).

Adicionalmente, para templating de URL:

| Helper | Descripcion |
| --- | --- |
| `{{encode valor}}` | URL-encode del valor (alias: `{{urlEncode valor}}`) |

{% hint style="warning" %}
La URL se compila con `noEscape: true` (sin HTML-escaping) porque no es HTML. Usa siempre `{{encode ...}}` en valores que puedan contener caracteres reservados en URLs (`&`, `=`, `?`, `/`, espacios, etc.).
{% endhint %}

### Ejemplos

```
https://app.ejemplo.com/embed?
  call={{encode call.id}}
  &agent={{encode user.email}}
  &segmento={{encode segment.name}}
  &ip={{encode extraData.ip}}
```

```
https://crm.ejemplo.com/contactos/{{encode call.id}}?rut={{encode form.rut}}
```

### Cuando se resuelve

La URL se resuelve **una sola vez** al momento de montar el iframe (inicio de la llamada o al habilitarse la extension). No se recompila cuando cambian valores reactivos (por ejemplo, mientras el agente llena el `agentForm`).

Si necesitas enviar datos a la app embebida en tiempo real durante la llamada, usa el protocolo `postMessage`.

## Permisos `allow`

Valores aceptados por el backend (otros seran rechazados):

| Valor | Descripcion |
| --- | --- |
| `camera` | Acceso a la camara |
| `microphone` | Acceso al microfono |
| `display-capture` | Captura de pantalla |
| `clipboard-write` | Escritura en clipboard |
| `clipboard-read` | Lectura de clipboard |
| `autoplay` | Reproduccion automatica de audio/video |
| `fullscreen` | Modo pantalla completa |
| `geolocation` | Acceso a ubicacion |
| `picture-in-picture` | Modo picture-in-picture |

**Valores por defecto** (si no se especifican):

```
camera; microphone; display-capture; clipboard-write; autoplay
```

## Permisos `sandbox`

Valores aceptados:

| Valor | Descripcion |
| --- | --- |
| `allow-scripts` | Ejecucion de JavaScript |
| `allow-same-origin` | Acceso a recursos del mismo origen |
| `allow-forms` | Envio de formularios |
| `allow-popups` | `window.open()` y links `target="_blank"` |
| `allow-popups-to-escape-sandbox` | Popups sin restricciones de sandbox |
| `allow-downloads` | Descargas de archivos |
| `allow-modals` | `alert()`, `confirm()`, `prompt()` |

**Valores por defecto:**

```
allow-scripts allow-same-origin allow-forms allow-popups allow-popups-to-escape-sandbox allow-downloads
```

{% hint style="warning" %}
Valores como `allow-top-navigation` no son aceptados por seguridad, ya que permitirian a la extension navegar la ventana principal.
{% endhint %}

## HTML renderizado

El iframe resultante en la consola sera similar a:

```html
<iframe
  src="https://app.example.com/embed?call=68123abc&agent=matias%40videsk.io"
  allow="camera; microphone; display-capture; clipboard-write; autoplay"
  sandbox="allow-scripts allow-same-origin allow-forms allow-popups allow-popups-to-escape-sandbox allow-downloads"
  referrerpolicy="no-referrer"
  loading="lazy"
/>
```

## Asociacion por entidad

Las extensiones se asocian a **segmentos** y/o **servicios** (calendarios) desde la propia entidad:

```
PATCH /segments/:segmentId
{ "extensions": ["ext_id_1", "ext_id_2"] }
```

```
PATCH /services/:serviceId
{ "extensions": ["ext_id_1"] }
```

Una misma extension puede estar asociada a multiples segmentos y servicios. Cada entidad controla que extensiones tiene habilitadas, lo que permite configuraciones flexibles por equipo o tipo de calendario.
