---
description: >-
  SDK para generar llamadas de cara a cliente (sitio web, app móvil, kioskos,
  etc.) mediante Javascript.
---

# 📞 Phone

Con este SDK podrás crear llamadas de forma programática, sin necesidad de preocuparte por las conexiones, parámetros, excepciones, etc.

Es decir, hemos creado este "enchufe" para llegar y usar de forma sencilla y una estructura de rápido aprendizaje, pero sin dejar de lado la flexibilidad y poder de nuestra API.

{% hint style="info" %}
Este SDK no provee interfaz, es decir, no hay código HTML, por lo que deberás manejar tu propia interfaz, ya sea en HTML puro, Javascript o con frameworks como Vue, React, Angular, Svelte, etc.
{% endhint %}

## Instalación

Para comenzar deberás instalar nuestro recurso en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/sdk/phone.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://assets.videsk.io/js/sdk/phone.min.js";
document.body.appendChild('body'); // O reemplaza con el nodo DOM que desees
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
No almacenes el contenido del script en tu servidor, **esto infringe nuestros términos de uso**.
{% endhint %}

{% hint style="danger" %}
Por seguridad y calidad de servicio tenemos un límite de peticiones por segundo por IP/Token, que consta de 20 peticiones en 1 segundo. Evita superar este límite, ya que nuestra Rest API bloqueará las peticiones de tus clientes.
{% endhint %}

## Ejemplos

A continuación podrás clonar un codesandbox que preparamos utilizando este SDK.

{% hint style="info" %}
El HTML y ciertas partes de Javascript **son de ejemplo**, las cuales deberás adaptar a tú framework o caso de uso.

Para usar este codesandbox, añade en la URL tu API Token de la siguiente manera:

https://xxxx.csb.app?token=**API\_TOKEN**

(Reemplaza API\_TOKEN)
{% endhint %}

{% embed url="https://codesandbox.io/s/phone-sdk-example-webview-android-vvct0" %}
Codesandbox usando Phone SDK
{% endembed %}

{% hint style="success" %}
Recuerda que deberá estar conectado al menos 1 agente en tu cuenta para probar este codesandbox.
{% endhint %}

## Instanciación

Primero deberás instanciar `VideskPhone` como un [constructor](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Classes/constructor).

```javascript
const phone = new VideskPhone(APIToken);
```

Con la variable `phone` podrás acceder a los métodos y propiedades.

{% hint style="info" %}
Si instancias `VideskPhone` sin un token automáticamente intentará extraer de la URL, por lo que podrás utilizar `token`, `videsk-token` o `api-key` como parámetro en la URL.&#x20;



Ejemplo:

`https://example.com?api-key=eyJhbGciOiJIUzI1NiIsI...`
{% endhint %}

## Métodos

Ya instanciado el SDK podrás acceder a los siguientes métodos:

### Segmentos 🚦

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

### Agentes disponibles 📞

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

### Llamar ☎

Con este método podrás llamar indicando el segmento de donde se realizará la llamada.

```javascript
await phone.call('5f7f67333baba9c4818d3a08');
await phone.connect('5f7f67333baba9c4818d3a08');
// Los dos métodos son equivalentes
```

### Abandonar&#x20;

Con este método podrás permitir a tus clientes abandonar la fila de espera.

{% hint style="warning" %}
Este método solo lo deberás utilizar cuando esté en la fila de espera, no antes ni después.
{% endhint %}

```javascript
phone.leave();
```

### Colgar

Con este método podrás colgar la llamada de forma manual.

```javascript
phone.hangup();
```

{% hint style="warning" %}
Deberás utilizar este método en conjunto con el [SDK de WebRTC](webrtc/), escuchando el evento de colgar.
{% endhint %}

```javascript
const events = {
    hangup: () => phone.hangup(),
};
const options = { el: '#webrtc' };
let webrtc = new VideskWebRTCSDK(idCall, events, options);
```

### Listen

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
Para los siguientes métodos deberás usar nuestros dos SDKs [Forms](forms.md) y [Captcha](captcha.md), **solo si deseas usarlos**.
{% endhint %}

### Obtener formulario

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

### Enviar formulario

{% hint style="warning" %}
Deberás hacer uso de nuestro SDK de [formularios](forms.md) y de [captcha](captcha.md).
{% endhint %}

