---
cover: ../../.gitbook/assets/image001.jpg
coverY: -1.2426938508686265
layout:
  width: default
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Google Analytics/Tag Manager

Nuestro widget es compatible de forma nativa y por defecto con los distintos productos de Google para analítica dentro de ellos están:

<table><thead><tr><th width="525.111083984375">Nombre</th><th data-type="checkbox">Compatibilidad</th></tr></thead><tbody><tr><td>Google Analytics 3 y 4 (<code>gtag</code>)</td><td>true</td></tr><tr><td>Google Analytics via GTM</td><td>true</td></tr><tr><td>Google Tag Manager</td><td>true</td></tr><tr><td>Google Ads</td><td>true</td></tr><tr><td>Universal Analytics (deprecado)</td><td>true</td></tr></tbody></table>

Para realizar medición de eventos equivalentes a interacciones de un usuario con el widget a través de Google Tag Manager debes seguir los siguientes pasos:

## Escuchar eventos

### 1. Crear `trigger`

Debe ir al menú lateral llamado **Triggers**.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Luego deberás dar crear un nuevo trigger desde el botón ![](<../../.gitbook/assets/image (71).png>). A continuación, selecciona el tipo de trigger llamado `Custom Event` en la categoría de Other.

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Luego en el campo Event name debes escribir `videsk.*` lo que capturará todos los eventos. Recuerda que deberás activar la opción Use regex matching.

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
En caso que no desees escuchar todos los eventos, deberás escribir el evento manualmente como `videsk.toggle`, `videsk.load`, `videsk.selected`, etc.
{% endhint %}

#### Nomenclatura de eventos

A diferencia de los [eventos capturables a través de Javascript en tu sitio web](../api/eventos.md), con Google Tag Manager la nomenclatura es similar pero sin el prefijo `on` y en minúsculas, es decir:

| Event name nativo | Event name GTM  |
| ----------------- | --------------- |
| onLoad            | videsk.load     |
| onSelected        | videsk.selected |
| onQueued          | videsk.queued   |

Puedes encontrar el listado de eventos disponibles en la siguiente página:

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

Finalmente, debes asegurarte de que el trigger se ha creado correctamente:

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

### 2. Crear etiqueta (tag)

Ahora simplemente deberás crear tu etiqueta pero en el caso de trigger deberás seleccionar el tigger custom event que haz creado previamente.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Finalmente, basado en tus necesidad podrás enviar esta información hacia Google Analytics o cualquier otra plataforma/integración que requieras.
