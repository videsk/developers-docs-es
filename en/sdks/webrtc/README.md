---
description: WebRTC video call connection instance SDK.
---

# 📹 WebRTC

With this SDK you can create an instance of WebRTC video call connection in a very simple way.

{% hint style="warning" %}
You must use this SDK with our [Phone SDK](../phone/).
{% endhint %}

## Installation

To get started you need to install our SDK on your website or mobile app. You have the following options.

{% tabs %}
{% tab title="HTML" %}
{% code lineNumbers="true" %}
```html
<script src="https://cdn.videsk.io/sdk/webrtc.min.js"></script>
```
{% endcode %}
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/webrtc.min.js";
document.body.appendChild('body'); // Or replace with the desired DOM node
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Don't store the content of our SDK on your server, **this violates our terms of service**.
{% endhint %}

## Usage

Our SDK is a web component, which allows you to access it like any HTML element or DOM node you are used to.

{% code lineNumbers="true" %}
```html
<videsk-webrtc></videsk-webrtc>
```
{% endcode %}

You can see more information about our web component in the following link:

{% content-ref url="../../web-components/webrtc/" %}
[webrtc](../../web-components/webrtc/)
{% endcontent-ref %}

{% hint style="info" %}
You will need to load the script from our CDN, otherwise it will be an empty tag.
{% endhint %}

Then, you must create a `WebRTC` instance which **will allow you to make the connection**.

{% code lineNumbers="true" %}
```javascript
const webrtc = new WebRTC();
await webrtc.create(accessToken, constraints);
```
{% endcode %}

You can see the available methods in the following page:

{% content-ref url="methods.md" %}
[methods.md](methods.md)
{% endcontent-ref %}

### Arguments

The `WebRTC` class receives three arguments:

#### `component` (optional)

It corresponds to the DOM reference of the web component, example:

{% code lineNumbers="true" %}
```javascript
const element = document.querySelector('videsk-webrtc');
new WebRTC(element);
```
{% endcode %}

If the value is `undefined`, `null` or invalid by default will create a `videsk-webrtc` node in the `parent` node which by default is `body`.

#### `parent` (optional)

Corresponds to the DOM reference where the `` web component will be attached (`append`).

{% code lineNumbers="true" %}
```javascript
const parent = document.querySelector('#custom-div');
new WebRTC(null, parent);
```
{% endcode %}

#### `options` (optional)

Corresponds to options that are given to the WebRTC instance to modify the default values.

{% code lineNumbers="true" %}
```javascript
const options = {
websocket: { hostname: 'wss://exchange.videsk.io' }
};
```
{% endcode %}

### Create instance

To create an instance you will only need two lines of code:

{% code lineNumbers="true" %}
```javascript
const webrtc = new WebRTC();
await webrtc.create(accessToken);
```
{% endcode %}