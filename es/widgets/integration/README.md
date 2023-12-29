---
description: >-
  Verás de forma breve como realizar la integración de nuestros widgets en tu
  sitio web.
---

# 🔌 Instalación

La forma base de integración es mediante un script. Este script carga recursos necesarios para renderizar el widget los cuales se componen de HTML, CSS y Javascript.

## Script de integración

{% hint style="info" %}
No somos compatibles con [SRI (Subresource Integrity)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource\_Integrity), de lo contrario no podríamos ofrecer actualizaciones y mejoras de forma constante los cuales son cada semana.
{% endhint %}

{% embed url="https://www.loom.com/share/68ea3f599d9f4c7cad50f126cd5b37cd?sid=cb16d1fa-f5c2-4cc1-b206-5d5477afc017" %}

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

Puedes acceder a la documentación de nuestra API en el siguiente enlace:

{% content-ref url="../api/" %}
[api](../api/)
{% endcontent-ref %}
