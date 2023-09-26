# 🔇 Cancelación de ruido

{% hint style="danger" %}
El código fuente es propiedad de Videsk. El uso está restringido a clientes activos de Videsk, siendo punible legalmente acciones de copia, modificación o uso sin autorización.
{% endhint %}

{% hint style="info" %}
Si deseas usar este SDK contáctanos a [support@videsk.io](mailto:support@videsk.io) o con tu ejecutivo de cuenta para autorizar el acceso.
{% endhint %}

Con este SDK podrás cancelar el ruido ambiente, amplificando la voz proveniente del micrófono del dispositivo.

## Consideraciones

{% hint style="info" %}
Este SDK opera mediante deep learning y redes neuronales recurrentes, lo que consume más CPU/GPU. Debes considerar el rendimiento del dispositivo antes de usar esta funcionalidad.
{% endhint %}

Este SDK está diseñado para ser usado solo en contextos de ruido ambiente controlado, no para ambientes de construcción, conciertos o fábricas. Si bien aplicará la cancelación de ruido no obtendrás el mejor resultado.

{% hint style="info" %}
El ruido ambiente ideal debe oscilar entre menor o igual a 90 db (decibelios).
{% endhint %}

Como referencia puedes usar esta tabla:

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption><p>Fuente: <a href="https://es.wikipedia.org/wiki/Decibelio">https://es.wikipedia.org/wiki/Decibelio</a></p></figcaption></figure>

## Uso

Según las instrucciones que te hayamos entregado de forma privada deberás hacer uso del SDK de la siguiente manera:

```javascript
Const suppresion = new NoiseSuppression();
```

Posteriormente deberás usar los métodos y propiedades disponibles.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Métodos</strong></td><td>Conoce cómo usar los métodos de <code>NoiseSuppression</code>.</td><td></td><td><a href="metodos.md">metodos.md</a></td></tr><tr><td><strong>Propiedades</strong></td><td>Conoce cuáles son las propiedades de <code>NoiseSuppression</code>.</td><td></td><td><a href="propiedades.md">propiedades.md</a></td></tr></tbody></table>
