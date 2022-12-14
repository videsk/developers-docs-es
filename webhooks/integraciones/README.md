---
description: Descubre como integrar Videsk con otras plataformas
---

# 馃帥 Integraciones

Si est谩 aqu铆 es porque estas buscando como integrar Videsk con otras plataformas de forma sencilla y en menos de 60 minutos.

El primer paso es conocer en qu茅 formato y estructura la plataforma deber谩 recibir los datos. Para ello te sugerimos buscar en Google "_**Nombre de plataforma**_ Rest API docs".

Podr谩s encontrar un listado de integraciones a modo de ejemplo en esta documentaci贸n, pero recuerda que somos compatible con casi todas las plataformas de mercado.

## Playground

Antes de comenzar la integraci贸n te recomendamos utilizar alguna plataforma gratuita que te permita recibir las peticiones de nuestros servidores para poder depurar y validar que todo est茅 correcto antes de enviar peticiones reales al servicio en producci贸n.

| URL                                    | Descripci贸n                                  | Precios       |
| -------------------------------------- | -------------------------------------------- | ------------- |
| [Webhook.site](https://webhook.site/)  | Simple, sin registros y r谩pido.              | Gratis y pago |
| [Request Bin](https://requestbin.com/) | Completo pero m谩s complejo.                  | Gratis y pago |
| [Ngrok](https://ngrok.com/)            | Local, requiere instalaci贸n y configuraci贸n. | Gratis.       |
| [Cloudflare Tunnel](./#playground)     | Local, requiere instalaci贸n y configuraci贸n. | Gratis.       |

{% hint style="info" %}
Te recomendamos utilizar [webhook.site](./#playground) para integraciones, en caso de servidores intermediarios que necesites desarrollar te sugerimos utilizar [ngrok](https://ngrok.com/) o [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation).
{% endhint %}

## Compatibilidad

**Videsk solo es compatible** con plataformas que permitan recibir **peticiones HTTP de un solo env铆o**, es decir, que no requieran pasos intermedios como autenticaci贸n o validaci贸n de dos pasos.

Por seguridad todas las plataformas debiesen utilizar al menos 1 m茅todo de autorizaci贸n mediante API keys, tokens, contrase帽as, etc. los cuales son enviados ya sea en cabeceras, como par谩metros en la url o en pocos casos en el cuerpo de la petici贸n. Estos m茅todos depender谩n de la plataforma en cuesti贸n.

{% hint style="warning" %}
Es de t煤 responsabilidad almacenar tokens, claves, o cualquier tipo de informaci贸n sensible como secretos, de lo contrario podr铆an ser visibles por otras personas de tu equipo.
{% endhint %}

## Ejemplos de integraciones

{% content-ref url="power-bi.md" %}
[power-bi.md](power-bi.md)
{% endcontent-ref %}

{% content-ref url="airtable.md" %}
[airtable.md](airtable.md)
{% endcontent-ref %}
