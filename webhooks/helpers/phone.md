# #phone

Este helper está diseñado para ayudarte a extraer o transformar el valor de un número de teléfono de forma sencilla a estructuras personalizadas.

Habitualmente usarás este helper para identificar valores del número de teléfono en Webhooks hacia plataformas para envío de notificaciones como SMS, llamadas telefónicas, WhatsApp, Telegram u otros.

## Modo de uso

Este helper debe recibir tres valores en el siguiente orden:

1. `phone`: Número de teléfono que deberás extraer desde los datos
2. `country`: Código del país, que deberás extraer desde los datos
3. `format`: El formato de salida que esperas. Los valores disponibles son: `code`, `code-plus`, `international` y `national`.

{% code title="Ejemplo" %}
```handlebars
{{phone customer.phone location.countryCode 'international' }}
```
{% endcode %}

En el caso de este ejemplo, la salida sería `+12345678900`.

{% code title="Ejemplo full" %}
```handlebars
{
    "code": {{phone customer.phone location.countryCode 'code' }},
    "number": {{phone customer.phone location.countryCode 'national' }},
    "fullNumber": {{phone customer.phone location.countryCode 'international' }},
}
```
{% endcode %}

## Formatos

La diferencia entre `international` y `national`, es que el primer contiene el codigo de país y el símbolo `+`. Y entre de formato entre `code` y `code-plus` es que este último incluye el símbolo `+` como sufijo.

El valor del número de teléfono puede ser con o sin código de país, con o sin espacios e no sensible si incluye el símbolo `+`. Es decir, `+12345678900`, `12345678900`, `2345678900` o `+1 234 567 8900`.

### `international`

```handlebars
{{phone 12345678900 'US' 'international' }}
```

Salida: `+12345678900`

### `national`

```handlebars
{{phone 12345678900 'US' 'national' }}
```

Salida: `2345678900`

### `code`

```handlebars
{{phone 12345678900 'US' 'code' }}
```

Salida: `1`

### `code-plus`

```handlebars
{{phone 12345678900 'US' 'code-plus' }}
```

Salida: `+1`
