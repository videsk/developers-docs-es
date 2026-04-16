---
description: >-
  Como configurar extensiones de tipo iframe en la Consola de Videsk,
  incluyendo permisos, sandbox y requisitos de seguridad.
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
  "segments": ["635c843f35f1254a417612d9"],
  "iframe": {
    "url": "https://app.example.com/embed",
    "allow": ["camera", "microphone", "clipboard-write"],
    "sandbox": ["allow-scripts", "allow-same-origin", "allow-forms"],
    "width": "100%",
    "height": "500px"
  },
  "contextScopes": ["user", "segment", "call"]
}
```

### Campos de `iframe`

| Campo | Tipo | Requerido | Descripcion |
| --- | --- | --- | --- |
| `url` | String | Si | URL HTTPS de la pagina a embeber |
| `allow` | String[] | No | Permisos del atributo `allow` del iframe |
| `sandbox` | String[] | No | Valores del atributo `sandbox` del iframe |
| `width` | String | No | Ancho CSS (default: `100%`) |
| `height` | String | No | Alto CSS (default: `100%`) |

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
  src="https://app.example.com/embed"
  allow="camera; microphone; display-capture; clipboard-write; autoplay"
  sandbox="allow-scripts allow-same-origin allow-forms allow-popups allow-popups-to-escape-sandbox allow-downloads"
  referrerpolicy="no-referrer"
  loading="lazy"
/>
```

## Segmentos

El campo `segments` controla en que segmentos aparece la extension:

- `[]` (vacio) = disponible en **todos** los segmentos de la cuenta
- `["id1", "id2"]` = solo disponible en esos segmentos

Esto permite que distintos equipos tengan extensiones diferentes segun su funcion.
