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

| Resolution (px)                                     | Bits video (bps)                                    | Bits audio (bps)                                   | Codec                                                               | Size (MB)                                       | Type                                                      |
| --------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------- | --------------------------------------------------------- |
| 1280x720                                            | 800,000                                             | 128,000                                            | video/webm;codecs="vp8"                                             | 7.1                                             | video + audio                                             |
| 1280x720                                            | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp8"                                             | 19.9                                            | video + audio                                             |
| 1280x720                                            | 100,000                                             | 6,000                                              | video/webm;codecs="vp8"                                             | 2.9                                             | video + audio                                             |
| 1280x720                                            | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp8"                                             | 10                                              | video + audio                                             |
| 1280x720                                            | 800,000                                             | 128,000                                            | video/webm;codecs="vp9"                                             | 7.3                                             | video + audio                                             |
| 1280x720                                            | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp9"                                             | 16.6                                            | video + audio                                             |
| 1280x720                                            | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp9"                                             | 10                                              | video + audio                                             |
| 1280x720                                            | 100,000                                             | 6,000                                              | video/webm;codecs="vp9"                                             | 0.9792                                          | video + audio                                             |
| 1080x720                                            | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp9"                                             | 16.2                                            | video + audio                                             |
| 1080x720                                            | 800,000                                             | 128,000                                            | video/webm;codecs="vp9"                                             | 7.4                                             | video + audio                                             |
| 1080x720                                            | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp9"                                             | 9.8                                             | video + audio                                             |
| 1080x720                                            | 100,000                                             | 6,000                                              | video/webm;codecs="vp9"                                             | 0.9813                                          | video + audio                                             |
| 1080x720                                            | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp8"                                             | 19.9                                            | video + audio                                             |
| 1080x720                                            | 800,000                                             | 128,000                                            | video/webm;codecs="vp8"                                             | 7.1                                             | video + audio                                             |
| 1080x720                                            | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp8"                                             | 10                                              | video + audio                                             |
| 1080x720                                            | 100,000                                             | 6,000                                              | video/webm;codecs="vp8"                                             | 2.6                                             | video + audio                                             |
| 640x480                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp9"                                             | 14.4                                            | video + audio                                             |
| 640x480                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp9"                                             | 6.6                                             | video + audio                                             |
| 640x480                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp9"                                             | 8.2                                             | video + audio                                             |
| 640x480                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp9"                                             | 0.9313                                          | video + audio                                             |
| 640x480                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp8"                                             | 19.9                                            | video + audio                                             |
| 640x480                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp8"                                             | 7                                               | video + audio                                             |
| 640x480                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp8"                                             | 10                                              | video + audio                                             |
| 640x480                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp8"                                             | 1.3                                             | video + audio                                             |
| 320x240                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp9"                                             | 12.9                                            | video + audio                                             |
| 320x240                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp9"                                             | 5.6                                             | video + audio                                             |
| 320x240                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp9"                                             | 7                                               | video + audio                                             |
| 320x240                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp9"                                             | 0.8735                                          | video + audio                                             |
| 320x240                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp8"                                             | 19.7                                            | video + audio                                             |
| 320x240                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp8"                                             | 7                                               | video + audio                                             |
| 320x240                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp8"                                             | 10                                              | video + audio                                             |
| 320x240                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp8"                                             | 0.8167                                          | video + audio                                             |
| 160x120                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp9"                                             | 12.9                                            | video + audio                                             |
| 160x120                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp9"                                             | 5.6                                             | video + audio                                             |
| 160x120                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp9"                                             | 7.1                                             | video + audio                                             |
| 160x120                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp9"                                             | 0.636                                           | video + audio                                             |
| 160x120                                             | 2,500,000                                           | 128,000                                            | video/webm;codecs="vp8"                                             | 14.3                                            | video + audio                                             |
| 160x120                                             | 800,000                                             | 128,000                                            | video/webm;codecs="vp8"                                             | 7                                               | video + audio                                             |
| 160x120                                             | 1,250,000                                           | 64,000                                             | video/webm;codecs="vp8"                                             | 9.9                                             | video + audio                                             |
| 160x120                                             | 100,000                                             | 6,000                                              | video/webm;codecs="vp8"                                             | 0.8213                                          | video + audio                                             |
| 160x120                                             | 100,000                                             | 25,000                                             | video/webm;codecs="vp9"                                             | 0.9992                                          | video + audio                                             |
| <mark style="background-color:blue;">640x480</mark> | <mark style="background-color:blue;">100,000</mark> | <mark style="background-color:blue;">25,000</mark> | <mark style="background-color:blue;">video/webm;codecs="vp9"</mark> | <mark style="background-color:blue;">1.1</mark> | <mark style="background-color:blue;">video + audio</mark> |

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
