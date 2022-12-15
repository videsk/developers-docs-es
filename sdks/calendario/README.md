---
description: Te explicamos como usar nuestro SDK de Calendario
---

# 📅 Calendario

Con este SDK podrás embeber y diseñar de forma programática calendarios para agendar, sin necesidad de preocuparte por las conexiones, parámetros, excepciones, etc.

Es decir, hemos creado este "enchufe" para llegar y usar de forma sencilla y una estructura de rápido aprendizaje, pero sin dejar de lado la flexibilidad y poder de nuestra API.

{% hint style="info" %}
Este SDK no provee interfaz, es decir, no hay código HTML, por lo que deberás manejar tu propia interfaz, ya sea en HTML puro, Javascript o con frameworks como Vue, React, Angular, Svelte, etc.
{% endhint %}

## Instalación

Para comenzar deberás instalar nuestro recurso en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
```html
<script src="https://cdn.videsk.io/sdk/calendar.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/calendar.min.js";
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

## Instanciar

Lo primero que debes hacer es instanciar una clase `Calendar`. El primer argumento corresponden al token de integración que obtienes de tu cuenta.

```javascript
const calendar = new Calendar(token);
```

Posteriormente puedes acceder a sus métodos y propiedades.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Métodos</strong></td><td>Conoce cómo usar los métodos de Calendar SDK.</td><td></td><td><a href="metodos.md">metodos.md</a></td><td></td></tr><tr><td><strong>Propiedades</strong></td><td>Conoce cuáles son las propiedades de Calendar SDK.</td><td></td><td><a href="propiedades.md">propiedades.md</a></td><td></td></tr></tbody></table>
