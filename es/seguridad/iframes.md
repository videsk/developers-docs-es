# 🖼 Iframes

Si requieres embeber un sitio donde esté el widget presente a través de un `iframe`, debes tener en consideración que existen requisitos de seguridad a cumplir para que no existan conflictos en el uso de cámara, micrófono, pantalla completa, gps, etc.

## Atributos

Lo primero que debes considerar es que debes añadir dos atributos olbigatorios `allow` y `allowfullscreen`, de lo contrario no funcionará correctamente el embebido.

```html
<iframe src="..." allow="camera;microphone" allowfullscreen="true"></iframe>
```

### Permisos extras

Si requieres de otros permisos como GPS, giroscopio, sensor de luz, etc. deberás añadirlos al atributo `allow` basado en la [documentación MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Permissions\_Policy).

## Usando librerías

También te sugiremos para evitar problemas de dominio cruzado el uso de nuestra librería de código abierto [iFrameX](https://github.com/videsk/iFrameX), que te permitirá crear iframes sin necesidad de un source diferente al actual, inyectando el contenido Javascript, CSS y HTML de forma dinámica.

{% embed url="https://github.com/videsk/iFrameX" %}
