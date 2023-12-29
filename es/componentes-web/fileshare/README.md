---
description: >-
  A continuación, proveemos la documentación para nuestro componente web de
  envíos de archivos.
---

# 🗃 Fileshare

Este componente web permite facilitar la gestión visual de los archivos que se vayan a enviar y recibir con muy pocas líneas de código, pero sin dejar de lado la personalización con HTML, CSS y Javascript.

Podrás usar el componente sin necesidad de modificar o añadir nada, o bien personalizar la caja de selección de archivos, comportamiento de envío, cómo adjuntar archivos y mucho más.

Primero deberás cargar el componente en la cabecera de tu sitio web como script:

```html
<script src="https://cdn.videsk.io/sdk/fileshare.component.min.js"></script>
```

{% hint style="warning" %}
Debes cargar el recurso antes de usar el componente `<videsk-fileshare>`, de lo contario será un elemento sin las propiedades y métodos. Además, debes tener cuidado con los atributos `async` o `defer`.
{% endhint %}

Para poder personalizar este componente solo deberás definirlo en alguna parte de tu código HTML:

```html
<videsk-fileshare></videsk-fileshare>
```

Una vez que has definido el componente podrás acceder a el mediante `querySelector` o cual selector HTML con Javascript.

```javascript
const component = document.querySelector('videsk-fileshare');
```

Posteriormente podrás hacer uso de sus propiedades, slots, métodos y eventos disponibles.



