# Widget position

You can move the widget position using CSS or Javascript code. To do this, you must add the following snippet:

### CSS

{% tabs %}
{% tab title="Left" %}
```css
.videsk-top-container {
    left: 3% !important;
    align-items: flex-start !important;
}

.videsk-button-iframe {
    left: 10px !important;
    right: unset !important;
    bottom: 10px;
}
```
{% endtab %}

{% tab title="Right" %}
```css
.videsk-top-container {
    right: 3% !important;
    align-items: flex-end !important;
}

.videsk-button-iframe {
    left: unset !important;
    right: 10px !important;
    bottom: 10px;
}
```
{% endtab %}
{% endtabs %}

### Javascript

{% tabs %}
{% tab title="Javascript (Left)" %}
```html
<script>
    const style = document.createElement('style');
    style.innerHTML = `
.videsk-top-container {
left: 3% !important;
align-items: flex-start !important;
}

.videsk-button-iframe {
position: absolute;
left: 10px !important;
right: unset !important;
bottom: 10px;
}
`;
    document.head.appendChild(style);
</script>
```
{% endtab %}

{% tab title="Javascript (Right)" %}
```
<script>
const style = document.createElement('style');
style.innerHTML = `
.videsk-top-container {
right: 3% !important;
align-items: flex-end !important;
}
.videsk-button-iframe {
position: absolute;
left: unset !important;
right: 10px !important;
bottom: 10px;
}
`;
document.head.appendChild(style);
</script>
```


{% endtab %}
{% endtabs %}

{% hint style="success" %}
🚧 We're working to make this customization available in the dashboard. 🚧
{% endhint %}

## Position based on resolution

To modify the position of the widget based on the resolution of the device you can use [CSS media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media\_Queries/Using\_media\_queries).

{% hint style="info" %}
`max-width` and `min-width` will represent breakpoints based on the resolution in pixels.
{% endhint %}

The following table provides the most common breakpoints:

| Resolutions | Device |
| --------------- | --------------------------------------- |
| 320px - 480px | Mobile devices |
| 481px - 768px | iPads and tablets |
| 769px - 1024px | Small screens (laptops, notebooks) |
| 1025px - 1200px | Desktops |
| 1201px or more | High resolution |

Here are some examples:

{% code title="Left Mobile" %}
```css
@media screen and (max-width: 600px) {

    .videsk-top-container {
        left: 3% !important;
        align-items: flex-start !important;
    }

    .videsk-button-iframe {
        left: 10px !important;
        right: unset !important;
        bottom: 10px;
    }

}
```
{% endcode %}

{% code title="Left Notebooks" %}
```css
@media screen and (min-width: 800px) {

    .videsk-top-container {
        left: 3% !important;
        align-items: flex-start !important;
    }

    .videsk-button-iframe {
        left: 10px !important;
        right: unset !important;
        bottom: 10px;
    }

}
```
{% endcode %}