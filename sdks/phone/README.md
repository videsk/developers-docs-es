---
description: Personaliza la experiencia de tus usuarios con Phone.
---

# 📞 Phone

Con `Phone` podrás crear llamadas de forma programática, sin necesidad de preocuparte por las conexiones, parámetros, excepciones, etc.

Phone es compatible con cualquier ambiente y framework, ya sea nativo, Svelte, Vue, React, Angular, etc.

## Instalación

Para comenzar deberás instalar nuestro recurso en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/sdk/phone.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://assets.videsk.io/js/sdk/phone.min.js";
document.body.appendChild('body'); // O reemplaza con el nodo DOM que desees
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
No almacenes el contenido del script en tu servidor, **esto infringe nuestros términos de uso**.
{% endhint %}

{% hint style="danger" %}
Por seguridad y calidad de servicio tenemos un límite de peticiones por segundo por IP/Token, que consta de 20 peticiones en 1 segundo. Evita superar este límite, ya que nuestra Rest API bloqueará las peticiones de tus clientes.
{% endhint %}

## Instanciación

Primero deberás instanciar `VideskPhone` como un [constructor](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Classes/constructor).

```javascript
const phone = new VideskPhone(APIToken);
```

En la variable `phone` podrás acceder a los métodos y propiedades.

{% hint style="info" %}
Si instancias `VideskPhone`sin un token automáticamente intentará extraerlo de la URL, por lo que podrás utilizar `token`, `videsk-token` o `api-key` como parámetro en la URL.&#x20;
{% endhint %}

```
https://example.com?api-key=eyJhbGciOiJIUzI1NiIsI...
```

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Métodos</strong></td><td>Listado de métodos disponibles en Phone.</td><td></td><td><a href="eventos.md">eventos.md</a></td></tr><tr><td><strong>Eventos</strong></td><td>Listado de eventos disponibles en Phone.</td><td></td><td><a href="eventos.md">eventos.md</a></td></tr></tbody></table>
