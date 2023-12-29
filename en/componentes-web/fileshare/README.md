---
description: >-
 We provide below the documentation for our File Upload Web Component.
---

# 🗃 Fileshare

This web component allows to ease the visual management of files that will be sent and received with just a few lines of code, without sacrificing the customization with HTML, CSS and JavaScript.

You can use the component without modifying or adding anything, or you can customize the file selection box, sending behavior, how to attach files and more.

First you will need to load the component as a script in the header of your site:

```html
<script src="https://cdn.videsk.io/sdk/fileshare.component.min.js"></script>
```

{% hint style="warning" %}
You must load the resources before using the `<videsk-fileshare>` component, otherwise it will be an element without the properties and methods. In addition, you should be careful with the `async` or `defer` attributes.
{% endhint %}

In order to customize this component you will only need to define it somewhere in your HTML code:

```html
<videsk-fileshare></videsk-fileshare>
```

Once you have defined the component you will be able to access it using `querySelector` or any HTML selector with JavaScript.

```javascript
const component = document.querySelector('videsk-fileshare');
```

Later you will be able to use its properties, slots, methods, and available events.