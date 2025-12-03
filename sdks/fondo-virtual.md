# 🖼️ Fondo virtual

SDK para procesar y reemplazar el fondo de un stream de video en tiempo real mediante segmentación basada en ML.

{% hint style="warning" %}
**Este SDK es diseñado y propiedad de Videsk, uso no autorizado será sancionado por ley.**&#x20;
{% endhint %}

***

## Instalación

El SDK se distribuye a través de CDN.

{% hint style="success" %}
Para acceder al SDK (`URL`), favor de contactar con tu ejecutivo de cuenta.
{% endhint %}

{% hint style="warning" %}
Está prohibido el uso de este SDK por parte de terceros que no tengan relación contractual con Videsk.&#x20;

**Cualquier uso no autorizado será sancionado por ley.**

🚨 El uso de este SDK está monitoreado activamente.
{% endhint %}

#### ESM (Recomendado)

Para proyectos modernos, importa el módulo directamente desde la URL:

```javascript
import VirtualBackground from 'URL';
```

#### IIFE (Legacy)

Si necesitas usarlo mediante etiqueta `<script>` clásica (expone `window.VirtualBackground`):

```javascript
<script src="URL"></script>
```

***

## Uso Básico

El flujo de trabajo estándar requiere: Importar, Configurar y Procesar.

#### 1. Inicialización y Configuración

```javascript
import VirtualBackground from 'URL';

// Instanciar
const virtualBackground = new VirtualBackground({ frameRate: 15 }); // 15 FPS recomendado

// Opción A: Aplicar Blur (Intensidad numérica)
virtualBackground.blur = 7;

// Opción B: Aplicar Imagen (URL)
// virtualBackground.image = 'https://mi-cdn.com/fondo.jpg';
```

#### 2. Renderizar y Comenzar

El SDK intercepta el `MediaStream` de la cámara y devuelve uno nuevo procesado.

```javascript
// 1. Obtener stream original de la cámara
const cameraStream = await navigator.mediaDevices.getUserMedia({ 
    video: { width: 640, height: 480 } 
});

// 2. Preparar el worker (Render)
// Solo es necesario si no hay un input activo
if (!virtualBackground.input?.active) {
    await virtualBackground.render(cameraStream);
}

// 3. Iniciar el procesamiento y obtener el nuevo stream
const outputStream = virtualBackground.start();

// 4. Usar el stream resultante (ej. en un elemento <video>)
document.querySelector('#my-video').srcObject = outputStream;
```

***

## Métodos y Propiedades

| **Método/Propiedad** | **Tipo**      | **Descripción**                                             |
| -------------------- | ------------- | ----------------------------------------------------------- |
| `blur`               | `number`      | Define la intensidad del desenfoque. Activa modo blur.      |
| `image`              | `string`      | URL de la imagen de fondo. Activa modo imagen.              |
| `render(stream)`     | `Promise`     | Inicializa el Worker y Canvas con el stream de origen.      |
| `start()`            | `MediaStream` | Inicia el bucle de procesamiento y retorna el stream final. |
| `pause()`            | `Promise`     | Detiene el procesamiento (reduce consumo CPU a 0).          |

***

## Ejemplo Completo (ESM)

Puedes copiar y pegar este bloque en un archivo HTML para probarlo rápidamente (requiere servidor local o contexto seguro HTTPS).

```html
<video id="preview" autoplay playsinline style="width: 640px; height: 480px; background: #000;"></video>

<script type="module">
  import VirtualBackground from 'URL';

  const run = async () => {
    try {
      // 1. Configuración inicial
      const vb = new VirtualBackground({ frameRate: 15 });
      const videoEl = document.getElementById('preview');

      // 2. Obtener cámara (resolución moderada para mejor performance)
      const stream = await navigator.mediaDevices.getUserMedia({ 
        video: { width: 640, height: 480 } 
      });

      // 3. Configurar efecto
      vb.blur = 8; 

      // 4. Iniciar SDK
      await vb.render(stream);
      const processedStream = vb.start();

      // 5. Visualizar
      videoEl.srcObject = processedStream;

    } catch (error) {
      console.error('Error al iniciar Virtual Background:', error);
    }
  };

  run();
</script>
```

***

## ⚠️ Rendimiento y Requisitos

Esta funcionalidad realiza segmentación de video _frame a frame_ en tiempo real. El consumo de recursos es intensivo.

#### Estimación de Consumo de Recursos

{% hint style="info" %}
Los valores a continuación son aproximados y pueden variar significativamente según la arquitectura del dispositivo y la carga del sistema.
{% endhint %}

| **Recurso** | **Impacto** | **Consumo Estimado (Aprox.)** | **Notas**                                                            |
| ----------- | ----------- | ----------------------------- | -------------------------------------------------------------------- |
| CPU         | Alto        | \~2 a 4 Cores dedicados       | El procesamiento de máscaras ocurre principalmente en CPU.           |
| RAM         | Alto        | +500 MB                       | Memoria adicional requerida solo para este proceso (Workers/Canvas). |
| GPU         | Moderado    | N/A                           | Utilizado para la inferencia del modelo TFLite.                      |

#### Requisitos Mínimos Recomendados (para 15 FPS estables)

| **Componente** | **Especificación Mínima** | **Recomendación de Configuración**                               |
| -------------- | ------------------------- | ---------------------------------------------------------------- |
| Procesador     | 4 Cores Físicos           | Intel Core i5 8va Gen / Ryzen 5 o superior.                      |
| Memoria        | 8 GB RAM Total            | Asegurar al menos 1 GB libre antes de iniciar la llamada.        |
| Resolución     | VGA (640x480)             | Crucial: Resoluciones HD (720p+) pueden causar latencia extrema. |

{% hint style="info" %}
Nota sobre Móviles: Aunque la funcionalidad ha sido testeada técnicamente en dispositivos móviles, no se recomienda su uso en producción. La combinación del procesamiento de video nativo de la videollamada más la segmentación por IA suele saturar la capacidad térmica y de batería de la mayoría de los smartphones, degradando la experiencia de usuario.
{% endhint %}

***

### Compatibilidad de Navegadores

El SDK requiere soporte robusto para `OffscreenCanvas`, `Web Workers` y `WebAssembly`.

| **Navegador**     | **Estado**       | **Versión Mínima** | **Notas**                                                                          |
| ----------------- | ---------------- | ------------------ | ---------------------------------------------------------------------------------- |
| Chrome / Chromium | ✅ Soportado      | 90+                | Mejor rendimiento (motor V8 optimizado).                                           |
| Edge              | ✅ Soportado      | 90+                | Basado en Chromium, rendimiento idéntico a Chrome.                                 |
| Firefox           | ✅ Soportado      | 105+               | Soporte completo de OffscreenCanvas añadido recientemente.                         |
| Safari (macOS)    | ⚠️ Parcial       | 16.4+              | Requiere las últimas versiones para soporte estable de OffscreenCanvas en workers. |
| Safari (iOS)      | ⛔ No Recomendado | -                  | Restricciones térmicas y de gestión de memoria severas.                            |
| Chrome (Android)  | ⚠️ Experimental  | -                  | Funciona técnicamente, pero no recomendado por performance.                        |
