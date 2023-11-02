# Métodos

## Segmentos 🚦

Con este método podrás obtener los segmentos de tu cuenta para mostrarlos a tus clientes.

{% tabs %}
{% tab title="Solicitar" %}
```javascript
const response = await phone.getSegments();
```
{% endtab %}

{% tab title="Respuesta" %}
```javascript
{
   "total": 2,
   "limit": 10,
   "skip": 0,
   "data": [
      {
         "name": "Segmento 1",
         "id": "5f7f67333baba9c4818d3a08"
      },
      {
         "name": "Segmento 2",
         "id": "203e4ffec73a69409edc14ea"
      }
   ],
   "cached": true
}
```
{% endtab %}
{% endtabs %}

## Agentes disponibles 📞

Con este método podrás obtener el total de agentes disponibles o en línea. Es relevante es que utilices este método para notificar a tus clientes cuando no hay agentes disponibles.

{% hint style="info" %}
Se aceptan dos argumentos, el primero el id del segmento y el segundo opcional con el estado a verificar. Este último recibe el estado como **`online`** o **`available`** .

El estado **`online`** entregará el número de agentes conectados en ese segmento.

Mientras que **`available`** entregará el número de agentes disponibles para atender, es decir, que no estén en llamada y conectados.
{% endhint %}

{% tabs %}
{% tab title="Solicitar" %}
```javascript
await phone.getAgents(segmentId); // Por defecto = online
await phone.getAgents(segmentId, 'available'); // Buscará la cantidad de agentes que estén listos para recibir una llamada.
```
{% endtab %}

{% tab title="Respuesta" %}
```javascript
1 // Integer
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
La respuesta de la API retornará el total como un número,`integer`. Es decir, podrás almacenar el total directamente en una variable. **No es un objeto**.
{% endhint %}

{% hint style="warning" %}
Por defecto, si realizas una llamada, el SDK verificará que existan agentes en estado online, en caso contrario se gatillará el evento `no-agents`.
{% endhint %}

## Llamar ☎

Con este método podrás llamar indicando el segmento de donde se realizará la llamada.

```javascript
await phone.call('5f7f67333baba9c4818d3a08');
await phone.connect('5f7f67333baba9c4818d3a08');
// Los dos métodos son equivalentes
```

## Abandonar&#x20;

Con este método podrás permitir a tus clientes abandonar la fila de espera.

{% hint style="warning" %}
Este método solo lo deberás utilizar cuando esté en la fila de espera, no antes ni después.
{% endhint %}

```javascript
phone.leave();
```

{% hint style="info" %}
También es posible abandonar la fila indicando el motivo o razón, solo si tienes razones de abandono configuradas. Para obtener las razones de abandono [dirígete aquí](metodos.md#obtener-razones-de-abandono).
{% endhint %}

```javascript
const [{ id }] = await phone.getAbandonReasons();
phone.setAbandonReason({ id });
```

{% hint style="danger" %}
Deberás usar el método `leave` o `setAbandonReason`, no ambos.
{% endhint %}

## Colgar

Con este método podrás colgar la llamada de forma manual.

```javascript
phone.hangup();
```

{% hint style="warning" %}
Deberás utilizar este método en conjunto con el [SDK de WebRTC](../webrtc/), escuchando el evento de colgar.
{% endhint %}

```javascript
const events = {
    hangup: () => phone.hangup(),
};
const options = { el: '#webrtc' };
let webrtc = new VideskWebRTCSDK(idCall, events, options);
```

## Listen

{% hint style="warning" %}
Puedes usar este método para escuchar los eventos o bien como se indica más abajo.
{% endhint %}

Con este metodo podrás asignar una función callback a un evento en particular de la siguiente namera:

{% code lineNumbers="true" %}
```javascript
phone.listen(eventName, callback);
// Ejemplo
phone.listen('queued', () => console.log('El cliente ha sido añadido a la fila'));
```
{% endcode %}

{% hint style="info" %}
Para los siguientes métodos deberás usar nuestros dos SDKs [Forms](../forms.md) y [Captcha](../captcha.md), **solo si deseas usarlos**.
{% endhint %}

***

## Obtener formulario

Con este método podrás obtener el formulario de un segmento. Recibe tres argumentos:

1. ID del segmento
2. Versión del formulario `base` o `contact`, por defecto `base`&#x20;
3. Despachar evento `true` o `false` `(opcional)`

```javascript
phone.getForm(segmentId, version);
```

{% hint style="info" %}
El valor de salida puede ser nulo, lo que significa que no hay formularios asociados y puedes continuar con la llamada.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
const response = await phone.getForm(segmentId, 'base');
if (!response) return continueWithCall();
// Carga Forms SDK
const { form } = response;
```
{% endcode %}

