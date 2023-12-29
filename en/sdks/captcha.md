---
description: >-
  In this section you will learn how to use Captcha with Forms in order to maximize the security and integrity of your account.
---

# 🤖 Captcha

{% hint style="warning" %}
For security reasons, Captcha cannot be removed.
{% endhint %}

This SDK allows you to add a unique captcha validation (_Completely Automated Public Turing test to tell Computers and Humans Apart_) easily regardless of the available provider.

{% hint style="info" %}
We are working to offer more integrations with providers that offer invisible captcha.
{% endhint %}

### Supported providers

* hCaptcha
* Google reCaptcha Enterprise
* Cloudflare Turnstile

## Installation

To use Forms SDK you can install it using our CDN.

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

## How to use

```javascript
const captcha = new CaptchaSDK(providerName, options);
```

{% hint style="info" %}
You should use this SDK together with [Phone](phone/#getting-started), which provides the arguments to instantiate Captcha.
{% endhint %}

### Options

The second argument of Captcha is an options object, which must contain:

* `siteKey`: site key, which you must obtain through [Phone](phone/#getting-started)
* `resource`: JS resource URL of the captcha provider
* `node`: DOM id as a `string` without query, that is, `#myButton` should be `myButton`.

{% hint style="warning" %}
Defining the `node` option only applies to providers: _hCaptcha_.
{% endhint %}

{% hint style="warning" %}
**The `node` option uses `document.getElementById(node)`**, so **you CANNOT use CSS selectors**.
{% endhint %}

You can find a working example with our Phone SDK.

{% content-ref url="phone/" %}
[phone](phone/)
{% endcontent-ref %}

## Methods

Once the SDK is instantiated you can access the following methods:

### `on`

This method aims to let you define a listener when an event occurs. The two arguments it receives are:

* `event`: name of the event
* `callback`: function that will be executed when the event occurs

```javascript
captcha.on('token', callback);
```

### `exec`

This method executes the activation of the captcha, which could be visible or invisible. The latter will depend on the provider.

```javascript
captcha.exec();
```

### `remove`

This method allows you to remove the generated captcha node.

```javascript
captcha.remove();
```

{% hint style="info" %}
As a good practice, use this method when captcha validation is successfully completed.
{% endhint %}

## Events

The available events are `token`, `close`, `error`.

### `token`

This event is fired once the validation has been successfully completed. The only argument is a `token`.

```javascript
captcha.on('token', token => {
  doSomething();
})
```

{% hint style="info" %}
This token is an automatically generated value that we use to validate the user's authenticity.
{% endhint %}

### `close`

This event is fired only if the captcha provider is visible and the validation interface has been closed/hidden. There are no arguments.

```javascript
captcha.on('close', () => {});
```

### `error`

This event is fired when there is an error in the validation, which does not necessarily have to be related to the robot-human validation.

```javascript
captcha.on('error', (error) => {
  doSomething();
});
```

{% hint style="info" %}
For more information about _hCaptcha_ errors visit [this page](https://docs.hcaptcha.com/configuration#error-codes).
{% endhint %}

## Example

```javascript
const captcha = new CaptchaSDK('hcaptcha', {
siteKey: '...',
resource: '...',
node: 'myButton'
});

captcha.on('token', token => sendMyForm(token));

myButton.addEventListener('click', () => captcha.exec());