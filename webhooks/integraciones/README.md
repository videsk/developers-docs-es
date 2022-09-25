---
description: Descubre como integrar Videsk con otras plataformas
---

# 🎛 Integraciones

Si está aquí es porque estas buscando como integrar Videsk con otras plataformas de forma sencilla y en menos de 60 minutos.

El primer paso es conocer en qué formato y estructura la plataforma deberá recibir los datos. Para ello te sugerimos buscar en Google "_**Nombre de plataforma**_ Rest API docs".

Podrás encontrar un listado de integraciones a modo de ejemplo en esta documentación, pero recuerda que somos compatible con casi todas las plataformas de mercado.

## Playground

Antes de comenzar la integración te recomendamos utilizar alguna plataforma gratuita que te permita recibir las peticiones de nuestros servidores para poder depurar y validar que todo esté correcto antes de enviar peticiones reales al servicio en producción.

| URL                                    | Descripción                                  | Precios       |
| -------------------------------------- | -------------------------------------------- | ------------- |
| [Webhook.site](https://webhook.site/)  | Simple, sin registros y rápido.              | Gratis y pago |
| [Request Bin](https://requestbin.com/) | Completo pero más complejo.                  | Gratis y pago |
| [Ngrok](https://ngrok.com/)            | Local, requiere instalación y configuración. | Gratis.       |
| [Cloudflare Tunnel](./#playground)     | Local, requiere instalación y configuración. | Gratis.       |

{% hint style="info" %}
Te recomendamos utilizar [webhook.site](./#playground) para integraciones, en caso de servidores intermediarios que necesites desarrollar te sugerimos utilizar [ngrok](https://ngrok.com/) o [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation).
{% endhint %}

## Compatibilidad

**Videsk solo es compatible** con plataformas que permitan recibir **peticiones HTTP de un solo envío**, es decir, que no requieran pasos intermedios como autenticación o validación de dos pasos.

Por seguridad todas las plataformas debiesen utilizar al menos 1 método de autorización mediante API keys, tokens, contraseñas, etc. los cuales son enviados ya sea en cabeceras, como parámetros en la url o en pocos casos en el cuerpo de la petición. Estos métodos dependerán de la plataforma en cuestión.

{% hint style="warning" %}
Es de tú responsabilidad almacenar tokens, claves, o cualquier tipo de información sensible como secretos, de lo contrario podrían ser visibles por otras personas de tu equipo.
{% endhint %}

## Ejemplos de integraciones

{% content-ref url="power-bi.md" %}
[power-bi.md](power-bi.md)
{% endcontent-ref %}

{% content-ref url="airtable.md" %}
[airtable.md](airtable.md)
{% endcontent-ref %}
