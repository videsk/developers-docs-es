# BeamPortFile

`BeamPortFile` es un tipo de constructor diseñado para crear una instancia de archivo personalizada al constructor nativo [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File/File), que inicio con 0 bytes pero puede mutar su buffer durante el tiempo.

## Propiedades

### `filename`

Esta propiedad corresponde al nombre del archivo, incluye extensión.

### `crc32`

Esta propiedad corresponde a la integridad de un archivo como cálculo de un número de 4 bytes.

### `size`

Esta propiedad entrega el valor del archivo en bytes.

### `mimeType`

Esta propiedad indica el [tipo MIME](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types) del archivo.

### `data`

Esta propiedad es un `Array` de `ArrayBuffer`, es decir, el listado de chunks como buffer.

### `buffered`

Esta propiedad indica la cantidad de datos añadidos en buffer mientras se reciben los chunks.

### `percentage`

Esta propiedad indica el porcentaje del archivo en buffer, de 0 a 100, durante la recepción usando el método [`add`](beamportfile.md#add). Esta propiedad se basa en [`buffered`](beamportfile.md#buffered).

## Métodos

### `add`

Este método permite añadir chunks de `ArrayBuffer` al buffer.

```javascript
beamPortFile.add(chunk);
```

### `arrayBuffer`

Este método asíncrono permite convertir el archivo a un `ArrayBuffer` como valor de salida.

```javascript
await beamPortFile.arrayBuffer();
```

### `blob`

Este método permite convertir el archivo en un `Blob` como valor de salida.

```javascript
beamPortFile.blob();
```
