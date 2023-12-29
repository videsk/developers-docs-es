---
description: >-
  A continuación, te explicaremos como utilizar Captcha con Forms para maximizar
  la seguridad e integridad de tu cuenta.
---

# 🤖 Captcha

{% hint style="warning" %}
Por motivos de seguridad, no es posible quitar Captcha.
{% endhint %}

Este SDK permite que puedas añadir una validación captcha (_Completely Automated Public Turing test to tell Computers and Humans Apart_) única de forma sencilla sin importar el proveedor disponible.

{% hint style="info" %}
Estamos trabajando para ofrecer más integraciones con proveedores que ofrezcan captcha invisibles.
{% endhint %}

### Proveedores compatibles

* hCaptcha
* Google reCaptcha Enterprise
* Cloudflare Turnstile

## Instalación

Para utilizar Forms SDK podrás instarlo mediante nuestro CDN.

{% tabs %}
{% tab title="HTML" %}
```html
<script src="https://cdn.videsk.io/sdk/captcha.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = 'https://cdn.videsk.io/sdk/captcha.min.js';
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

## Modo de uso

```javascript
const captcha = new CaptchaSDK(providerName, options);
```

{% hint style="info" %}
Deberás usar este SDK junto con [Phone](phone/#obtener-formulario), el cual provee los argumentos para instanciar Captcha.
{% endhint %}

### Opciones

El segundo argumento de Captcha es un object de opciones, el cual debe contener:

* `siteKey`: clave del sitio, el cual debes obtener mediante [Phone](phone/#obtener-formulario)
* `resource`: URL del recurso JS del proveedor captcha
* `node`: id DOM como `string` sin query, es decir, `#myButton` debe ser `myButton`.

{% hint style="warning" %}
Definir la opción `node` solo aplica para proveedores: _hCaptcha_.
{% endhint %}

{% hint style="warning" %}
**La opción `node` utiliza `document.getElementById(node)`**, por lo tanto **NO puedes utilizar selectores CSS**.
{% endhint %}

Podrás encontrar un ejemplo funcional junto a nuestro Phone SDK.

{% content-ref url="phone/" %}
[phone](phone/)
{% endcontent-ref %}

## Métodos

Ya instanciado el SDK podrás acceder a los siguientes métodos:

### `on`

Este método tiene como objetivo que definas un oyente cuando un evento ocurra. Los dos argumentos que recibe son:

* `event`: nombre del evento
* `callback`: función que se ejecutará al ocurrir el evento

```javascript
captcha.on('token', callback);
```

### `exec`

Este método ejecuta la activación del captcha, el cual podría ser visible o invisible. Esto último dependerá del proveedor.

```javascript
captcha.exec();
```

### `remove`

Este método permite eliminar el nodo captcha generado.

```javascript
captcha.remove();
```

{% hint style="info" %}
Como buena práctica utiliza este método al momento en que la validación captcha se complete exitosamente.
{% endhint %}

## Eventos

Los eventos disponibles son `token`, `close`, `error`.

### `token`

Este evento se dispara una vez que se ha completado la validación de forma exitosa. El único argumento es un `token`.

```javascript
captcha.on('token', token => {
    doSomething();
})
```

{% hint style="info" %}
Este token es un valor generado automáticamente que utilizamos para validar la autenticidad del usuario.
{% endhint %}

### `close`

Este evento se dispara solo si el proveedor captcha es visible y se ha cerrado/ocultado la interfaz de validación. No hay argumentos.

```javascript
captcha.on('close', () => {});
```

### `error`

Este evento se dispara cuando existe un error en la validación, el cual no necesariamente debe estar relacionado con la validación robot-humano.

```javascript
captcha.on('error', (error) => {
  doSomething();
});
```

{% hint style="info" %}
Para más información sobre errores de _hCaptcha_ visita [esta página](https://docs.hcaptcha.com/configuration#error-codes).
{% endhint %}

## Ejemplo

```javascript
const captcha = new CaptchaSDK('hcaptcha', {
    siteKey: '...',
    resource: '...',
    node: 'myButton'
});

captcha.on('token', token => sendMyForm(token));

myButton.addEventListener('click', () => captcha.exec());
```
