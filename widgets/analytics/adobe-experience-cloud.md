---
cover: ../../.gitbook/assets/Adobe-Experience-Cloud-logo.jpg
coverY: 14.035092002467106
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

# Adobe Experience Cloud

Nuestro widget es compatible de forma nativa y por defecto con Adobe Experience Platform para analítica dentro de ellos están:

### Compatibles

* Adobe Experience Platform (Web SDK)
* Adobe Launch (Experience Platform Tags)
* Adobe Analytics (AppMeasurement)
* Adobe DTM (Dynamic Tag Manager)

### Incompatibles

* Adobe Target
* Adobe Audience Manager
* Adobe Campaign

{% hint style="success" %}
Las **incompatibilidades** hacen referencia a integración nativa, la cual puedes [suplir usando la propia API del widget](../api/).
{% endhint %}

#### Nomenclatura de eventos

A diferencia de los [eventos capturables a través de Javascript en tu sitio web](../api/eventos.md), con Adobe Experience Cloud la nomenclatura es similar pero sin el prefijo `on` y en minúsculas, es decir:

| Event name nativo | Event name GTM  |
| ----------------- | --------------- |
| onLoad            | videsk.load     |
| onSelected        | videsk.selected |
| onQueued          | videsk.queued   |

Puedes encontrar el listado de eventos disponibles en la siguiente página:

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}
