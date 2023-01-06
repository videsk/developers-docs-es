# Métodos

## `enable`

Con este método habilitarás la cancelación de ruido. Deberás entregar un solo argumento el cual corresponde al medio (`MediaStream`) que contenga al menos una pista de audio, excepto a que previamente lo hayas deshabilitado.

{% hint style="info" %}
Para obtener un MediaStream, te recomendamos hacer uso del método [`camera`](../../componentes-web/webrtc/metodos.md#camera) de nuestro componente WebRTC.
{% endhint %}

{% hint style="warning" %}
Este método es asíncrono.
{% endhint %}

```javascript
const streamFiltered = await suppression.enable(stream);
```

El valor de retorno corresponde a un `MediaStream` con la pista de audio activada con cancelación de ruido.

Posteriormente deberás hacer uso de nuestro WebRTC. Por ejemplo, al momento de [crear una instancia](../webrtc/metodos.md#create) de WebRTC deberás entregar como último argumento el MediaStream con cacelación de ruido.

```javascript
const streamFiltered = await suppression.enable(stream);
webrtc.create(accessToken, null, streamFiltered);
```

## `disable`

Con este método desactivas la cancelación de ruido.

```javascript
suppression.disable();
```

Si nuevamente deseas volver a habilitar la cancelación de ruido solo debes volver a hacer uso del método [`enable`](metodos.md#enable), sin necesidad de entregar el argumento `MediaStream`.
