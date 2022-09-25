# Posición del widget

Es posible mover el widget de posición mediante código CSS o Javascript. Para ello deberás añadir el siguiente snippet:

### CSS

{% tabs %}
{% tab title="Izquierda" %}
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

{% tab title="Derecha" %}
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
{% tab title="Javascript (Izquierda)" %}
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

{% tab title="Javascript (Derecha)" %}
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
🚧 Estamos trabajando para que esta personalización la puedas realizar por el dashboard. 🚧
{% endhint %}

## Posición en base a resolución

Para modificar la posición del widget basado en la resolución del dispositivo puede utilizar [CSS media queries](https://developer.mozilla.org/es/docs/Web/CSS/Media\_Queries/Using\_media\_queries).

{% hint style="info" %}
`max-width` y `min-width` representarán puntos de quiebre (breakpoints) en base a la resolución en pixeles.
{% endhint %}

La siguiente tabla porporciona breakpoints más comunes:

| Resoluciones    | Dispositivo                             |
| --------------- | --------------------------------------- |
| 320px - 480px   | Mobile devices                          |
| 481px - 768px   | iPads y tablets                         |
| 769px - 1024px  | Pantallas pequeñas (laptops, notebooks) |
| 1025px - 1200px | Escritorios                             |
| 1201px o más    | Alta resolución                         |

A continuación, te proporcionamos algunos ejemplos:

{% code title="Izquierda móvil" %}
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

{% code title="Izquierda notebooks" %}
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
