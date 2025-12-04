# 🖼️ Fondo virtual

SDK propietario de **Videsk** para procesar y reemplazar el fondo de un stream de video en tiempo real mediante segmentación basada en Machine Learning y renderizado acelerado por hardware (WebGL2).

{% hint style="warning" %}
**⚠️ Aviso Legal**

Este SDK es propiedad intelectual de Videsk. El uso no autorizado o por parte de terceros sin relación contractual está prohibido y será sancionado por ley. El uso de este SDK es monitoreado activamente.
{% endhint %}

## Instalación

{% hint style="info" %}
El SDK se distribuye a través de CDN. Para obtener la `URL` de acceso, contacte a su ejecutivo de cuenta.
{% endhint %}

{% tabs %}
{% tab title="ESM (Recomendado)" %}
```javascript
import VirtualBackground from 'URL_DEL_SDK';
```

Para proyectos modernos con bundlers (Vite, Webpack) o módulos nativos de navegador:
{% endtab %}

{% tab title="IIFE (Legacy)" %}
```html
<script src="URL_DEL_SDK"></script>
```

Para inclusión directa mediante etiqueta script (expone `window.VirtualBackground`):


{% endtab %}
{% endtabs %}

***

## Uso Básico

El flujo de trabajo estándar consta de 3 fases: **Configuración**, **Renderizado** y **Consumo**.

#### 1. Inicialización

```javascript
import VirtualBackground from 'URL_DEL_SDK';

// Se recomienda limitar los FPS para controlar el consumo de CPU/GPU
const { frameRate } = VirtualBackground.getRecommendedSettings();
const virtualBackground = new VirtualBackground({ frameRate });
```

#### 2. Configuración del Efecto

Puedes cambiar el efecto en cualquier momento (incluso durante el stream).

```javascript
// Opción A: Blur (Desenfoque)
// Valor numérico: 0 (sin blur) a 20+ (muy borroso)
virtualBackground.blur = 7;

// Opción B: Imagen de Fondo
// Acepta URL absoluta o relativa (debe cumplir con CORS)
virtualBackground.image = 'https://mi-cdn.com/fondo.jpg';

// Para quitar la imagen y volver al blur:
virtualBackground.image = null;
```

#### 3. Procesamiento y Salida

El método `render()` Inicializa los Workers y el contexto WebGL. El método `start()` devuelve el nuevo `MediaStream`.

```javascript
// 1. Obtener stream de la cámara del usuario
const cameraStream = await navigator.mediaDevices.getUserMedia({
    video: { width: 640, height: 480 } // Resolución recomendada: VGA
});

// 2. Preparar el motor de renderizado (si no está activo)
if (!virtualBackground.isActive) {
    await virtualBackground.render(cameraStream);
}

// 3. Iniciar el bucle de procesamiento y obtener el stream procesado
virtualBackground.start();

// 4. Inyectar en el elemento de video
document.querySelector('#my-video').srcObject = virtualBackground.stream;
```

***

### API Reference

### Propiedades

| `blur`     | `number`  | Define la intensidad del desenfoque gaussiano. Si es `0`, el fondo se ve nítido. |
| ---------- | --------- | -------------------------------------------------------------------------------- |
| `image`    | `string`  | URL de la imagen de fondo. Si se establece, tiene prioridad sobre el `blur`.     |
| `isActive` | `boolean` | (Read-only) Indica si el SDK tiene un stream de entrada activo.                  |
| `options`  | `object`  | Objeto de configuración inicial (ej. `{ frameRate: 15 }`).                       |

### Métodos

| `render(stream)`         | `Promise<void>`                          | Inicializa los Web Workers, transfiere el `OffscreenCanvas` y carga los modelos de ML. Es el paso más pesado.                                         |
| ------------------------ | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `start()`                | `MediaStream`                            | Inicia el bucle de procesamiento de frames y devuelve el stream resultante (mezcla de audio original y video procesado).                              |
| `pause()`                | `MediaStream`                            | Detiene el procesamiento para reducir el consumo de CPU/GPU a casi cero, devolviendo el stream original sin procesar temporalmente.                   |
| `getRecommendedSettings` | `{ frameRate: Number, backend: String }` | Método estático que provee recomiendación del `frameRate` dependiendo de la arquitectura y compatibilidad del dispositivo (alterna entre 15 y 30 fps) |

