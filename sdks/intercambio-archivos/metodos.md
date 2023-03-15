# Métodos

Los siguientes métodos te permiten acceder a funciones que cambiarán el comportamiento o ayudantes para ciertas acciones.

Para usar los siguientes métodos debes usar la instancia generada por [Phone](../phone/) SDK.

```javascript
const fileshare = phone.extensionGetModule('fileshare');
```

## `add`

Este método permite adjuntar archivos a la lista, pero no se enviaránc hasta usar el método `send`. Para obtener este archivo debes hacer uso de un elemento DOM de tipo `file` y el archivo a&#x20;

```javascript
fileshare.add(file);
```

El tipo de elemento DOM HTML es el siguiente (ejemplo):

{% hint style="info" %}
Puedes pasar como argumento un único archivo o como lista `FileList`.
{% endhint %}

```html
<input type="file" accept="image/*,.pdf" />
```

La documentación oficial de `input` file [está aquí](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file).

## `send`

Este método permite enviar los archivos que estén en el listado de archivos, pero no han sido enviados.

```javascript
fileshare.send();
```

## `cancel`

Este método permite cancelar el envío de archivos en curso.

{% hint style="info" %}
Esto cancelará todos los archivos en curso de envío, no es posible cancelar individualmente
{% endhint %}

```javascript
fileshare.cancel();
```

## `download`

Este método permite descargar un archivo en particular al dispositivo. Para ello debes proporcionar el id del archivo, el cual podrás encontrar en el listado `fileshare.queue`.

```javascript
fileshare.download(fileId);
```

## `remove`

Este método permite eliminar un archivo que aún no se ha enviado o no se está enviando. Para ello debes proporcionar el id del archivo, el cual podrás encontrar en el listado `fileshare.queue`.

```javascript
fileshare.remove(fileId);
```

## `find`

Este método puedes buscar fácilmente el archivo el cual retorna un valor como `Object`. El único argumento que debes proporcionar el id del archivo.

```javascript
fileshare.find(fileId);
```
