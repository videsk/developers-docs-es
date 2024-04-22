# #jwt

Este tipo de helper tiene como utilidad generar un JWT basado en los valores de ingreso a través de `payload`, `privateKey` y `options`.

Habitualmente usarás este JWT se utilizará en las cabeceras o `headers` de la solicitud Webhooks.

{% hint style="info" %}
Evita usar este helper, prefiere usar un medio de autenticación que no requiera autorizar a nuestra aplicación a generar credenciales válidas, es decir, prefiere almacenar en secretos una credencial caducable o bloqueable.
{% endhint %}

{% hint style="danger" %}
Se recomienda, entregar `payload`, `privateKey` y `options` como secretos en vez de basados en body.&#x20;
{% endhint %}

{% hint style="warning" %}
Es probable que en el editor de Webhooks no sea posible visualizar en vivo un JWT válido, debido a las limitantes criptográficas.
{% endhint %}

## Modo de uso

Para generar un JWT se requieren tres componentes principales cada uno de ellos con sus propias opciones dependiendo de tus necesidades. El contenido del helper debe ser un `JSON` válido, es decir, sus keys/claves deben contener doble comilla, no puede ser un `Object`.

{% code title="Estructura" %}
```handlebars
{{#jwt}}
    {
        "payload": (String|JSON),
        "privateKey": String,
        "options": JSON
    }
{{/jwt}}
```
{% endcode %}

### Modos de generación

Dependiendo de tu necesidad te sugerimos dos modos con el que podrás usar este helper.

En el **modo dinámico** es cuando requieres que los valores del `payload` u `options` se generen en base a los datos dinámicos.

Y más recomendado, el **modo estático** que te permitiría generar JWT sin necesidad de ingresar datos dinámicos, ya que la expiración puede quedar configurada como relativa.

{% tabs %}
{% tab title="Dinámico" %}
```json
{{#jwt}}
    {
        "payload": {
            "user": {{parser agent._id}}
        },
        "privateKey": {{ secrets.privateKey }},
        "options": {
            "expiresIn": "1m"
        }
    }
{{/jwt}}
```
{% endtab %}

{% tab title="Estático" %}
```handlebars
{{#jwt secrets.jwtOptions }}{{/jwt}}
```
{% endtab %}
{% endtabs %}

## Configuración

### `payload`

El payload es el contenido (visible) que desees que vaya en el JWT, que puede ser un `String` o bien un `Object`.

{% hint style="danger" %}
No ingreses secretos en este campo ya que son visibles al momento de decodificar un JWT.
{% endhint %}

{% code title="Ejemplo" %}
```handlebars
{{#jwt}}
    {
        "payload": { "user": {{parser agent._id}} },
        ...
    }
{{/jwt}}
```
{% endcode %}

### `privateKey`

El `privateKey` es el secreto con el cual se firmará el JWT. El tipo de dato debe ser solo un `String`.

{% code title="Ejemplo" %}
```handlebars
{{#jwt}}
    {
        "privateKey": "..."
    }
{{/jwt}}
```
{% endcode %}

### `options`

Las opciones para generar un JWT son variadas, dependiendo de tu necesidad. Puedes leer los [campos estándares usados en un JWT aquí](https://en.wikipedia.org/wiki/JSON\_Web\_Token).

{% hint style="success" %}
Escoge los valores de cada opción siempre con la seguridad como primera prioridad.
{% endhint %}

#### `algorithm`

Algoritmo a usar para cifrar el JWT. Los valores disponibles son `HS256`, `HS384`, `HS512`, `RS256`, `RS384`, `RS512`, `ES256`, `ES384`, `ES512`, `RS256`, `RS384`, `RS512`. El valor por defecto es `HS256`.

{% hint style="info" %}
El algoritmo debe coincidir con los aceptados por el servidor de destino.
{% endhint %}

```json
{ "algorithm": "HS256" }
```

#### `audience`

Dentifica a los destinatarios para los que está destinado el JWT. Debe ser de tipo `String`.

```json
{ "audience": "..." }
```

#### `subject`

Identifica el tema del JWT. Debe ser de tipo `String`.

```json
{ "subject": "..." }
```

#### `issuer`

Identifica el sujeto que emitió el JWT. Debe ser de tipo `String`.

```json
{ "issuer": "..." }
```

#### `header`

{% hint style="warning" %}
Este campo puede sobreescribir el valor del algoritmo.
{% endhint %}

Identifica qué algoritmo se utiliza para generar la firma. Debe ser de tipo `JSON`. Los valores del `JSON` deben ser `alg` y `typ`.

```json
{ "alg": "HS256", "typ": "JWT" }
```

#### `jwtid`

Identificador único del token que distingue entre mayúsculas y minúsculas, incluso entre diferentes emisores.

```json
{ "jwtid": "..." }
```

#### `expiresIn`

Identifica el tiempo de vencimiento a partir del cual el JWT no debe aceptarse para su procesamiento. Debe ser de tipo `String`, bajo el siguiente formato:

* milisegundos: `800ms` o `800 milliseconds`
* segundos: `5s` o `5 seconds`
* minutos: `5m` o `5 minutes`
* horas: `1h` o `1 hours`
* días: `2d` o `2 days`
* semanas: `1w` o `1 week`
* meses: `2mo` o `2 months`
* año: `1y` o `1 year`

```json
{ "expiresIn": "5s" }
```

{% hint style="info" %}
Recomendamos mantener el tiempo de expiración no mayor a 1 minuto y no menor a 5 segundos. Generamos el JWT justo antes de enviar la solicitud.
{% endhint %}

#### `notBefore`

Identifica la hora en la que el JWT comenzará a ser aceptado para su procesamiento.

El formato es equivalente a como funciona para **`expiresIn`**.

```json
{ "notBefore": "1s" }
```

{% hint style="danger" %}
Sugerimos no utilizar esta opción ya que puede provocar errores en la autenticación.
{% endhint %}
