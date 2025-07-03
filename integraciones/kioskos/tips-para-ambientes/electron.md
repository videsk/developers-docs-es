---
description: >-
  A continuación, podrás encontrar las mejores prácticas para integrar con apps
  Electron.
---

# Electron

## Politicas de autoplay

Electron al estar basado en Chromium trae consigo la política de autoreproducción restringida, que limita reproducir videos y audios solo cuando existe un clic por parte de un usuario.

Por ello, recomendamos desactivar esta restricción de la siguiente manera:

### Opción 1 (BrowserWindow)

{% code lineNumbers="true" %}
```javascript
const { BrowserWindow } = require('electron');

const mainWindow = new BrowserWindow({
  width: 1200,
  height: 800,
  webPreferences: {
    // Desactiva las políticas de autoplay
    autoplayPolicy: 'no-user-gesture-required',
  }
});
```
{% endcode %}

### Opción 2 (commandLine)

{% code lineNumbers="true" %}
```javascript
const { app } = require('electron');

app.commandLine.appendSwitch('autoplay-policy', 'no-user-gesture-required');
app.commandLine.appendSwitch('disable-features', 'MediaEngagementBypassAutoplayPolicies');
app.commandLine.appendSwitch('disable-background-media-suspend');
```
{% endcode %}

