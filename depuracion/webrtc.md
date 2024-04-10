---
description: >-
  Descubre como realizar diagnósticos a tu equipo y/o red cuando las
  videollamadas no conectan en entornos corporativos.
---

# WebRTC

## Pruebas

Esta documentación tiene como objetivo que puedas identificar problemas relacionadas a un equipo o la red.

{% hint style="warning" %}
Recuerda que estas pruebas las debes realizar en el dispositivo que estás experimentando fallas. En caso que sean fallas de red, podrás utilizar cualquier dispositivo pero conectado a la misma red.
{% endhint %}

1. Accede a este [enlace](https://gauge.videsk.io/)
2. Haz clic en el botón verde `Start`
3. Espera a que finalice las pruebas con "Video Bandwidth" finalizado
4. En la parte superior busca el ícono de "bicho" al lado izquierdo del botón verde `Start`.
5. Luego haz clic en `Download report`
6. Envíanos un correo a [support@videsk.io](mailto:support@videsk.io), con el asunto "Pruebas de WebRTC" indicando el nombre de tu empresa, adjuntando el archivo `testrtc-...Z.log`

## Razones de problemas

Lee a continuación para conocer las razones por tus agentes no podrían conectarse de forma correcta.

### Perisféricos

{% hint style="info" %}
Es posible que las pruebas arrojen errores en el micrófono si este está apagado o silenciado desde tu equipo o teclado.
{% endhint %}

![Error al capturar audio](<../.gitbook/assets/image (60).png>)

Como requisitos mínimo deberás contar con micrófono para unirte a las videollamadas.

![Éxito al detectar cámara](<../.gitbook/assets/image (33).png>)

### Red

Para identificar problemas de red es necesario entender ciertos conceptos.&#x20;

![Pruebas de red](<../.gitbook/assets/image (51).png>)

`Network` consiste en pruebas propias de la red, siendo necesario disponer de al menos conexiones `UDP` o `TCP`. Si ambos tipos de protocolos de transmisión están restringidos no podrás conectar las videollamadas.

{% hint style="info" %}
No es requerido contar con compatibilidad IPv6.
{% endhint %}

![Pruebas de conexión](<../.gitbook/assets/image (59).png>)

Para el caso de `Connectivity` serán las pruebas de conexión, donde se probará la disponibilidad de conectar desde tu red con `Relay`, es decir, servidores de retransmisión, `Reflexive` para conexión P2P fuera de la red y finalmente conexión `Host` también P2P pero dentro de la red.

Dependiendo de las políticas de tu red y caso de uso, deberás contar con al menos 1 tipo de conexión disponible. Para el caso en que tus clientes o agentes estén fuera de tu red es necesario contar con al menos disponibilidad `Relay`.

Te sugerimos leer nuestra documentación de configuración de Firewalls.

{% content-ref url="../seguridad/firewall/" %}
[firewall](../seguridad/firewall/)
{% endcontent-ref %}

En el caso que tus clientes y agentes (ambos) estén dentro de la misma red deberás contar con conexión `Host`.