Con este método podrás enviar un formulario. Recibe un argumento como `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong>    values,
    type,
    segment,
    token,
}
</code></pre>

* `values` es un array obtenido mediante [Form SDK](forms.md).
* `type` es el tipo de formulario pudiendo ser `pre-call` o `contact`.
* `segment` es el id del segmento a llamar.
* `token` es un string obtenido mediante [Captcha SDK](captcha.md).

```javascript
const response = await phone.sendForm(data);
const formId = response.submission; // Form id
```

{% hint style="info" %}
El valor de salida puede ser nulo, lo que significa que alguno de los campos del formularios son inválidos o el token captcha expiró.
{% endhint %}

### Obtener encuesta

Con este método podrás obtener una encuesta de un segmento. Recibe un solo argumento id del segmento:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const response = await phone.getSurvey(segmentId);
</strong><strong>const { form } = response;
</strong></code></pre>

### Enviar encuesta

{% hint style="warning" %}
Deberás hacer uso de nuestro SDK de [formularios](forms.md).
{% endhint %}

Con este método podrás enviar una encuesta. Recibe un argumento como `object`:

<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>const data = {
</strong>    values,
    call,
    segment,
}
</code></pre>

* `values` es un array obtenido mediante [Form SDK](forms.md).
* `call` es el id de la llamada.

```javascript
await phone.sendSurvey(data);
```

{% hint style="info" %}
El valor de salida puede ser nulo, lo que significa que alguno de los campos de la encuesta son inválidos.
{% endhint %}

## Eventos

Phone SDK posee un listado de eventos que te ayudarán a ejecutar acciones sobre el HTML. Son los cuales deberás escuchar mediante funciones para realizar cambios de interfaz.

{% @figma/embed fileId="ZgAVJ4UIU5hHN9F0sXWNG7" nodeId="0:1" url="https://www.figma.com/file/ZgAVJ4UIU5hHN9F0sXWNG7/Widget-workflow?node-id=0%3A1" %}

Para utilizar los eventos deberás realizar lo siguiente:

{% tabs %}
{% tab title="Listener (Recomendado)" %}
```javascript
const phone = new VideskPhone(APIToken);
phone.listen('no-agents', () => {});
```
{% endtab %}

{% tab title="Alternativa 1" %}
```javascript
const events = { ... };
const phone = new VideskPhone(APIToken, events);
```
{% endtab %}

{% tab title="Alternativa 2" %}
```javascript
const phone = new VideskPhone(APIToken);
phone.on['no-agents'] = () => {};
```
{% endtab %}

{% tab title="Alternativa 3" %}
```javascript
onst phone = new VideskPhone(APIToken);
phone.on = { ... };
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Los siguientes **eventos con \* (asterisco) son requeridos y obligatorios**, si no los escuchas de forma apropiada el comportamiento del SDK no será el esperado.
{% endhint %}

### `token-error`

Este evento se emitirá cuando el token proporcionado sea erróneo, mal formado o inválido. Esto podría eventualmente suceder si un administrador de cuenta, elimina la integración desde la cuenta.

{% hint style="info" %}
Esto deberá ser escuchado, solo en caso de ambiente de desarrollo.
{% endhint %}

```javascript
phone.on['token-error'] = () => {
    // Verificar token
};
```

### `no-agents`\*

Este evento se emitirá cuando no existan agentes conectados en tu cuenta luego de haber intentado la llamada mediante el método `phone.call()`.

```javascript
phone.on['no-agents'] = () => {
  // Muestra un mensaje que no hay agentes disponibles
};
```

### `queued`\*

Este evento se emite cuando el cliente ha sido añadido a la fila de espera, luego de haber llamado al método `phone.call()`.

```javascript
phone.on['queued'] = (event) => {
  const { position, avgWait, segment } = event;
  // Muestra una interfaz que permita visualizar la posición y/o el tiempo de espera.
};
```

{% hint style="warning" %}
La posición y/o el tiempo de espera, podrían estar desactivados por el administrador de la cuenta.
{% endhint %}

