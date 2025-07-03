---
description: Te explicamos las mejoras prácticas para usar Chrome o Chromium en modo kiosko
---

# Chrome/Chromium

### Windows

#### Chrome:

```batch
"C:\Program Files\Google\Chrome\Application\chrome.exe" ^
  --kiosk ^
  --autoplay-policy=no-user-gesture-required ^
  --disable-features=MediaEngagementBypassAutoplayPolicies ^
  --disable-background-media-suspend ^
  --disable-web-security ^
  --disable-infobars ^
  --disable-notifications ^
  --disable-session-crashed-bubble ^
  --disable-restore-session-state ^
  --no-first-run ^
  --incognito ^
  --start-maximized ^
  "https://tu-aplicacion.com"
```

#### Chromium:

```batch
"C:\Program Files\Chromium\Application\chrome.exe" ^
  --kiosk ^
  --autoplay-policy=no-user-gesture-required ^
  --disable-features=MediaEngagementBypassAutoplayPolicies ^
  --disable-background-media-suspend ^
  --disable-web-security ^
  --disable-infobars ^
  --disable-notifications ^
  --disable-session-crashed-bubble ^
  --disable-restore-session-state ^
  --no-first-run ^
  --incognito ^
  --start-maximized ^
  "https://tu-aplicacion.com"
```

### macOS

#### Chrome:

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --kiosk \
  --autoplay-policy=no-user-gesture-required \
  --disable-features=MediaEngagementBypassAutoplayPolicies \
  --disable-background-media-suspend \
  --disable-web-security \
  --disable-infobars \
  --disable-notifications \
  --disable-session-crashed-bubble \
  --disable-restore-session-state \
  --no-first-run \
  --incognito \
  --start-maximized \
  "https://tu-aplicacion.com"
```

#### Chromium:

```bash
/Applications/Chromium.app/Contents/MacOS/Chromium \
  --kiosk \
  --autoplay-policy=no-user-gesture-required \
  --disable-features=MediaEngagementBypassAutoplayPolicies \
  --disable-background-media-suspend \
  --disable-web-security \
  --disable-infobars \
  --disable-notifications \
  --disable-session-crashed-bubble \
  --disable-restore-session-state \
  --no-first-run \
  --incognito \
  --start-maximized \
  "https://tu-aplicacion.com"
```

### Linux

#### Chrome:

```bash
google-chrome \
  --kiosk \
  --autoplay-policy=no-user-gesture-required \
  --disable-features=MediaEngagementBypassAutoplayPolicies \
  --disable-background-media-suspend \
  --disable-web-security \
  --disable-infobars \
  --disable-notifications \
  --disable-session-crashed-bubble \
  --disable-restore-session-state \
  --no-first-run \
  --incognito \
  --start-maximized \
  "https://tu-aplicacion.com"
```

#### Chromium:

```bash
chromium-browser \
  --kiosk \
  --autoplay-policy=no-user-gesture-required \
  --disable-features=MediaEngagementBypassAutoplayPolicies \
  --disable-background-media-suspend \
  --disable-web-security \
  --disable-infobars \
  --disable-notifications \
  --disable-session-crashed-bubble \
  --disable-restore-session-state \
  --no-first-run \
  --incognito \
  --start-maximized \
  "https://tu-aplicacion.com"
```

### Explicación de los parámetros clave

#### Para autoplay:

* `--autoplay-policy=no-user-gesture-required`: Permite autoplay sin interacción del usuario
* `--disable-features=MediaEngagementBypassAutoplayPolicies`: Desactiva las políticas de engagement
* `--disable-background-media-suspend`: Evita que se suspendan los medios en segundo plano

#### Para modo kiosko:

* `--kiosk`: Modo pantalla completa sin interfaz del navegador
* `--disable-infobars`: Elimina las barras informativas
* `--disable-notifications`: Desactiva notificaciones
* `--disable-session-crashed-bubble`: Elimina el aviso de sesión crasheada
* `--disable-restore-session-state`: No restaura sesiones anteriores
* `--no-first-run`: Omite la configuración inicial
* `--incognito`: Modo incógnito (opcional, pero útil para kioscos)
* `--start-maximized`: Inicia maximizado

### Scripts de automatización

#### Windows (.bat):

```batch
@echo off
echo Iniciando Chrome en modo kiosko...
"C:\Program Files\Google\Chrome\Application\chrome.exe" --kiosk --autoplay-policy=no-user-gesture-required --disable-features=MediaEngagementBypassAutoplayPolicies --disable-background-media-suspend --disable-web-security --disable-infobars --disable-notifications --disable-session-crashed-bubble --disable-restore-session-state --no-first-run --incognito --start-maximized "https://tu-aplicacion.com"
```

#### Linux/macOS (.sh)

```bash
#!/bin/bash
echo "Iniciando Chrome en modo kiosko..."
google-chrome \
  --kiosk \
  --autoplay-policy=no-user-gesture-required \
  --disable-features=MediaEngagementBypassAutoplayPolicies \
  --disable-background-media-suspend \
  --disable-web-security \
  --disable-infobars \
  --disable-notifications \
  --disable-session-crashed-bubble \
  --disable-restore-session-state \
  --no-first-run \
  --incognito \
  --start-maximized \
  "https://tu-aplicacion.com"
```

{% hint style="warning" %}
Recuerda que algunos de estos parámetros (como `--disable-web-security`) pueden tener implicaciones de seguridad, por lo que son apropiados para entornos controlados como kioscos, pero no para navegación general.
{% endhint %}
