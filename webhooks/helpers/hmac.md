# #hmac

Este helper genera una firma HMAC a partir de los datos proporcionados, usada habitualmente para verificar la autenticidad e integridad de solicitudes en Webhooks.

{% hint style="info" %}
A diferencia del helper `#jwt`, `hmac` es un helper inline — no requiere bloque de apertura y cierre.
{% endhint %}

## Modo de uso

```handlebars
{{hmac data secret algorithm encoding}}
```

| Parámetro   | Tipo     | Requerido | Por defecto |
|-------------|----------|-----------|-------------|
| `data`      | `String` | ✓         | —           |
| `secret`    | `String` | ✓         | —           |
| `algorithm` | `String` | ✗         | `sha256`    |
| `encoding`  | `String` | ✗         | `hex`       |

### Ejemplos

{% tabs %}
{% tab title="Básico" %}
```handlebars
{{hmac body secrets.webhookSecret}}
```
{% endtab %}

{% tab title="Con algoritmo" %}
```handlebars
{{hmac body secrets.webhookSecret 'sha512'}}
```
{% endtab %}

{% tab title="Con algoritmo y encoding" %}
```handlebars
{{hmac body secrets.webhookSecret 'sha256' 'base64'}}
```
{% endtab %}

{% tab title="Datos anidados" %}
```handlebars
{{hmac webhook.body config.apiSecret}}
```
{% endtab %}
{% endtabs %}

## Configuración

### `data`

Los datos que se firmarán. Puede ser un `String` estático o una referencia a una variable del contexto. Los valores numéricos se convierten automáticamente a `String`.

{% hint style="danger" %}
Si `data` está vacío, el helper retornará un error: `Error: Data to sign is required`.
{% endhint %}

```handlebars
{{hmac payload secrets.key}}
```

### `secret`

La clave secreta con la que se generará la firma HMAC. Debe ser de tipo `String`.

{% hint style="danger" %}
Siempre entrega el secreto a través de `secrets` y nunca como valor estático en el template.
{% endhint %}

```handlebars
{{hmac payload secrets.webhookSecret}}
```

### `algorithm`

Algoritmo de hash a utilizar. El valor por defecto es `sha256`.

Los valores disponibles son los soportados por Node.js `crypto`: `sha1`, `sha256`, `sha384`, `sha512`, entre otros.

{% hint style="info" %}
El algoritmo debe coincidir con el que espera el servidor de destino al momento de verificar la firma.
{% endhint %}

```handlebars
{{hmac payload secrets.key 'sha512'}}
```

### `encoding`

Formato de salida de la firma generada. El valor por defecto es `hex`.

| Valor       | Descripción                                          |
|-------------|------------------------------------------------------|
| `hex`       | Hexadecimal. El más común en integraciones webhook.  |
| `base64`    | Base64 estándar. Puede contener `+`, `/` y `=`.      |
| `base64url` | Base64 URL-safe. Sin `+`, `/` ni `=`.                |
| `latin1`    | Encoding binario Latin-1.                            |
| `binary`    | Alias de `latin1`.                                   |

{% hint style="warning" %}
Si el encoding proporcionado no está en la lista anterior, el helper retornará un error: `Error: Invalid encoding`.
{% endhint %}

```handlebars
{{hmac payload secrets.key 'sha256' 'base64url'}}
```

## Errores comunes

| Error | Causa |
|---|---|
| `Error: Data to sign is required` | El parámetro `data` está vacío o no resuelve ningún valor. |
| `Error: Secret key is required` | El parámetro `secret` está vacío o no resuelve ningún valor. |
| `Error: Invalid encoding: <valor>` | El encoding indicado no está entre los soportados. |
| `Failed to generate HMAC: <detalle>` | El algoritmo indicado no es válido o no está soportado por Node.js `crypto`. |
