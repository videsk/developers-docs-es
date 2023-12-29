---
description: Descubre como realizar la integración con kioskos físicos
---

# Kioskos

## Modo kiosko en Chrome

Activar el modo kiosko de Google Chrome evitará que usuarios puedan minimizar o cerrar el navegador.

{% hint style="info" %}
Los siguientes comandos funcionan en cualquier navegador basado en Chromium como Chrome, Edge, Opera, Brave, etc.
{% endhint %}

El siguiente comando es un ejemplo que contiene los argumentos como:

* `--kiosk`, abrirá Chrome con funciones de interacción limitadas
* `--fullscreen`, abrirá Chrome en pantalla completa
* `-tab`, indicará que sitio web deberá abrir&#x20;

{% code title="Ejemplo" %}
```
[ruta o comando chrome] --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

{% hint style="warning" %}
Recuerda reemplazar `https://example.com` con la URL del sitio donde esté la integración.
{% endhint %}

{% hint style="danger" %}
No incluyes enlaces a sitios externos, ya que se abrirán en otra pestaña dificultando el regreso al sitio original.
{% endhint %}

### Windows

```
start chrome.exe --kiosk --fullscreen -tab https://example.com
```

#### Ejecutar al inicio de Windows (Opcional)

Si deseas que Chrome se abra cada vez que Windows se inicie, deberás añadir este archivo de la siguente manera:

1. Abre menú de Windows y abre "Ejecutar" o bien apreta las teclas Windows + R
2. Escribe `Shell:startup`
3. Descarga este archivo en la carpeta abierta:

{% file src="../.gitbook/assets/kiosk.cmd" %}

{% hint style="info" %}
En caso que no puedas descargar el archivo por bloqueos de seguridad en la red, abre un block de notas, pega el siguiente contenido, pégalo y guárdalo con el nombre `kiosk.cmd`.



**Deberás asegurarte de guardar con la extensión "Todos los archivos", no como `.txt`**
{% endhint %}

{% code title="Contenido archivo .CMD" %}
```batch
@echo off
start chrome --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

4\. Abre el archivo con block de notas, cambia la URL por tu sitio web y guarda los cambios.

5\. Listo! Reinicia Windows y Chrome se abrirá automáticamente al inicio.

{% hint style="info" %}
Para eliminar la apertura automática deberás eliminar el archivo de la carpeta de inicio.
{% endhint %}

### Linux

```
google-chrome --kiosk --fullscreen -tab https://example.com
```

#### Ejecutar al inicio de Linux (Opcional)

Si deseas que Chrome se abra cada vez que Linux se inicie, deberás añadir este archivo de la siguente manera:

1. Descarga este archivo en cualquier ubicación

{% file src="../.gitbook/assets/kiosk.service" %}

{% hint style="info" %}
En caso que no puedas descargar el archivo debido a bloqueos de seguridad en la red, copia el siguiente contenido y pégalo en un archivo llamado `kiosk.service`
{% endhint %}

{% code title="Contenido archivo .service" %}
```bash
[Unit]
Description=Open Google Chrome after reboot

[Service]
Type=simple
ExecStart=/bin/bash google-chrome --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

2\. Abre la terminal con la combinación de teclas <mark style="background-color:blue;">Ctrl</mark> + <mark style="background-color:blue;">Alt</mark> + <mark style="background-color:blue;">T</mark>&#x20;

3\. Ejecuta los siguentes comandos, uno tras otro:

```
$ cd /etc/systemd/system
$ sudo mv /{REPLACE_DOWNLOAD_FILEPATH} ./
$ sudo chmod 644 ./kiosk.service
$ sudo service enable kiosk.service
```

4\. Listo! Ahora cuando Linux reinicie se abrirá Google Chrome automáticamente.

{% hint style="info" %}
Si deseas obtener más detalles de otros argumentos disponibles para abrir Google Chrome o navegadores basados en Chromium ingresa a [este enlace](https://peter.sh/experiments/chromium-command-line-switches/).
{% endhint %}
