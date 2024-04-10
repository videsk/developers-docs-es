---
description: >-
  Encontrarás información relacionada con la configuración necesaria si cuentas
  con firewall en la red donde operará Videsk.
---

# ⛔ Firewall

{% hint style="danger" %}
Por defecto, utilizamos el puerto 443 para todas las conexiones sobre TCP y UDP.
{% endhint %}

Esta información te ayudará a configurar correctamente lo necesario para que Videsk logre operar en un entorno protegido por WAFs de tu negocio.

Te reocmendamos opcionalmente leer sobre ciertos conceptos, para ello te recomendamos dirigirte a la siguiente sección.

{% content-ref url="../../conceptos.md" %}
[conceptos.md](../../conceptos.md)
{% endcontent-ref %}

{% content-ref url="tipos-de-nat.md" %}
[tipos-de-nat.md](tipos-de-nat.md)
{% endcontent-ref %}

***

## Servicios de Videsk

Videsk se desploza en tres grandes componentes:

1. Infraestructura lógica
2. Infraestructura de medios (red TURN)
3. Infraestructura de componentes UI

Los componentes lógicos y componentes UI operan sobre puertos 443 sobre protocolo TCP, como cualquier recurso web. Mientras que en el caso de nuestra infraestructura de medios, mas conocida como red TURN es un poco más complejo, pero principalmente operan sobre puerto 443.

Particularmente, en este último caso disponemos de la siguiente nomenclatura de FQDN para nuestra red TURN:

`{country}-{location}{number}.turn.videsk.io`

Ejemplo: `us-west1.turn.videsk.io`

Esto permite identificar qué país y ubicación se encuentra el servidor. Por lo tanto, puedes realizar un listado blanco por wildcard o bien por cada servidor FQDN o IP. Esto debido, a que la selección del servidor a utilizar dependerá de la ubicación física del usuario (cliente y agente)  con el objetivo de reducir latencia.

{% hint style="info" %}
En caso de una conexión internacional, ambos cliente y ejecutivo se encuentren en continentes diferentes, la comunicación se realizará a través de nuestra red.
{% endhint %}

***

## Ambientes de red

Dependiendo del caso a uso en tu negocio se debería configurar en tu firewall ciertas reglas para asegurar la operación de la plataforma.

{% hint style="success" %}
**Solo es necesario aplicar las siguientes reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en el puerto 443 `DTLS` (UDP) y `TLS` (TCP), y solo como respaldo 80 (TCP).
{% endhint %}

| Caso                 | Escenario                                           | Solución                                                         |
| -------------------- | --------------------------------------------------- | ---------------------------------------------------------------- |
| Home office + VPN    | Firewall con bloqueo por dominios                   | Añadir `*.videsk.io` a la lista blanca                           |
| Sucursales o tiendas | Firewall permite solo tráfico 443 sobre TCP         | Se sugiere permitir protocolo UDP para `*.turn.videsk.io`        |
| Oficina              | Segmentos de red con NAT simétrico                  | Asegurar tráfico UDP/TCP sobre puerto 443                        |
| MPLS                 | Firewall con análisis de tráfico DPI, alta latencia | Desactivar DPI para tráfico `*.turn.videsk.io` sobre 443 UDP/TCP |

{% hint style="info" %}
Si posees un firewall de capa 3, contáctanos a [support@videsk.io](mailto:support@videsk.io), con el asunto: "**IPs turn servers list"**, para obtener el listado de IP de nuestros servidores. _Verificaremos tu identidad asociada a la organización._
{% endhint %}

{% hint style="warning" %}
Como mínimo se debe permitir tráfico por protocolo `TCP`.



_No se recomienda utilizar únicamente protocolo TCP, debido a la naturaleza del protocolo y la alta latencia que podría provocar en la comunicación._
{% endhint %}

***

## Dominios

Videsk solo utiliza un único dominio base: `videsk.io`, esto para toda la operación crítica.

La forma más sencilla de permitir todo el tráfico de Videsk sobre el puerto 443 es listando de manera wildcard:

`*.videsk.io`

Al añadir nuestro dominio wildcard, aseguras el funcionamiento de toda nuestra infraestructura en tu red. Existen otras opciones, en caso que no cuentes con un firewall con esas capacidades.

{% hint style="warning" %}
**Solo es necesario aplicar las reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en el puerto 443 DTLS (UDP) y TLS (TCP), y solo como respaldo 80 (TCP).
{% endhint %}

### Infraestructura TURN

Deberás añadir nuestro dominio wilcard de servidores TURN a una lista blanca:

```bash
*.turn.videsk.io
```

{% hint style="danger" %}
Sugerimos no utilizar direcciones IP, ya que nuestra infraestructura varía dependiendo de la posición geográfica, por lo que podemos incrementar el número de servidores o disminuirlos según la demanda, **no recomendamos utilizar las IPs**.
{% endhint %}

### Infraestructura lógica y UI

Para las demás aplicaciones como nuestra Rest API, dashboard, consola, etc. se encuentran como subdominios de primer nivel **`*.videsk.io`** . Estos son:

```bash
app.videsk.io
console.videsk.io
api.videsk.io
assets.videsk.io
cdn.videsk.io
agamotto.videsk.io
exchange.videsk.io
rt.videsk.io
```

Adicionalmente y opcionalmente a los dominios anteriores, <mark style="background-color:green;">**sugerimos**</mark> añadir los siguientes dominios wildcard de servicios de terceros, los cuales nos permiten entregar un mejor soporte.

```
cloudflareinsights.com
*.pendo.io
*.lr-ingest.io
```

***

## Puertos

Utilizamos puerto estándar `443`, tanto para comunicación con nuestra API como nuestros servidores TURN.

Solo para el caso de nuestra **red TURN** utilizamos conexiones cifradas mediante puerto `443` sobre protocolo `UDP` (DTLS) y `TCP` (TLS), el cual se adaptará automáticamente dependiendo de la disponibilidad `UDP` de la red. Mientras que el puerto `80` sobre `TCP` como medio de respaldo en caso que no sea posible usar cifrado en la conexión.

Evita capturar paquetes de forma activa para analisis de tráfico DPI (Deep Packet Inspection), ya que son conexiones cifradas y provocarás alta latencia en la comunicación.

***

## Subprocesadores

{% hint style="info" %}
**Es importante para entregar el mejor servicio, que nuestros sistemas de monitoreo no sean bloqueados por extensiones del navegador, equipo o redes. De lo contrario dificulta a nuestro equipo identificar y resolver problemas de forma proactiva.**
{% endhint %}

### Cloudflare

Nuestros servicios se encuentran detrás nuestro proxy WAF Cloudflare, la lista de servidores se encuentran en el siguiente enlace: [https://www.cloudflare.com/ips/](https://www.cloudflare.com/ips/)

```
cloudflareinsights.com
```

### Sentry

La lista de IP de nuestro monitor de errores Sentry se encuentra en el siguiente enlace: [https://docs.sentry.io/product/security/ip-ranges/](https://docs.sentry.io/product/security/ip-ranges/)

### LogRocket

Utilizamos un monitor de sesiones llamado LogRocket, actualmente no es posible listar por IP, por lo que sugerimos utilizar listas blancas por dominio base.

```
*.lr-ingest.io
```
