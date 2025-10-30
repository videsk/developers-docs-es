# Stats

A continuación se detalla el listado de estadísticas de la conexión en curso. Podrás obtener las estadísticas mediante el evento [stats](eventos.md#stats).

En total, las estadísticas disponibles son 64 puntos de medición divididos en instantáneos y acumulativos.

Debes considerar que estas estadísticas corresponden a cada conexión con cada participante. Por lo tanto, recibirás bajo el mismo evento múltiples estadísticas de cada participante.

{% hint style="info" %}
Las estadísticas estarán disponibles cada 5 segundos.
{% endhint %}

## Tipos de estadísticas

### Identificación de Conexión

| Nombre           | Tipo     | Medición    | Enums                                            | Descripción                                                                                                            |
| ---------------- | -------- | ----------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| `peerId`         | `string` | Instantáneo | -                                                | Identificador único del peer remoto en la sesión. Útil para correlacionar métricas cuando hay múltiples participantes. |
| `ip`             | `string` | Instantáneo | -                                                | Dirección IP del endpoint de conexión (puede ser del relay TURN si connectionType es "relay").                         |
| `port`           | `number` | Instantáneo | -                                                | Puerto del endpoint de conexión.                                                                                       |
| `protocol`       | `string` | Instantáneo | `udp`, `tcp`                                     | Protocolo de transporte. UDP es lo más común y eficiente, TCP indica problemas de firewall.                            |
| `networkType`    | `string` | Instantáneo | `ethernet`, `wifi`, `cellular`, `vpn`, `unknown` | Tipo de interfaz de red del cliente.                                                                                   |
| `connectionType` | `string` | Instantáneo | `host`, `srflx`, `relay`                         | Modo de conexión ICE. host=P2P directo (ideal), srflx=través de NAT, relay=servidor TURN (mayor latencia).             |
| `timestamp`      | `number` | Instantáneo | -                                                | Momento de captura de métricas (epoch en milisegundos).                                                                |
| `ua`             | `string` | Instantáneo | -                                                | User-Agent del navegador. Útil para correlacionar problemas específicos de browser/versión.                            |

***

### Audio - Recepción (Inbound)

| Nombre                  | Tipo     | Medición    | Enums                                          | Descripción                                                                                                                        |
| ----------------------- | -------- | ----------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `audioJitter`           | `number` | Instantáneo | -                                              | Variación en segundos del tiempo de llegada de paquetes. Valores normales: 0-0.03s. >0.05s indica red inestable.                   |
| `audioPacketsLost`      | `number` | Acumulativo | -                                              | Total de paquetes perdidos desde inicio. Packet loss rate = lost/(lost+received). <1% excelente, 1-3% aceptable, >5% problemático. |
| `audioPacketsReceived`  | `number` | Acumulativo | -                                              | Total de paquetes de audio recibidos exitosamente desde inicio de la conexión.                                                     |
| `audioInboundLevel`     | `number` | Instantáneo | -                                              | Nivel de audio entrante (0-1). Útil para detectar silencio o problemas de captura del peer remoto.                                 |
| `audioBytesReceived`    | `number` | Acumulativo | -                                              | Total de bytes de audio recibidos. Para calcular bitrate actual: diferencial entre snapshots dividido por tiempo transcurrido.     |
| `audioPacketsDiscarded` | `number` | Acumulativo | -                                              | Paquetes que llegaron pero se descartaron (buffer overflow, jitter excesivo). Idealmente 0.                                        |
| `audioInboundMimeType`  | `string` | Instantáneo | `audio/opus`, `audio/PCMU`, `audio/PCMA`, etc. | Códec de audio entrante. Opus es el estándar moderno (adaptativo, eficiente).                                                      |

***

### Audio - Transmisión (Outbound)

| Nombre                          | Tipo      | Medición    | Enums                                          | Descripción                                                                                                                      |
| ------------------------------- | --------- | ----------- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `audioLevel`                    | `number`  | Instantáneo | -                                              | Nivel de audio saliente (0-1). 0=silencio, útil para Voice Activity Detection (VAD).                                             |
| `audioSampleDuration`           | `number`  | Instantáneo | -                                              | Duración en segundos de cada muestra de audio. Típicamente 0.02 (20ms).                                                          |
| `audioBytesSent`                | `number`  | Acumulativo | -                                              | Total de bytes de audio enviados desde inicio de la conexión.                                                                    |
| `audioPacketsSent`              | `number`  | Acumulativo | -                                              | Total de paquetes de audio enviados desde inicio.                                                                                |
| `audioActive`                   | `boolean` | Instantáneo | `true`, `false`                                | Indica si el track de audio está activo (no muted/stopped).                                                                      |
| `audioMimeType`                 | `string`  | Instantáneo | `audio/opus`, `audio/PCMU`, `audio/PCMA`, etc. | Códec configurado para envío. Debería coincidir con audioInboundMimeType del peer.                                               |
| `audioRetransmittedBytesSent`   | `number`  | Acumulativo | -                                              | Bytes retransmitidos por NACK. Valores altos indican pérdida de paquetes en el peer receptor.                                    |
| `audioRetransmittedPacketsSent` | `number`  | Acumulativo | -                                              | Paquetes retransmitidos por NACK. Alto indica que el peer tiene packet loss.                                                     |
| `audioTotalPacketSendDelay`     | `number`  | Acumulativo | -                                              | Tiempo total en segundos que los paquetes esperaron en queue antes de enviarse. Valores altos=CPU saturada o bandwidth limitado. |
| `audioNack`                     | `number`  | Acumulativo | -                                              | Negative Acknowledgments recibidos (peer pidiendo retransmisión). Alto=peer tiene packet loss.                                   |
| `audioBitrate`                  | `number`  | Instantáneo | -                                              | Bitrate configurado en bps. Opus típicamente usa 32000 bps (32kbps) para voz.                                                    |

***

### Video - Recepción (Inbound)

| Nombre                 | Tipo     | Medición    | Enums                                               | Descripción                                                                                                                          |
| ---------------------- | -------- | ----------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `videoJitter`          | `number` | Instantáneo | -                                                   | Variación en segundos del tiempo de llegada de paquetes de video. >0.05s causa frames irregulares y stuttering.                      |
| `videoPacketsLost`     | `number` | Acumulativo | -                                                   | Total de paquetes de video perdidos. Packet loss afecta más a video que audio (no hay interpolación automática).                     |
| `videoDecoder`         | `string` | Instantáneo | -                                                   | Decodificador usado por el navegador: libvpx (VP8/VP9), FFmpeg, h264, etc.                                                           |
| `videoIPliLoss`        | `number` | Acumulativo | -                                                   | Intra Picture Loss Indicator. Frames I (keyframes) perdidos. Crítico porque sin ellos el video se congela hasta el próximo keyframe. |
| `videoFramesDropped`   | `number` | Acumulativo | -                                                   | Frames que llegaron pero se descartaron (decoder saturado, late arrival). Alto=CPU limitada o jitter excesivo.                       |
| `videoFreezes`         | `number` | Acumulativo | -                                                   | Cantidad de congelamientos de video detectados. Indica problemas graves de red o CPU.                                                |
| `videoFreezeDuration`  | `number` | Acumulativo | -                                                   | Duración total en segundos de todos los congelamientos.                                                                              |
| `videoFrames`          | `number` | Acumulativo | -                                                   | Total de frames decodificados exitosamente desde inicio de la conexión.                                                              |
| `videoPacketsReceived` | `number` | Acumulativo | -                                                   | Total de paquetes de video recibidos exitosamente.                                                                                   |
| `videoBytesReceived`   | `number` | Acumulativo | -                                                   | Total de bytes de video recibidos. Indica bandwidth real consumido por video entrante.                                               |
| `videoInboundMimeType` | `string` | Instantáneo | `video/VP8`, `video/VP9`, `video/H264`, `video/AV1` | Códec de video recibido.                                                                                                             |

***

### Video - Transmisión (Outbound)

| Nombre                          | Tipo      | Medición    | Enums                                               | Descripción                                                                                                  |
| ------------------------------- | --------- | ----------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `videoMimeType`                 | `string`  | Instantáneo | `video/VP8`, `video/VP9`, `video/H264`, `video/AV1` | Códec de video configurado para envío. Debería coincidir con videoInboundMimeType del peer.                  |
| `videoBytesSent`                | `number`  | Acumulativo | -                                                   | Total de bytes de video enviados. Comparar con videoBytesReceived del peer para detectar packet loss.        |
| `videoPacketsSent`              | `number`  | Acumulativo | -                                                   | Total de paquetes de video enviados desde inicio.                                                            |
| `videoActive`                   | `boolean` | Instantáneo | `true`, `false`                                     | Track de video activo (no stopped ni sin frames).                                                            |
| `videoNack`                     | `number`  | Acumulativo | -                                                   | NACKs recibidos del peer. Alto=peer tiene packet loss en video.                                              |
| `videoOPliLoss`                 | `number`  | Acumulativo | -                                                   | Outbound Picture Loss Indicator. Similar a IPli pero para salida (frames I que no llegaron al peer).         |
| `videoLimitations`              | `string`  | Instantáneo | `none`, `bandwidth`, `cpu`, `other`                 | Indica qué está limitando la calidad del video enviado actualmente.                                          |
| `videoLimitationsBandwidth`     | `number`  | Acumulativo | -                                                   | Tiempo en segundos que la conexión ha estado limitada por bandwidth.                                         |
| `videoLimitationsCpu`           | `number`  | Acumulativo | -                                                   | Tiempo en segundos que la conexión ha estado limitada por CPU (encoder saturado).                            |
| `videoLimitationsNone`          | `number`  | Acumulativo | -                                                   | Tiempo en segundos sin limitaciones (operación óptima).                                                      |
| `videoLimitationsOther`         | `number`  | Acumulativo | -                                                   | Tiempo en segundos limitado por otras causas.                                                                |
| `videoRetransmittedBytesSent`   | `number`  | Acumulativo | -                                                   | Bytes de video retransmitidos por NACK del peer.                                                             |
| `videoRetransmittedPacketsSent` | `number`  | Acumulativo | -                                                   | Paquetes de video retransmitidos por NACK del peer.                                                          |
| `videoTotalPacketSendDelay`     | `number`  | Acumulativo | -                                                   | Delay acumulado en segundos de paquetes en queue antes de envío. >0.1s acumulado en pocos segundos=problema. |
| `videoBitrate`                  | `number`  | Instantáneo | -                                                   | Bitrate configurado/target en bps. 1700000 (1.7Mbps) es razonable para 720p/30fps.                           |

***

### Métricas de Transporte

| Nombre                     | Tipo     | Medición    | Enums                                                                                 | Descripción                                                                                                                             |
| -------------------------- | -------- | ----------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `availableOutgoingBitrate` | `number` | Instantáneo | -                                                                                     | Estimación dinámica del bandwidth disponible en bps. WebRTC ajusta calidad basándose en esto. Fluctuaciones grandes=red inestable.      |
| `bytesDiscardedOnSend`     | `number` | Acumulativo | -                                                                                     | Bytes descartados antes de enviar (típicamente por congestión). Idealmente 0.                                                           |
| `packetsDiscarded`         | `number` | Acumulativo | -                                                                                     | Paquetes descartados antes de enviar. Idealmente 0.                                                                                     |
| `bytesReceived`            | `number` | Acumulativo | -                                                                                     | Total de bytes recibidos combinado (audio + video + overhead SRTP/STUN).                                                                |
| `bytesSent`                | `number` | Acumulativo | -                                                                                     | Total de bytes enviados combinado (audio + video + overhead SRTP/STUN).                                                                 |
| `currentRoundTripTime`     | `number` | Instantáneo | -                                                                                     | RTT actual en segundos (ping). <0.1s excelente, 0.1-0.3s aceptable, >0.3s lag notable.                                                  |
| `lastPacketReceived`       | `number` | Instantáneo | -                                                                                     | Timestamp epoch en ms del último paquete recibido. Útil para detectar conexión muerta.                                                  |
| `lastPacketSent`           | `number` | Instantáneo | -                                                                                     | Timestamp epoch en ms del último paquete enviado.                                                                                       |
| `packetsSent`              | `number` | Acumulativo | -                                                                                     | Total de paquetes RTP/RTCP enviados.                                                                                                    |
| `packetsReceived`          | `number` | Acumulativo | -                                                                                     | Total de paquetes RTP/RTCP recibidos.                                                                                                   |
| `totalRoundTripTime`       | `number` | Acumulativo | -                                                                                     | Suma de todas las mediciones de RTT en segundos. Dividir por cantidad de mediciones para obtener RTT promedio.                          |
| `state`                    | `string` | Instantáneo | `checking`, `connected`, `completed`, `failed`, `disconnected`, `closed`, `succeeded` | Estado ICE de la conexión. checking=negociando, connected/completed=funcional, failed/disconnected=sin conectividad, closed=finalizada. |

***

## Valores de referencias

1. **Packet Loss <3%**: Tanto audio como video
2. **Jitter <30ms (0.03s)**: Especialmente en audio
3. **RTT <150ms (0.15s)**: Para videoconferencia interactiva
4. **videoLimitations = "none"**: Si no, identificar cuello de botella
5. **connectionType = "host"**: Ideal, "relay" como fallback

## Ejemplo

```json
{
    "peerId": "2ff7ac7e-38c5-4c51-b4b6-16889bd645b0",
    "ip": "XX.XXX.XX.XX",
    "port": 56749,
    "protocol": "udp",
    "networkType": "ethernet",
    "connectionType": "relay",
    "timestamp": 1761845560417,
    "ua": "Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko) Chrome/141.0.0.0 Safari/537.36",
    "audioJitter": 0.006,
    "audioPacketsLost": 0,
    "audioPacketsReceived": 211,
    "audioInboundLevel": 0.043733024079103976,
    "audioBytesReceived": 16610,
    "audioPacketsDiscarded": 0,
    "audioInboundMimeType": "audio/opus",
    "audioLevel": 0,
    "audioSampleDuration": 0,
    "audioBytesSent": 16403,
    "audioPacketsSent": 209,
    "audioActive": true,
    "audioMimeType": "audio/opus",
    "audioRetransmittedBytesSent": 0,
    "audioRetransmittedPacketsSent": 0,
    "audioTotalPacketSendDelay": 0.000607,
    "audioNack": 0,
    "videoJitter": 0.008,
    "audioBitrate": 32000,
    "videoPacketsLost": 0,
    "videoDecoder": "libvpx",
    "videoIPliLoss": 0,
    "videoFramesDropped": 0,
    "videoFreezes": 0,
    "videoFreezeDuration": 0,
    "videoFrames": 30,
    "videoPacketsReceived": 737,
    "videoBytesReceived": 734399,
    "videoInboundMimeType": "video/VP8",
    "videoMimeType": "video/VP8",
    "videoBytesSent": 646396,
    "videoPacketsSent": 660,
    "videoActive": true,
    "videoNack": 0,
    "videoOPliLoss": 0,
    "videoLimitations": "none",
    "videoLimitationsBandwidth": "",
    "videoLimitationsCpu": "",
    "videoLimitationsNone": 4.905,
    "videoLimitationsOther": "",
    "videoRetransmittedBytesSent": 0,
    "videoRetransmittedPacketsSent": 0,
    "videoTotalPacketSendDelay": 0.225802,
    "videoBitrate": 1700000,
    "availableOutgoingBitrate": 3412307,
    "bytesDiscardedOnSend": 0,
    "packetsDiscarded": 0,
    "bytesReceived": 792115,
    "bytesSent": 672476,
    "currentRoundTripTime": 0.035,
    "lastPacketReceived": 1761845560415,
    "lastPacketSent": 1761845560400,
    "packetsSent": 901,
    "packetsReceived": 1040,
    "totalRoundTripTime": 0.141,
    "state": "succeeded"
}
```

