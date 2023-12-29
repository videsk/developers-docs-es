# Customizable bubble

To change the default bubble, you need to code a couple of HTML elements and add some JavaScript code that will interact with the API of the widget.

## Example

{% hint style="success" %}
The content is an example, you can reuse it or create your own code. The structure, color, content, text, icon, etc. are completely customizable.
{% endhint %}

{% embed url="https://codesandbox.io/s/playground-widget-custom-bubble-ejt85" %}

## ¿Cómo funciona?

There are relevant elements when modifying the default bubble. For this, you should consider the following:

### CSS Styles

```css
.videsk-top-container {
    z-index: 9999 !important;
}

.videsk-button-iframe {
    visibility: hidden;
}
```

With the previous CSS code you will overwrite the default styles, to give way to your own bubble.

### Widget API

The second most relevant thing is that you know about our widget API which, in addition to allowing you to open or close the widget, has `listeners` that will help you listen for actions on it.

The important thing is to attach a listener to the `click` event to run the `toggle` method of the widget itself.

```javascript
function myToggleFunction () {
  if (window.videsk) videsk.toggle();
}

yourOwnBubble.addEventListener('click', myToggleFunction);
```

{% hint style="info" %}
Remember that `yourOwnBubble` is your DOM element that you can reference by querySelector.
{% endhint %}