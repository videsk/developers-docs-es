---
description: >-
  SDK para generar formularios y encuestas generados en su cuenta mediante
  Javascript.
---

# 📄 Formularios

{% hint style="warning" %}
La documentación y recursos necesarios para utilizar Forms SDK está estrictamente restringido para uso de clientes de Videsk. Nos reservamos el derecho de restringir su acceso y uso, si detectamos un uso inadecuado.
{% endhint %}

## Instalación

Para utilizar Forms SDK podrás instarlo mediante nuestro CDN.

{% tabs %}
{% tab title="HTML" %}
```html
<link rel="stylesheet" href="https://cdn.videsk.io/sdk/forms.min.css" />
<script src="https://cdn.videsk.io/sdk/forms.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const link = document.createElement('link');
link.rel = "stylesheet";
link.href = "https://cdn.videsk.io/sdk/forms.min.css";
document.head.appendChild(link);

const script = document.createElement('script');
script.src = 'https://cdn.videsk.io/sdk/forms.min.js';
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Debes cargar ambos recursos CSS y JS, de lo contrario Forms no funcionará correctamente.
{% endhint %}

## Modo de uso

{% code lineNumbers="true" %}
```javascript
const form = new FormSDK({ target: document.querySelector('#form-container') });
```
{% endcode %}

De forma simple puedes instanciar Forms. Posteriormente deberás definir oyentes de eventos y adjuntar métodos a un botón personalizado.

## Propiedades

### `data`

Con esta propiedad podrás obtener el formulario con sus campos sin necesidad de llamar al método `submit`.

```javascript
form.data
// output
[{...}]
```

## Métodos

Ya instanciado el SDK podrás acceder a los siguientes métodos:

### `on`

Este método tiene como objetivo que definas un oyente cuando un evento ocurra. Los dos argumentos que recibe son:

* `event`: nombre del evento
* `callback`: función que se ejecutará al ocurrir el evento

```javascript
form.on('submit', callback);
```

### `render`

Con este método renderizas los campos del formulario. Los dos argumentos que recibe son:

* `form`: array de campos obtenido por [SDK](phone.md#obtener-formulario) o API
* `readonly`: define si son de lectura o escritura, por defecto `false`

```javascript
form.render(values);
```

### submit

Este método permite enviar el formulario activando la validación de campos y posteriormente el evento `submit`.

Puedes obtener los valores de los campos y su validez mediante un valor retorno de tipo `object` que contiene `data` (array) y `valid` (boolean).

```javascript
const response = form.submit();
const { data, valid } = response;
```

{% hint style="info" %}
Te sugerimos trabajar con eventos, ya que tendrás mayor control sobre las acciones `submit` del formulario. **Evita usar los valores de retorno**.
{% endhint %}

### `set/update`

Con este método podrás actualizar el **valor de un campo** en específico mediante sus propiedades como: `name`, `label`, `type`, `value` y `_id`. Este método recibe cuatro argumento:

* **`name`**: valor con el cual se va a buscar el campo
* **`value`**: valor a insertar en el campo
* `property`: propiedad a modificar, por defecto es `value`
* `key`: nombre de la propiedad a buscar, por defecto es `name`

{% tabs %}
{% tab title="Insertar valor" %}
```javascript
form.set('customer_email', 'john@example.com');
```
{% endtab %}

{% tab title="Campo requerido" %}
```javascript
form.set('customer_email', true, 'properties.required', 'name');
```
{% endtab %}

{% tab title="Campo solo lectura" %}
```javascript
form.set('email', true, 'properties.readonly', 'type');
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Disponemos de un método envoltorio que puede facilitar el uso.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
// Actualizar por name del campo
form.update('value', 'john@example.com').of('customer_email');
form.update('value', 'john@example.com').of('customer_email', 'name');
// Actualizar por _id
form.update('properties.required', true).of('60fb2623854bb563f843ba09', '_id');
```
{% endcode %}

### `destroy`

Este método elimina por completo el nodo HTML donde se renderizó.

```javascript
form.destroy();
```

{% hint style="info" %}
Te sugerimos como buena práctica usar este método una vez que no necesitas el formulario, es decir, es enviado exitosamente.
{% endhint %}

## Eventos

Los eventos disponibles son `submit`, `ready`, `updated`, `error`.

### `submit`

Este evento se produce una vez que se ejecuta el método `submit()`. El único argumento callback es un `object` compuesto de:

* `valid`: boolean que indica si todos los campos son válidos

```javascript
form.on('submit', (event) => {
    const { valid } = event;
});
```

{% hint style="info" %}
Con este evento deberás usar [Captcha](captcha.md) **si es un formulario**, no una encuesta.
{% endhint %}

{% hint style="warning" %}
[Captcha](captcha.md) no es opcional para formularios base o de contacto, excepto para encuestas.
{% endhint %}

### `ready`

Con este evento podrás oír cuando el formulario ha sido renderizado exitosamente. No contiene argumento callback.

```javascript
form.on('ready', () => {});
```

### `updated`

Con este evento podrás escuchar la actualización del valor de un campo. El argumento callback es un `object` compuesto de:

* `_id`: corresponde el id del campo actualizado como `string`.
* `value`: corresponde al valor del campo, el cual puede ser `string`, `boolean`, `array` o `number`.

```javascript
form.on('updated', event => {
    const { _id, value } = event;
});
```

### `error`

Con este evento podrás escuchar errores que solo podrían surgir al momento de renderizar el formulario. Contiene tres argumentos compuestos de:

* `name`: nombre del error como `string`
* `code`: código del error los puede ser `400` y `403`
* `message`: mensaje legible sobre el error

{% hint style="info" %}
Esto solo **podría ocurrir si insertas un formulario generado manualmente**. Se recomienda siempre administrar los formularios desde tu [cuenta dashboard](https://app.videsk.io/forms).
{% endhint %}

```javascript
form.on('error', (name, code, message) => {
    // Catch with ingestor o similar
});
```

## Ejemplo

```javascript
const form = new FormSDK({ target: document.querySelector('#form-container') });

// Listen when submit the form
form.on('submit', ({ valid }) => {
  if (valid) doSomething();
});

// Attach submit to custom button
document.querySelector('#myButton').addEventListener('click', () => form.submit());

// Render the form
form.render(arrayWithFormElements);
```
