---
description: >-
  Podrás encontrar conceptos relacionados a tecnología, redes y conexiones que
  utilizamos.
---

# ☝ Conceptos

## WebRTC

WebRTC es una tecnología de navegador que permite realizar conexiones seguras de forma nativa entre pares mediante protocolos DTLS-SRTP. **Esto permite realizar conexiones seguras sin necesidad de descargar extensiones o instaladores en los equipos de los usuarios.**

Si bien se puede utilizar con varios propósitos, en Videsk lo utilizamos como medio de conexión de alta velocidad para gran parte de nuestras características.

## P2P (Peer-to-Peer)

P2P es un modelo de conexión entre pares capas de realizar conexiones entre redes de forma directa, sin intermediarios como servidores o proxies. Esta tecnología viene siendo utilizada hace varios años atrás, más conocido entornos de descargas de archivos como Torrent.

El gran beneficio de este tipo de conexión es la alta velocidad de transferencia de datos y escalable, aunque también presenta restricciones frente a redes restringidas por WAFs, debido a que requiere un tipo de NAT abierto para auto seleccionar IP público/local y puertos de los usuarios.

Existen ciertos casos donde no es posible realizar las conexiones P2P, por lo que se recurre a un componente que se encarga de distribuir los datos, un servidor de relé.

## Servidor de relé

Un servidor de relé o TURN permite realizar conexiones en entornos donde la red donde se transita es restrictiva como NAT simétricos que restringen IP y/o puertos.

También se utilizan en ciertos casos donde la conexión no es estable y necesita de un punto de acceso único para transportar datos de video y audio.&#x20;

Este tipo de conexiones mediante servidores de relé agregan cierto nivel de latencia ya que requiere llegar a nuestros servidores los cuales participan como medio de relé entre los participantes de las videollamadas.
