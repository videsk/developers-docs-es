---
description: >-
  Encontrarás información relacionada con la configuración necesaria si cuentas
  con firewall en la red donde operará Videsk.
---

# ⛔ Firewall

{% hint style="warning" %}
**Solo es necesario aplicar las siguientes reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en los puertos 80 (UDP/TCP) y 443 (TCP/TLS). En caso que las conexiones UDP estén bloqueadas nuestro sistema intentará automáticamente por TCP.
{% endhint %}

Esta información te ayudará a configurar correctamente lo necesario para que Videsk logre operar en un entorno protegido por WAFs de tu negocio.

Primero es necesario que conozcas ciertos conceptos, para ello te recomendamos dirigirte a la siguiente sección.

{% content-ref url="../conceptos.md" %}
[conceptos.md](../conceptos.md)
{% endcontent-ref %}

## 1. Tipo de NAT

Lo primero que deberás determinar es el tipo de NAT que posees en tu negocio. Existen varios tipos de configuraciones, las cuales necesitarán ciertos ajustes para permitir traficar videollamadas y otras funciones:

| Tipo NAT                                           | Descripción                                                                                                                                                                                                                                                                                                                                                                        | Requiere ajustes |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Cono completo (Full-Cone)                          | NAT mapeará la dirección IP y puerto interno a una dirección y puerto público diferentes. Una vez establecido, cualquier host externo puede comunicarse con el host de la red privada enviando los paquetes a una dirección IP y puerto externo que haya sido mapeado. Esta implementación NAT es la menos segura, puesto que una atacante puede adivinar qué puerto está abierto. | ❌                |
| Cono restringido (Restricted Cone)                 | En este caso de la conexión restringida, la IP y puerto externos de NAT son abiertos cuando el host de la red privada quiere comunicarse con una dirección IP específica fuera de su red. La NAT bloqueará todo tráfico que no venga de esa dirección IP específica.                                                                                                               | ✅/❌              |
| Cono restringido de puertos (Port-Restricted Cone) | En una conexión restringida por puerto NAT bloqueará todo el tráfico a menos que el host de la red privada haya enviado previamente tráfico a una IP y puerto específico, entonces solo en ese caso esa IP/puerto tendrán acceso a la red privada.                                                                                                                                 | ✅                |
| Simétrico (Symmetric)                              | En este caso la traducción de dirección IP privada a dirección IP pública depende de la dirección IP de destino donde se quiere enviar el tráfico.                                                                                                                                                                                                                                 | ✅                |

__[_Fuente original_](https://es.wikipedia.org/wiki/Traducci%C3%B3n\_de\_direcciones\_de\_red)__

## 2. Tipo de firewall

{% hint style="warning" %}
**Solo es necesario aplicar las siguientes reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en los puertos 80 (UDP/TCP) y 443 (TCP/TLS). En caso que las conexiones UDP estén bloqueadas nuestro sistema intentará automáticamente por TCP.
{% endhint %}



{% hint style="info" %}
Si posees un firewall de capa 3, contáctanos a [support@videsk.io](mailto:support@videsk.io), con el asunto: "**IPs turn servers list"**, para obtener el listado de IP de nuestros servidores. _Verificaremos tu identidad asociada a la organización._
{% endhint %}

Para añadir las reglas tu firewall debe permitir añadir listados de FQDN wildcard, eso significa añadir subdominios de la siguiente manera: `*.videsk.io`

{% hint style="info" %}
Debes considerar que si las reglas aplicadas sobre la red son sobre protocolos `UDP` y/o `TCP`, como mínimo se debe permitir tráfico por protocolo `TCP`.
{% endhint %}

## 2. Listar servidores

{% hint style="warning" %}
**Solo es necesario aplicar las siguientes reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en los puertos 80 (UDP/TCP) y 443 (TCP/TLS). En caso que las conexiones UDP estén bloqueadas nuestro sistema intentará automáticamente por TCP.
{% endhint %}



Si ya has reconocido el tipo de NAT y Firewall que posees, entonces procede a crear una regla de acceso a nuestros servidores con los siguientes datos:

### FQDN

{% hint style="success" %}
Te sugerimos para máxima compatibilidad añadir nuestro dominio wildcard **`*.videsk.io`** a tu firewall.
{% endhint %}

Deberás añadir nuestro dominio `wilcard` de servidores TURN a una lista blanca:

```bash
*.turn.videsk.io
```

{% hint style="danger" %}
Sugerimos no utilizar direcciones IP, ya que nuestra infraestructura varía dependiendo de la posición geográfica, por lo que podemos incrementar el número de servidores o disminuirlos según la demanda, **no recomendamos utilizar las IPs**.
{% endhint %}

{% hint style="info" %}
Si posees un firewall de capa 3, contáctanos a [support@videsk.io](mailto:support@videsk.io), con el asunto: "**IPs turn servers list"**, para obtener el listado de IP de nuestros servidores. _Verificaremos tu identidad asociada a la organización._
{% endhint %}

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

Adicional a los dominios anteriores sugerimos añadir los siguientes dominios wildcard de servicios de terceros, los cuales nos permiten entregar un mejor soporte.

```
cloudflareinsights.com
*.pendo.io
*.lr-ingest.io
*.ipregistry.co
```

{% hint style="warning" %}
Nuestros servicios se encuentran detrás nuestro proxy WAF Cloudflare, la lista de servidores se encuentran en el siguiente enlace: [https://www.cloudflare.com/ips/](https://www.cloudflare.com/ips/)
{% endhint %}

{% hint style="warning" %}
La lista de IP de nuestro monitor de errores Sentry se encuentra en el siguiente enlace: [https://docs.sentry.io/product/security/ip-ranges/](https://docs.sentry.io/product/security/ip-ranges/)&#x20;
{% endhint %}

{% hint style="danger" %}
Utilizamos un monitor de sesiones llamado LogRocket, actualmente no es posible listar por IP, por lo que sugerimos utilizar listas blancas por dominio base.
{% endhint %}

{% hint style="info" %}
**Es importante para entregar el mejor servicio, que nuestros sistemas de monitoreo no sean bloqueados por extensiones del navegador, equipo o redes. De lo contrario dificulta a nuestro equipo identificar y resolver problemas de forma proactiva.**
{% endhint %}

### Puertos

{% hint style="warning" %}
**Solo es necesario aplicar las siguientes reglas a tu firewall en caso que las políticas sean muy restrictivas o por dominios**. Todo nuestro tráfico se realiza en los puertos 80 (UDP/TCP) y 443 (TCP/TLS). En caso que las conexiones UDP estén bloqueadas nuestro sistema intentará automáticamente por TCP.
{% endhint %}



Utilizamos puertos estándar como el `80` y `443`, tanto para comunicación con nuestra Rest API como nuestros servidores TURN.

Para el caso de nuestra red TURN utilizamos conexiones mediante puerto 80 sobre protocolo `UDP` y `TCP`, el cual se adaptará dependiendo de la disponibilidad `UDP` de la red. Mientras que el puerto `443` sobre `TLS/TCP` para usar relé cifrado punto a punto de estar disponible sobre la red.

{% hint style="info" %}
Para el caso del puerto `80` en toda nuestra infraestructura realizará una redirección automática al puerto `443`.
{% endhint %}
