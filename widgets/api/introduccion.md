# Introducción

Nuestro producto Widget tiene la capacidad de ser interactuado mediante su propia API. Esto permite a los desarrolladores personalizar su comportamiento basado en eventos o funciones dispuestas para ellos.

Para acceder a la API se debe usar la variable global:

```javascript
videsk
// Or
window.videsk

// Example
videsk.toggle();
// Or
window.videsk.toggle();
```

### Activar modo debug

Para activar el modo debug deberás asignar el valor `true`a la variable global `__VIDESK_WIDGET_DEBUG__` antes de cargar el `script`.

```javascript
window.__VIDESK_WIDGET_DEBUG__ = true;
```

Esto permitirá mostrar en consola información del estado de los eventos y estado de las funciones, cada uno con sus valores de retorno correspondientes.

{% hint style="danger" %}
**No olvides eliminar el modo debug en modo producción.**
{% endhint %}

A continuación se describe el uso de los eventos y funciones disponibles como API.

{% hint style="info" %}
Antes de comenzar recuerda el uso de la variable global `videsk` como acceso a la Widget API.
{% endhint %}

{% content-ref url="variables-globales.md" %}
[variables-globales.md](variables-globales.md)
{% endcontent-ref %}

{% content-ref url="metodos.md" %}
[metodos.md](metodos.md)
{% endcontent-ref %}

{% content-ref url="eventos.md" %}
[eventos.md](eventos.md)
{% endcontent-ref %}

{% content-ref url="ajustes.md" %}
[ajustes.md](ajustes.md)
{% endcontent-ref %}
