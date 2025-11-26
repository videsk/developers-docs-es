# Quality

El SDK incluye un sistema de monitoreo de calidad que detecta y reporta problemas en tiempo real durante las videollamadas.

```javascript
webrtc.addEventListener('quality:issues', event => {
    const { ... } = event.detail;
});
```

## Quality Issues

El monitor de calidad detecta automáticamente los siguientes problemas:

| Issue Type             | Origin  | Severity           | Descripción                                       | Umbral Warning | Umbral Critical |
| ---------------------- | ------- | ------------------ | ------------------------------------------------- | -------------- | --------------- |
| `packetLoss`           | `local` | warning / critical | Pérdida de paquetes en la recepción (video/audio) | 1%             | 10%             |
| `latency`              | `local` | warning / critical | Latencia de red (Round-Trip Time)                 | 500ms          | 1500ms          |
| `jitter`               | `video` | warning / critical | Variación en llegada de paquetes de video         | 80ms           | 150ms           |
| `jitter`               | `audio` | warning / critical | Variación en llegada de paquetes de audio         | 35ms           | 60ms            |
| `bandwidth-limitation` | `local` | warning / critical | Video limitado por ancho de banda                 | 2s/5s          | 4s/5s           |
| `freezes`              | `video` | warning / critical | Congelamientos de video detectados                | 3 freezes/5s   | 10 freezes/5s   |

#### Interpretación de Severidades

* **Warning**: Degradación notable en la calidad, pero la comunicación sigue siendo funcional
* **Critical**: Problemas severos que dificultan o imposibilitan la comunicación efectiva

#### Origin Values

* `local`: Problema en la recepción local (tu downlink o el uplink del peer)
* `video`: Específico del stream de video
* `audio`: Específico del stream de audio

***

## Cómo usar

Puedes configurar los umbrales de calidad al inicializar el SDK:

```javascript
const latency = { warning: 500, critical: 1500 }; // ms
const thresholds = Object.assign(WebRTC.thresholds, { latency });
const webrtc = new WebRTC(component, parent, { thresholds });
```

## Eventos

### `quality:issues`

Se emite cuando se detecta un problema de calidad en **tu conexión local**.

| Propiedad   | Tipo   | Valores Posibles                                                     | Descripción                     |
| ----------- | ------ | -------------------------------------------------------------------- | ------------------------------- |
| `type`      | string | `packetLoss`, `latency`, `jitter`, `bandwidth-limitation`, `freezes` | Tipo de problema detectado      |
| `severity`  | string | `warning`, `critical`                                                | Nivel de severidad del problema |
| `origin`    | string | `local`, `video`, `audio`                                            | Origen o categoría del problema |
| `value`     | number | -                                                                    | Valor numérico de la métrica    |
| `timestamp` | number | -                                                                    | Timestamp Unix (ms) del evento  |

```javascript
webrtc.addEventListener('quality:issues', (event) => {
    const { type, severity, origin, value, timestamp } = event.detail;
    // Do something...
});
```

### `quality:recovered`

Se emite cuando un problema de calidad se ha recuperado en **tu conexión local**.

| Propiedad   | Tipo   | Valores Posibles                                                     | Descripción                      |
| ----------- | ------ | -------------------------------------------------------------------- | -------------------------------- |
| `type`      | string | `packetLoss`, `latency`, `jitter`, `bandwidth-limitation`, `freezes` | Tipo de problema que se recuperó |
| `origin`    | string | `local`, `video`, `audio`                                            | Origen o categoría del problema  |
| `timestamp` | number | -                                                                    | Timestamp Unix (ms) del evento   |

```javascript
webrtc.addEventListener('quality:recovered', (event) => {
    const { type, origin, timestamp } = event.detail;
    // Do something...
});
```

### `peer:quality`

Se emite cuando se detecta un problema de calidad en **la conexión del peer remoto**. Este evento te permite saber si el otro participante está experimentando problemas.

| Propiedad   | Tipo   | Valores Posibles                                                     | Descripción                      |
| ----------- | ------ | -------------------------------------------------------------------- | -------------------------------- |
| `status`    | string | `issues` o `recovered`                                               | Estado del problema detectado    |
| `peerId`    | string | -                                                                    | ID del peer con problemas        |
| `alias`     | string | -                                                                    | Alias del peer (si fue asignado) |
| `type`      | string | `packetLoss`, `latency`, `jitter`, `bandwidth-limitation`, `freezes` | Tipo de problema detectado       |
| `severity`  | string | `warning`, `critical`                                                | Nivel de severidad del problema  |
| `origin`    | string | `local`, `video`, `audio`                                            | Origen o categoría del problema  |
| `value`     | number | -                                                                    | Valor numérico de la métrica     |
| `timestamp` | number | -                                                                    | Timestamp Unix (ms) del evento   |

```javascript
webrtc.addEventListener('peer:quality', (event) => {
    const { status, peerId, alias, type, severity, origin, value, timestamp } = event.detail;
    // Do something...
});
```

***

## Ejemplos de uso

```javascript
webrtc.addEventListener('peer:quality', (event) => {
    const { alias, peerId, type, severity } = event.detail;
    const name = alias || peerId;
    
    showNotification({
        title: 'Problemas de Conexión',
        message: `${name} está experimentando problemas de ${type}`,
        type: severity
    });
});
```

***

## Cálculos

### Debounce

Para evitar alertas por problemas momentáneos, el sistema utiliza debounce:

* **Issue Detection**: Un problema debe persistir durante **2 intervalos consecutivos** (10 segundos) antes de emitir el evento (por defecto).
* **Recovery Detection**: El problema debe estar ausente durante **2 intervalos consecutivos** (10 segundos) antes de emitir recuperación (por defecto).

### Severidad

Si un problema activo cambia de severidad, el evento se emite inmediatamente:

```javascript
// t=0s: packet loss = 2% → warning emitido (después de debounce)
// t=10s: packet loss = 12% → critical emitido inmediatamente (escalamiento)
// t=15s: packet loss = 1.5% → warning emitido inmediatamente (degradación)
// t=25s: packet loss = 0.3% → recovered emitido (después de debounce)
```

### Ventana deslizante (Packet Loss)

El packet loss utiliza una ventana deslizante de **2 intervalos (10 segundos)** para calcular el promedio y evitar alertas por spikes momentáneos.

***

## Notas Técnicas

* Los eventos se emiten cada **5 segundos** (intervalo de stats)
* El sistema de debounce requiere **2 mediciones consecutivas** para confirmar issues y recuperaciones
* Los umbrales están calibrados según datos reales de producción con >14,000 peers
* Packet loss se calcula como promedio de ventana deslizante para mayor estabilidad
* Bandwidth limitation y freezes son deltas del intervalo actual (últimos 5s)
* Los eventos `peer:quality` se propagan automáticamente vía signaling entre peers

***

## Troubleshooting

#### Muchas alertas de warning

Considera ajustar los umbrales según tu caso de uso:

```javascript
const webrtc = new WebRTC(component, parent, {
    thresholds: {
        packetLoss: {
            warning: 0.03,  // Más tolerante
            critical: 0.15
        }
    }
});
```

#### Issues oscilando entre warning y critical

Si un issue oscila constantemente, considera ampliar el rango de umbrales en la configuración de `thresholds`.