***

## Tabla de Compatibilidad

El SDK utiliza tecnologías avanzadas del navegador para lograr rendimiento en tiempo real:

1. **Web Workers:** Para separar el procesamiento de la UI.
2. **OffscreenCanvas:** Para renderizar gráficos fuera del hilo principal.
3. **WebGL 2.0:** Para aceleración por hardware (GPU).
4. **WASM / SIMD:** Para la inferencia del modelo de IA.

| Navegador                 | Estado      | Versión Mínima | Notas Técnicas                                                                                             |
| ------------------------- | ----------- | -------------- | ---------------------------------------------------------------------------------------------------------- |
| **Chrome / Chromium**     | ✅ Soportado | 90+            | Motor V8 optimizado. Mejor rendimiento en `ImageBitmap` y `OffscreenCanvas`.                               |
| **Edge**                  | ✅ Soportado | 90+            | Basado en Chromium. Rendimiento idéntico a Chrome.                                                         |
| **Firefox**               | ✅ Soportado | 105+           | Soporte completo de `OffscreenCanvas` añadido en v105.                                                     |
| **Safari (macOS)**        | ⚠️ Parcial  | 16.4+          | Requiere Safari 16.4+ para soporte estable de `OffscreenCanvas` en Workers. Versiones anteriores fallarán. |
| **Safari (iOS / iPadOS)** | ⛔ No Rec.   | -              | Aunque técnicamente carga en 16.4+, la gestión térmica de iOS suele bloquear el proceso tras unos minutos. |
| **Chrome (Android)**      | ⚠️ Exp.     | -              | Funciona en gama alta. En gama media/baja puede causar sobrecalentamiento rápido.                          |

{% hint style="info" %}
**Nota sobre WebGL2:** Si el dispositivo no soporta WebGL2 (necesario para los Shaders 300 es), el SDK intentará hacer fallback a renderizado por CPU, lo cual incrementará drásticamente el uso del procesador.
{% endhint %}

***

## Rendimiento y Requisitos

Esta funcionalidad realiza segmentación de video _frame a frame_ en tiempo real utilizando redes neuronales.

#### Consumo Estimado

* **CPU:** Alto (\~2 a 4 Cores dedicados si falla la GPU).
* **RAM:** +500 MB (Modelos TFLite + Buffers de video).
* **GPU:** Moderado (Inferencia de texturas WebGL).

#### Hardware Recomendado (para 15 FPS estables)

* **CPU:** Intel Core i5 8va Gen / AMD Ryzen 5 o superior (arquitectura x64 recomendada).
* **Resolución de entrada:** Se recomienda encarecidamente **VGA (640x480)**.
  * _Advertencia:_ Usar resoluciones HD (720p/1080p) cuadruplica la cantidad de píxeles a procesar, lo que puede causar latencia alta y desincronización de audio/video en la mayoría de las laptops.

***

## Ejemplo Completo (HTML + ES Modules)

```html
<!DOCTYPE html>
<html lang="es">
<body>
    <video id="preview" autoplay playsinline muted style="width: 640px; height: 480px; background: #000;"></video>
    <button id="btn-start">Iniciar Cámara</button>

    <script type="module">
        import VirtualBackground from 'URL_DEL_SDK';

        const videoEl = document.getElementById('preview');
        const btn = document.getElementById('btn-start');
        
        // Instancia global
        const frameRate = VirtualBackground.getRecommendedSettings().frameRate;
        const vb = new VirtualBackground({ frameRate });

        btn.addEventListener('click', async () => {
            try {
                // 1. Obtener media
                const stream = await navigator.mediaDevices.getUserMedia({ 
                    video: { width: 640, height: 480 } 
                });

                // 2. Configurar
                vb.blur = 10; 

                // 3. Renderizar y reemplazar
                await vb.render(stream);
                vb.start();

                videoEl.srcObject = vb.stream;
                
            } catch (err) {
                console.error("Error:", err);
                alert("No se pudo iniciar el Virtual Background");
            }
        });
    </script>
</body>
</html>
```
