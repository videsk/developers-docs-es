# Eventos

Los siguientes eventos te permiten escuchar diferentes estados al momento de intercambiar archivos.

Los siguientes eventos los deberás escuchar desde la instancia de [Phone](../phone.md) SDK, **no** desde una instancia de `FileShare`, esto debido a que se hará cargo de emitir eventos cuando sea necesario.

{% embed url="https://www.figma.com/file/2i9FRajfNU50zYjcNC3Tmu/Fileshare-Events-Flow?node-id=0%3A1" %}

## `fileshare-ready`

Este evento se emite cuando la conexión de alta velocidad esta completada y lista para transferir archivos.

```javascript
phone.addEventListener('fileshare-ready', () => {
    const fileshare = phone.extensionGetModule('fileshare');
    // Do something
});
```

## `fileshare-closed`

Este evento se emite cuando la conexión de alta velocidad se cierra producto de problemas de red.

```javascript
phone.addEventListener('fileshare-closed', () => {
    // Do something
});
```

## `fileshare-canceled`

Este evento se emite cuando un archivo que esta en progreso de envío se cancela antes de completarse o ha fallado en el transporte.

```javascript
phone.addEventListener('fileshare-canceled', () => {
    // Do something
});
```

## `fileshare-new-file`

Este evento se emite cuando se adjunta un nuevo archivo, pero aún no ha sido enviado.

```javascript
phone.addEventListener('fileshare-new-file', event => {
    const { side, data } = event.detail;
    // Do something
});
```

{% hint style="info" %}
Este evento se emitará por cada archivo añadido o a enviar.
{% endhint %}

## `fileshare-file-removed`

Este evento se emite cuando un archivo adjunto pero no enviado, se elimina de la bandeja de envió.

```javascript
phone.addEventListener('fileshare-file-removed', event => {
    const { fileId } = event.detail;
    // Do something
});
```

## `fileshare-completed`

Este evento se emite cuando un archivo en proceso de envío se ha completo exitosamente.

```javascript
phone.addEventListener('fileshare-completed', event => {
    const { queueIndex, status } = event.detail;
    // Do something
});
```

## `fileshare-progress`

Este evento se emite cuando se está en proceso de envío de un archivo, indicando su progreso.

```javascript
phone.addEventListener('fileshare-progress', event => {
    const { fileId, progress } = event.detail;
    // Do something
});
```
