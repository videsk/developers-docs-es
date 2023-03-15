# Eventos

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

## `token-error`

Este evento se emitirá cuando el token proporcionado sea erróneo, mal formado o inválido. Esto podría eventualmente suceder si un administrador de cuenta, elimina la integración desde la cuenta.

{% hint style="info" %}
Esto deberá ser escuchado, solo en caso de ambiente de desarrollo.
{% endhint %}

```javascript
phone.on['token-error'] = () => {
    // Verificar token
};
```

## `no-agents`\*

Este evento se emitirá cuando no existan agentes conectados en tu cuenta luego de haber intentado la llamada mediante el método `phone.call()`.

```javascript
phone.on['no-agents'] = () => {
  // Muestra un mensaje que no hay agentes disponibles
};
```

## `queued`\*

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

## `queue-updated`\*

Este evento se emitirá cuando se actualice la posición en la fila, solo posterior al evento `queued`. **Es de suma relevancia que escuches este evento.**

```javascript
phone.on['queue-updated'] = (event) = {
    const { position } = event;
    // Actualizar posición en la fila
};
```

## `customer-leave`\*

Este evento se emitirá cuando se ejecuta el evento `phone.leave()` estando en la fila de espera.

```javascript
phone.on['customer-leave'] = () => {
    // Mostrar un mensaje de abandono de fila
};
```

## `dismissed`\*

Este evento se emitirá cuando un agente rechace la llamada.

```javascript
phone.on['dismissed'] = () => {
    // Mostrar un mensaje de llamada rechazada
};
```

## `out-queue`

Este evento se emite cuando la llamada ha sido contestada por un agente. **Es opcional escuchar este evento**.

```javascript
phone.on['out-queue'] = () => {
    // No es necesario modificar nada
};
```

## `answered`\*

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
Recuerda que deberás cargar nuestro WebRTC con anterioridad. Para más información visíta la documentión de [WebRTC SDK](../webrtc/).
{% endhint %}

## `connected-call`

Este evento se emite cuando se ha conectado a la llamada de forma exitosa. **Es opcional escuchar este evento**.

```javascript
phone.on['connected-call'] = () => {
    // No es necesario modificar nada
};
```

## `agent-disconnect`

Este evento se emite cuando el agente quién contestó la llamada eventualmente se desconecta de la videollamada por problemas de red. **Es opcional escuchar este evento**.

{% hint style="warning" %}
No deberás terminar la llamada, ya que el agente se reconectará de forma automática. En caso de traspasar varios minutos nuestra API terminará la llamada de forma automática.
{% endhint %}

```javascript
phone.on['agent-disconnect'] = () => {
    // Mostrar un mensaje de agente desconectado
};
```

## `customer-hangup`

Este evento se emite cuando se ejecuta el método `phone.hangup()`. **Es opcional escuchar este evento**.

```javascript
phone.on['customer-hangup'] = () => {
    // Muestra un mensaje de llamada finalizada
};
```

## `ended`\*

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

## `transferred-segment`\*

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

## `transferred-agent`\*

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

## `connection-error`

Este evento se emitirá cuando exista algún error en la red o parámetros mal formados que se enviaron a la API. **Es opcional escuchar este evento**.

```javascript
phone.on['connection-error'] = (event) => {
    const { event, code, name, message, date, errors } = event;
}
```

## `network-issues`\*

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

## `http-block`

Este evento se emitirá cuando nuestra API detecte actividad sospechosa como un bot o una llamada desde una red poco confiable. **Es opcional escuchar este evento**.

{% hint style="info" %}
Este tipo de comportamiento no es configurable, el cual permite entregar una mejor calidad de servicio a todos nuestros clientes, bloqueando potenciales atacantes o bots.
{% endhint %}

```javascript
phone.on['http-block'] = () => {
    // Mostrar mensaje de red poco confiable
};
```

## `transport-disconnect`

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
