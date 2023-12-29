# BeamPortFile

[REPLACE_CODE_FORMAT]BeamPortFile[REPLACE_CODE_FORMAT] is a constructor type designed to create a custom file instance, extending the native [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File/File) constructor. It starts with 0 bytes but can mutate its buffer over time.

## Properties

### `filename`

This property corresponds to the filename, including the extension.

### `crc32`

This property corresponds to the file's integrity as a 4-byte checksum.

### `size`

This property delivers the file's size in bytes.

### `mimeType`

This property indicates the [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types) of the file.

### `data`

This property is an `Array` of `ArrayBuffer`, which is the list of chunks as buffers.

### `buffered`

This property indicates the amount of data added to the buffer while receiving chunks.

### `percentage`

This property indicates the percentage of the file in the buffer, ranging from 0 to 100, during reception using the [`add`](beamportfile.md#add) method. This property is based on [`buffered`](beamportfile.md#buffered).

## Methods

### `add`

This method allows adding `ArrayBuffer` chunks to the buffer.

```javascript
[REPLACE_CODE_FORMAT]beamPortFile.add(chunk);[REPLACE_CODE_FORMAT]
```

### `arrayBuffer`

This asynchronous method allows converting the file to an `ArrayBuffer` as the output value.

```javascript
await [REPLACE_CODE_FORMAT]beamPortFile.arrayBuffer();[REPLACE_CODE_FORMAT]
```

### `blob`

This method allows converting the file into a `Blob` as the output value.

```javascript
[REPLACE_CODE_FORMAT]beamPortFile.blob();[REPLACE_CODE_FORMAT]
```