{% code lineNumbers="true" %}
```javascript
const response = await phone.getForm(segmentId, 'contact');
// Carga Forms SDK
const { form } = response;
```
{% endcode %}

Ejemplo:

{% code lineNumbers="true" %}
```javascript
const totalAgents = await phone.getAgents(segmentId);

if (totalAgents < 1) return showContactFormNotAvailable(segmentId);

const response = await phone.getForm(segmentId, 'base');

if (response) return showBaseFormPreviousCall(response.form);
else continueWithCallWithoutForm(); 
```
{% endcode %}

{% hint style="danger" %}
Si activas un formulario base en un segmento **no podrás continuar a la llamada sin un formulario** previamente enviado.
{% endhint %}

## Enviar formulario

{% hint style="warning" %}
Deberás hacer uso de nuestro SDK de [formularios](../forms.md) y de [captcha](../captcha.md).
{% endhint %}

Con este método podrás enviar un formulario. Recibe un argumento como `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong>    values,
    type,
    segment,
    token,
}
</code></pre>

* `values` es un array obtenido mediante [Form SDK](../forms.md).
* `type` es el tipo de formulario pudiendo ser `pre-call` o `contact`.
* `segment` es el id del segmento a llamar.
* `token` es un string obtenido mediante [Captcha SDK](../captcha.md).

```javascript
const response = await phone.sendForm(data);
const formId = response.submission; // Form id
```

{% hint style="info" %}
El valor de salida puede ser nulo, lo que significa que alguno de los campos del formularios son inválidos o el token captcha expiró.
{% endhint %}

## Obtener encuesta

Con este método podrás obtener una encuesta de un segmento. Recibe un solo argumento id del segmento:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const response = await phone.getSurvey(segmentId);
</strong><strong>const { form } = response;
</strong></code></pre>

## Enviar encuesta

{% hint style="warning" %}
Deberás hacer uso de nuestro SDK de [formularios](../forms.md).
{% endhint %}

Con este método podrás enviar una encuesta. Recibe un argumento como `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong>    values,
    call,
    segment,
}
</code></pre>

* `values` es un array obtenido mediante [Form SDK](../forms.md).
* `call` es el id de la llamada.

```javascript
await phone.sendSurvey(data);
```

{% hint style="info" %}
El valor de salida puede ser nulo, lo que significa que alguno de los campos de la encuesta son inválidos.
{% endhint %}

## Obtener razones de abandono

Con este método podrás obtener las razones de abandono configuradas en tu cuenta.

{% tabs %}
{% tab title="Obtener" %}
```javascript
const abandonReasons = await phone.getAbandonReasons();
```
{% endtab %}

{% tab title="Respuesta" %}
```javascript
[
    {
        "label": "Tiempo de espera",
        "name": "too-much-wait",
        "id": "62ed6b537fb69f6ce50c8539"
    },
    {
        "label": "Resolví mis dudas",
        "name": "resolve-my-doubts",
        "id": "6306422767b540c40429973d"
    }
]
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Deberás verificar en tu cuenta que existen razones de abandono configuradas, de lo contrario obtendrás un error 404.
{% endhint %}
