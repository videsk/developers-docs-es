---
description: >-
  A continuaci贸n, te explicaremos como utilizar Captcha con Forms para maximizar
  la seguridad e integridad de tu cuenta.
---

# 馃 Captcha

{% hint style="warning" %}
Por motivos de seguridad, no es posible quitar Captcha.
{% endhint %}

Este SDK permite que puedas a帽adir una validaci贸n captcha (_Completely Automated Public Turing test to tell Computers and Humans Apart_) 煤nica de forma sencilla sin importar el proveedor disponible.

{% hint style="info" %}
Estamos trabajando para ofrecer m谩s integraciones con proveedores que ofrezcan captcha invisibles.
{% endhint %}

### Proveedores compatibles

* hCaptcha
* Google reCaptcha Enterprise
* Cloudflare Turnstile

## Instalaci贸n

Para utilizar Forms SDK podr谩s instarlo mediante nuestro CDN.

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
Deber谩s usar este SDK junto con [Phone](phone.md#obtener-formulario), el cual provee los argumentos para instanciar Captcha.
{% endhint %}

### Opciones

El segundo argumento de Captcha es un object de opciones, el cual debe contener:

* `siteKey`: clave del sitio, el cual debes obtener mediante [Phone](phone.md#obtener-formulario)
* `resource`: URL del recurso JS del proveedor captcha
* `node`: id DOM como `string` sin query, es decir, `#myButton` debe ser `myButton`.

{% hint style="warning" %}
Definir la opci贸n `node` solo aplica para proveedores: _hCaptcha_.
{% endhint %}

{% hint style="warning" %}
**La opci贸n `node` utiliza `document.getElementById(node)`**, por lo tanto **NO puedes utilizar selectores CSS**.
{% endhint %}

Podr谩s encontrar un ejemplo funcional junto a nuestro Phone SDK.

{% content-ref url="phone.md" %}
[phone.md](phone.md)
{% endcontent-ref %}

## M茅todos

Ya instanciado el SDK podr谩s acceder a los siguientes m茅todos:

### `on`

Este m茅todo tiene como objetivo que definas un oyente cuando un evento ocurra. Los dos argumentos que recibe son:

* `event`: nombre del evento
* `callback`: funci贸n que se ejecutar谩 al ocurrir el evento

```javascript
captcha.on('token', callback);
```

### `exec`

Este m茅todo ejecuta la activaci贸n del captcha, el cual podr铆a ser visible o invisible. Esto 煤ltimo depender谩 del proveedor.

```javascript
captcha.exec();
```

### `remove`

Este m茅todo permite eliminar el nodo captcha generado.

```javascript
captcha.remove();
```

{% hint style="info" %}
Como buena pr谩ctica utiliza este m茅todo al momento en que la validaci贸n captcha se complete exitosamente.
{% endhint %}

## Eventos

Los eventos disponibles son `token`, `close`, `error`.

### `token`

Este evento se dispara una vez que se ha completado la validaci贸n de forma exitosa. El 煤nico argumento es un `token`.

```javascript
captcha.on('token', token => {
    doSomething();
})
```

{% hint style="info" %}
Este token es un valor generado autom谩ticamente que utilizamos para validar la autenticidad del usuario.
{% endhint %}

### `close`

Este evento se dispara solo si el proveedor captcha es visible y se ha cerrado/ocultado la interfaz de validaci贸n. No hay argumentos.

```javascript
captcha.on('close', () => {});
```

### `error`

Este evento se dispara cuando existe un error en la validaci贸n, el cual no necesariamente debe estar relacionado con la validaci贸n robot-humano.

```javascript
captcha.on('error', (error) => {
  doSomething();
});
```

{% hint style="info" %}
Para m谩s informaci贸n sobre errores de _hCaptcha_ visita [esta p谩gina](https://docs.hcaptcha.com/configuration#error-codes).
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
