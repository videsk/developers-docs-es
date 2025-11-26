# Propiedades

A continuación, exponemos las propiedades disponibles, con sus descripciones y los tipos de datos de entrada.

## `localStream`

**Tipo:** `MediaStream | undefined` (solo lectura)

Retorna el stream de medios local (cámara y micrófono) si está activo.

```javascript
const stream = webrtc.localStream;
```

**Retorna:**

* `MediaStream` si hay un stream local activo
* `undefined` si no hay stream o el stream no está activo

***

## `layout`

**Tipo:** `string` (lectura/escritura)

Obtiene o establece el layout de visualización de los peers.

```javascript
// Obtener layout actual
const currentLayout = webrtc.layout;
console.log('Layout actual:', currentLayout);

// Establecer layout
webrtc.layout = 'grid';     // Vista en cuadrícula
webrtc.layout = 'sidebar';  // Vista con sidebar
```

**Valores permitidos:**

* `'sidebar'`: Layout con barra lateral
* `'grid'`: Layout en cuadrícula

**Nota:** Intentar establecer un valor no válido mostrará una advertencia en consola y no aplicará el cambio.

***

## `alias`

**Tipo:** `string | undefined` (lectura/escritura)

Alias legible para identificar al usuario actual. Este alias se propaga a través de los eventos y facilita la identificación de peers en la UI.

```javascript
// Asignar alias
webrtc.alias = 'John Doe';

// Obtener alias
const currentAlias = webrtc.alias;
console.log('Mi alias:', currentAlias);

// El alias estará disponible en eventos de otros peers
webrtc.addEventListener('peer:quality', (event) => {
    console.log(`Peer ${event.detail.alias} tiene problemas`);
});
```

**Retorna:**

* `string` si se ha asignado un alias
* `undefined` si no se ha asignado

