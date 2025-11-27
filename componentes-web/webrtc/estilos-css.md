# Estilos (CSS)

A continuación, se describen propiedades CSS que pueden utilizarse para cambiar el estilo visual.

## `::part()`&#x20;

Este operador permite aplicar estilos CSS a componentes de shadow root de nuestros componentes web.

### `chat`

Permite aplicar estilos CSS a todo el componente de chat. Internamente se utiliza el componente `videsk-chat`.

```css
videsk-webrtc::part(chat) {
  /* styles */
}
```

### `buttons`

Permite aplicar estilos CSS al contenedor de los botones de acciones (mic, cam, hangup, etc).

```css
videsk-webrtc::part(buttons) {
    /* styles */
}
```

Dentro de buttons se encuentran todos los botones por defecto descritos en [Slots](slots.md), tienen exactamente los mismos nombres:

```css
videsk-webrtc::part(button-x) {
    /* styles */
}
```

| ::part(X)            |
| -------------------- |
| button-toggle-camera |
| button-screen        |
| button-chat          |
| button-mic           |
| button-hangup        |
| button-cam           |
| button-fullscreen    |

### `participants`

Permite aplicar estilos CSS al contenedor de los participantes.

{% hint style="info" %}
Si aplicas CSS a este componente, debes considerar que depende del [layout](propiedades.md).  Puedes sobrescribir el comportamiento, pero los estilos están definidos para adaptarse automáticamente.
{% endhint %}

```css
videsk-webrtc[grid]::part(participants) {
    /* styles */
}

videsk-webrtc[sidebar]::part(participants) {
    /* styles */
}
```

### `participants-toggle`

Permite aplicar estilos CSS al elemento que permite mostrar y ocultar a los participantes cuando el layout es `sidebar`.

```css
videsk-webrtc::part(participants-toggle) {
    /* styles */
}
```

### `container`

Permite aplicar estilos CSS al contenedor principal de todo `videsk-webrtc`.

{% hint style="info" %}
Debes tener precaución con los estilos que apliques, ya que por defecto nuestro componente usa CSS `grid` para posicionar componentes.
{% endhint %}

```css
videsk-webrtc::part(container) {
    /* styles */
}
```
