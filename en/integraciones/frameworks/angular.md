---
description: How to use our development kit or SDK with Angular.
---

# Angular

The methods of integration in Angular will largely depend on the version and architecture, so the examples below will focus on maximizing efficiency in importation and availability throughout the code.

## Single App

If you are developing with Angular as a SPA, we suggest adding our SDKs as JS dependencies in the `index.html` file.

```html
<head>
  ...
  <script src="https://cdn.videsk.io/sdk/webrtc.min.js"></script>
  ...
</head>
```

## Microfrontend

If you are developing with Angular based on a microfrontend architecture, the best way is to create a `scripts.js` or `dependencies.js` file that contains the necessary imports.

This way, you can import the dependencies with tree-shaking, and the bundle file will exclude dependencies, which will only load when necessary.

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

## Declare Web Component

To use our web components, you can create an Angular component within your application and then associate it with our web component.

{% hint style="info" %}
You will need to load the component from our CDN in your `index.html`.
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