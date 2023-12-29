---
description: Cómo usar nuestros kit de desarrollo o SDK con Angular.
---

# Angular

Los métodos de integración en Angular dependerán en gran medida de la versión y arquitectura, por lo que los ejemplos a continuación se centrarán en máxima eficiencia en la importación y disponibilidad a través del código.

## Single App

En caso que estés desarrollando con Angular como SPA, te sugerimos añadir nuestros SDKs como dependencias JS en el archivo `index.html`.

```html
<head>
  ...
  <script src="https://cdn.videsk.io/sdk/webrtc.min.js"></script>
  ...
</head>
```

## Microfrontend

Si estás desarrollando con Angular basado en arquitectura microfrontend, la mejor forma es crear un archivo `scripts.js` o `dependencies.js` que contenga las importaciones necesarias.

De esta manera, podrás importar las dependencies con tree-shaking, y el archivo bundle excluirá las dependencias las cuales cargarán solo cuando sean necesarias.

{% code title="scripts.js" %}
```javascript
import WebRTC from 'https://cdn.videsk.io/sdk/webrtc.min.js';
import Calendar from 'https://cdn.videsk.io/sdk/calendar.min.js';

export { WebRTC, Calendar };
```
{% endcode %}

{% code title="app.component.ts" %}
```javascript
import { Component } from '@angular/core';
import { WebRTC, Calendar } from 'path/to/scripts.js';

@Component({
  selector: 'app-root',
  template: '<p>{{ message }}</p>',
})
export class AppComponent {
  message: string;

  constructor() {
    const webrtc = new WebRTC('JWT');
    const calendar = new Calendar();
  }
}
```
{% endcode %}

## Declarar componente web

Para usar nuestros componentes web puedes crear un componente Angular dentro de tu aplicación y luego asociarlo a nuestro componente web.

{% hint style="info" %}
Deberás cargar el componente desde nuestra CDN en tu `index.html`.
{% endhint %}

```javascript
import { Component, AfterViewInit } from '@angular/core';

declare const WebRTC: any;

@Component({
  selector: 'app-videsk-webrtc',
  template: '<videsk-webrtc></videsk-webrtc>'
})
export class MyComponent implements AfterViewInit {
  ngAfterViewInit() {
    new WebRTC(accessToken);
  }
}
```
