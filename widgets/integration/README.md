---
description: >-
  Verás de forma breve como realizar la integración de nuestros widgets en tu
  sitio web.
---

# 🔌 Instalación

La forma base de integración es mediante un script.

## Script de integración

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/videsk-widget.min.js" videsk-token="REPLACE_TOKEN" async></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement("script");
script.src = "https://assets.videsk.io/js/videsk-widget.min.js";
script.setAttribute("videsk-token", "REPLACE_TOKEN");
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
🚧 Estamos trabajando para mover nuestra documentación. 🚧
{% endhint %}

Puedes acceder a la [documentación de API de nuestro widget desde aquí](https://docs.videsk.io/dashboard/integration/api-widget).