{% hint style="info" %}
El tiempo de espera está en unidades de minutos, por lo que te sugerimos utilizar [nuestra librería de código abierto](https://github.com/videsk/humanize-date) que "humaniza" la unidad de tiempo, para mostarla en segundos, minutos, horas, etc. dependiendo del valor.

Ejemplo:

Si el tiempo de espera retornado es 0.5 minutos, entonces nuestra librería devolverá 30 segundos.
{% endhint %}

### `queue-updated`\*

Este evento se emitirá cuando se actualice la posición en la fila, solo posterior al evento `queued`. **Es de suma relevancia que escuches este evento.**

```javascript
phone.on['queue-updated'] = (event) = {
    const { position } = event;
    // Actualizar posición en la fila
};
```

### `customer-leave`\*

Este evento se emitirá cuando se ejecuta el evento `phone.leave()` estando en la fila de espera.

```javascript
phone.on['customer-leave'] = () => {
    // Mostrar un mensaje de abandono de fila
};
```

### `dismissed`\*

Este evento se emitirá cuando un agente rechace la llamada.

```javascript
phone.on['dismissed'] = () => {
    // Mostrar un mensaje de llamada rechazada
};
```

### `out-queue`

Este evento se emite cuando la llamada ha sido contestada por un agente. **Es opcional escuchar este evento**.

```javascript
phone.on['out-queue'] = () => {
    // No es necesario modificar nada
};
```

### `answered`\*

Este evento se emite cuando la llamada ha sido contestada por un agente.

```javascript
phone.on['answered'] = (event) => {
    const { call } = event;
    // Deberás hacer uso de nuestro SDK de WebRTC
    let webrtc = new VideskWebRTCSDK(call, events, options);
    webrtc.create();
};
```

{% hint style="info" %}
Recuerda que deberás cargar nuestro WebRTC con anterioridad. Para más información visíta la documentión de [WebRTC SDK](webrtc/).
{% endhint %}

### `connected-call`

Este evento se emite cuando se ha conectado a la llamada de forma exitosa. **Es opcional escuchar este evento**.

```javascript
phone.on['connected-call'] = () => {
    // No es necesario modificar nada
};
```

### `agent-disconnect`

Este evento se emite cuando el agente quién contestó la llamada eventualmente se desconecta de la videollamada por problemas de red. **Es opcional escuchar este evento**.

{% hint style="warning" %}
No deberás terminar la llamada, ya que el agente se reconectará de forma automática. En caso de traspasar varios minutos nuestra API terminará la llamada de forma automática.
{% endhint %}

```javascript
phone.on['agent-disconnect'] = () => {
    // Mostrar un mensaje de agente desconectado
};
```

### `customer-hangup`

Este evento se emite cuando se ejecuta el método `phone.hangup()`. **Es opcional escuchar este evento**.

```javascript
phone.on['customer-hangup'] = () => {
    // Muestra un mensaje de llamada finalizada
};
```

### `ended`\*

Este evento se emite cuando se termina la llamada, ya sea por lado de agente o al ejecutar el método `phone.hangup()`.

```javascript
phone.on['ended'] = () => {
    // Muestra un mensaje de llamada finalizada
    webrtc.destroy();
};
```

{% hint style="warning" %}
Deberás eliminar la instancia de WebRTC creada, mediante el método `destroy()`.
{% endhint %}

### `transferred-segment`\*

Este evento se emitirá cuando un agente ha transferido al cliente a un segmento nuevo.

```javascript
phone.on['transferred-segment'] = (event) => {
    const { queue } = event;
    // Mostrar un mensaje, no deberás hacer nada con las conexiones
};
```

{% hint style="info" %}
El SDK realizará las conexiones automáticamente, empezando el ciclo desde el evento `queued` por lo tanto, solo deberás asegurarte que esté escuchándose.
{% endhint %}

### `transferred-agent`\*

Este evento se emitirá cuando un agente ha transferido al cliente a un agente en específico.

```javascript
phone.on['transferred-agent']= (event) => {
    const { call } = event;
    // Deberás crear una nueva instancia de WebRTC SDK y destruir la anterior
    webrtc.destroy();
    webrtc = new new VideskWebRTCSDK(call, events, options);
    webrtc.create();
};
```

### `connection-error`

Este evento se emitirá cuando exista algún error en la red o parámetros mal formados que se enviaron a la API. **Es opcional escuchar este evento**.

```javascript
phone.on['connection-error'] = (event) => {
    const { event, code, name, message, date, errors } = event;
}
```

### `network-issues`\*

Este evento se emitirá cuando existan problemas de red, como desconexión a Internet o demasiadas reconexiones producto de una red poco confiable.

```javascript
phone.on['network-issues'] = () => {
    // Mostrar mensaje de red poco estable
};
```

{% hint style="info" %}
Nuestra API tiene un algorítmo que identificará a un potencial cliente que presente una red poco **estable**, lo cual provocará que se rechace una conexión en la fila de espera.

Esto se debe a que la red requerida para la conexión en la fila de espera es minima, da como conclusion que la red del cliente no soportará una conexion estable de videollamada.

**El parámetro evaluado no es la velocidad, si no la estabilidad de la red.**
{% endhint %}

### `http-block`

Este evento se emitirá cuando nuestra API detecte actividad sospechosa como un bot o una llamada desde una red poco confiable. **Es opcional escuchar este evento**.

{% hint style="info" %}
Este tipo de comportamiento no es configurable, el cual permite entregar una mejor calidad de servicio a todos nuestros clientes, bloqueando potenciales atacantes o bots.
{% endhint %}

```javascript
phone.on['http-block'] = () => {
    // Mostrar mensaje de red poco confiable
};
```

### `transport-disconnect`

Este evento se emite cuando nuestra API desconecta de forma automática la conexión ya sea en la fila de espera o al terminar la llamada. Es decir, naturalmente este evento se emitirá dos veces en una llamada normal. **Es opcional escuchar este evento**.

```javascript
phone.on['transport-disconnect'] = () => {
    // Uso interno
};
```

## Límites y usos

{% hint style="danger" %}
No crees más de una instancia de `VideskPhone`, ya que podrías generar múltiples llamadas. Esto afectará en los reportes y podrías suspender tu cuenta por comportamiento sospechoso.
{% endhint %}

Este SDK te permitirá integrar Videsk en múltiples ambientes, ya sea en un sitio web, aplicación móvil utilizando marcos web, kioskos, IoT, etc.

**Para el caso de integraciones en apps iOS y Android**, te sugerimos utilizar [Custom Tabs](https://developer.chrome.com/docs/android/custom-tabs/) para Android y [Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) para iOS.

Estos marcos web (Custom Tabs y Safari View Controller) ofrecerán máxima compatibilidad para las videollamadas. Otros marcos como WebView para Android y iOS son compatibles pero podrías experimentar ciertos bugs activos en este tipo de integración.

{% hint style="info" %}
En caso de bugs pueden enviarnos un correo a [developers@videsk.io](mailto:developers@videsk.io) o bien desde tu dashboard.
{% endhint %}

