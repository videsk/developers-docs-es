---
description: >-
  A continuación te entregamos una guía para definir la calidad vs coste en base
  a tus necesidades.
---

# Tamaños y resolución

En tu cuenta puedes definir la parámetros que permitan flexibilizar entre calidad de grabación vs costo de almacenamiento, por lo que dependiendo de las necesidades de tu negocio podrás optar entre calidad alta, estándar o baja, como también configuración avanzada como bits y resolución.

## Valores por defecto

Con el respaldo de un set de pruebas que se muestran en esta tabla concluimos que la mejor configuración calidad/costo es:

* Resolución: `640x480`
* Bits video: `100,000`
* Bits audio: `25,000`

Esta configuración definida como **calidad estándar** entrega como valor de referencia archivos de `1.1 MB` por minuto o 60 segundos.

## Tabla calidad/tamaño

La tabla a continuación expone el listado de tamaños, bits, resolución y codecs utilizados para las grabaciones de prueba de 1 minuto o 60 segundos.

Las resoluciones que se utilizaron en estas pruebas son `(ancho x alto)` en pixeles:

* `1280 x 720`
* `1080 x 720`
* `640 x 480`
* `320 x 240`
* `160 x 120`

{% hint style="info" %}
Recuerda que los valores de tamaño (MB) pueden variar en base a la resolución de video, pero por sobre todo la tasa de bits por segundo para cada pista de video y audio.
{% endhint %}

{% hint style="info" %}
La cantidad de bits por segundo máximos es de `2,500,000` (video) y `128,000` (audio), mientras que lo mínimo es `100,000` (video) y `6,000` (audio).
{% endhint %}

<table><thead><tr><th width="171">Resolution (px)</th><th>Bits video (bps)</th><th>Bits audio (bps)</th><th>Codec</th><th>Size (MB)</th><th>Type</th></tr></thead><tbody><tr><td>1280x720</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>7.1</td><td>video + audio</td></tr><tr><td>1280x720</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>19.9</td><td>video + audio</td></tr><tr><td>1280x720</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp8"</td><td>2.9</td><td>video + audio</td></tr><tr><td>1280x720</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp8"</td><td>10</td><td>video + audio</td></tr><tr><td>1280x720</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>7.3</td><td>video + audio</td></tr><tr><td>1280x720</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>16.6</td><td>video + audio</td></tr><tr><td>1280x720</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp9"</td><td>10</td><td>video + audio</td></tr><tr><td>1280x720</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp9"</td><td>0.9792</td><td>video + audio</td></tr><tr><td>1080x720</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>16.2</td><td>video + audio</td></tr><tr><td>1080x720</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>7.4</td><td>video + audio</td></tr><tr><td>1080x720</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp9"</td><td>9.8</td><td>video + audio</td></tr><tr><td>1080x720</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp9"</td><td>0.9813</td><td>video + audio</td></tr><tr><td>1080x720</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>19.9</td><td>video + audio</td></tr><tr><td>1080x720</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>7.1</td><td>video + audio</td></tr><tr><td>1080x720</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp8"</td><td>10</td><td>video + audio</td></tr><tr><td>1080x720</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp8"</td><td>2.6</td><td>video + audio</td></tr><tr><td>640x480</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>14.4</td><td>video + audio</td></tr><tr><td>640x480</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>6.6</td><td>video + audio</td></tr><tr><td>640x480</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp9"</td><td>8.2</td><td>video + audio</td></tr><tr><td>640x480</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp9"</td><td>0.9313</td><td>video + audio</td></tr><tr><td>640x480</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>19.9</td><td>video + audio</td></tr><tr><td>640x480</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>7</td><td>video + audio</td></tr><tr><td>640x480</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp8"</td><td>10</td><td>video + audio</td></tr><tr><td>640x480</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp8"</td><td>1.3</td><td>video + audio</td></tr><tr><td>320x240</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>12.9</td><td>video + audio</td></tr><tr><td>320x240</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>5.6</td><td>video + audio</td></tr><tr><td>320x240</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp9"</td><td>7</td><td>video + audio</td></tr><tr><td>320x240</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp9"</td><td>0.8735</td><td>video + audio</td></tr><tr><td>320x240</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>19.7</td><td>video + audio</td></tr><tr><td>320x240</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>7</td><td>video + audio</td></tr><tr><td>320x240</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp8"</td><td>10</td><td>video + audio</td></tr><tr><td>320x240</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp8"</td><td>0.8167</td><td>video + audio</td></tr><tr><td>160x120</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>12.9</td><td>video + audio</td></tr><tr><td>160x120</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp9"</td><td>5.6</td><td>video + audio</td></tr><tr><td>160x120</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp9"</td><td>7.1</td><td>video + audio</td></tr><tr><td>160x120</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp9"</td><td>0.636</td><td>video + audio</td></tr><tr><td>160x120</td><td>2,500,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>14.3</td><td>video + audio</td></tr><tr><td>160x120</td><td>800,000</td><td>128,000</td><td>video/webm;codecs="vp8"</td><td>7</td><td>video + audio</td></tr><tr><td>160x120</td><td>1,250,000</td><td>64,000</td><td>video/webm;codecs="vp8"</td><td>9.9</td><td>video + audio</td></tr><tr><td>160x120</td><td>100,000</td><td>6,000</td><td>video/webm;codecs="vp8"</td><td>0.8213</td><td>video + audio</td></tr><tr><td>160x120</td><td>100,000</td><td>25,000</td><td>video/webm;codecs="vp9"</td><td>0.9992</td><td>video + audio</td></tr><tr><td><mark style="background-color:blue;">640x480</mark></td><td><mark style="background-color:blue;">100,000</mark></td><td><mark style="background-color:blue;">25,000</mark></td><td><mark style="background-color:blue;">video/webm;codecs="vp9"</mark></td><td><mark style="background-color:blue;">1.1</mark></td><td><mark style="background-color:blue;">video + audio</mark></td></tr></tbody></table>

{% hint style="danger" %}
La información en este documento es de propiedad de Videsk. Sin la autorización explícita para uso, copia o distribución en sitios o documentos externos a Videsk conlleva una violación de derechos de autor punible legalmente.
{% endhint %}

## Almacenamiento mensual

Para calcular el tamaño aproximado mensual de las grabaciones debes contar con un valor referencial de:

* Promedio de duración de las llamadas en minutos
* Cantidad de llamadas por hora, día o mes
* Calidad/Resolución

En el siguiente cálculo de ejemplo consideramos duración promedio de **10 minutos**, **1000 llamadas diarias** y una calidad de grabación estándar `640x480 (100,000 bps + 25,000bps)` equivalente a `1.1 MB` por minuto, aproximadamente.

$$
tamaño (MB) = (minutos * participantes* 1.1 MB) * llamadas*30 días
$$

Considerando videollamadas de **2 participantes**, solo agente y cliente (sin pantalla compartida), el tamaño mensual sería equivalente a `660 GB`.

## Calculadora

Puedes usar esta calculadora diseñada que **entrega un aproximado** en gigabytes y tarifa mensual.

{% hint style="warning" %}
Este es un estimador y no corresponde a una tarifa fija o exacta.
{% endhint %}

{% embed url="https://t.videsk.io/" %}
