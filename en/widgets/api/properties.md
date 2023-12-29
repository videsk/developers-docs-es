---
description: This document defines the available properties to interact with the widget programmatically
---

# Properties

Our widget contains properties that allow us to change or overwrite the default behavior.

{% hint style="info" %}
We recommend you to use these properties only after `videsk-load` event has been fired.

```javascript
document.addEventListener('videsk-load', () => {
  // Now you can use the properties
  videsk.xyz = '...';
});
```
{% endhint %}

## `constraints`

This read/write property allows you to overwrite the default camera and/or microphone values.

This value will overwrite the microphone and camera options, regardless if your client selects `microphone only` or `microphone + camera`.

{% hint style="warning" %}
It doesn't overwrite the explicit authorization from the client through the browser, so if the user denies the access to camera and/or microphone, they won't be able to access the video call.
{% endhint %}

{% hint style="info" %}
By default, this value is undefined.
{% endhint %}

{% tabs %}
{% tab title="Basic" %}
{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
  video: false, // without camera
  audio: true,
};
videsk.constraints // undefined
```
{% endcode %}


{% endtab %}

{% tab title="Fixed microphone" %}
{% hint style="info" %}
We recommend you to use the [device](https://developers.videsk.io/widgets/api/methods#device) method to obtain the device ID.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
  video: true,
  audio: {
    deviceId: {
      ideal: 'REPLACE_DEVICE_ID'
    }
  },
};
```
{% endcode %}
{% endtab %}

{% tab title="Fixed camera" %}
{% hint style="info" %}
We recommend you to use the [device](https://developers.videsk.io/widgets/api/methods#device) method to obtain the device ID.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
  audio: true,
  video: {
    deviceId: {
      ideal: 'REPLACE_DEVICE_ID'
    }
  },
};
```
{% endcode %}
{% endtab %}

{% tab title="Back camera" %}
{% code lineNumbers="true" %}
```javascript
videsk.constraints = {
  audio: true,
  video: {
    facingMode: 'environment'
  }
};
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
We recommend you to use this property on kiosks and interactive totems. This way, you can set up the permissions in advance in order to avoid technical errors.
{% endhint %}

## `fullscreen`

This property allows you to set the widget to cover the entire site without adding custom CSS.

```javascript
videsk.fullscreen = true;
```

{% code lineNumbers="true" %}
```javascript
document.addEventListener('videsk-load', () => {
  videsk.fullscreen = true;
  videsk.toggle(true);
});
```
{% endcode %}

{% hint style="warning" %}
Using the widget in `fullscreen` mode will hide the bubble, therefore, you will need to use `videsk.toggle(true)` to force its visibility.
{% endhint %}