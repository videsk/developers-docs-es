# Ajustes

Nuestro widget posee una configuración o ajuste que contiene componentes como colores de cabecera, cuerpo, botones y textos, donde cada uno de ellos se puede configurar por separado.

Por defecto, el comportamiento es obtener el ajuste del widget que hayas configurado en tu cuenta mediante nuestra API.

{% hint style="info" %}
Recuerda que esta función permite sobre escribir los ajustes y diseños que hayas configurado desde tu cuenta.
{% endhint %}

Pero también es posible forzar un ajuste propio añadiendo un poco de código en tu sitio web. Para ello deberás tener en cuenta que la estructura es la siguiente:

```json
{
   "logo": {
      "url": "...",
      "height": 180
   },
   "colors": {
      "background": "rgb(255,255, 255, 1)",
      "font": "rgb(255,255, 255, 1)",
      "gradient": "linear-gradient(to right, rgb(23, 54, 189) 0%, rgb(0, 99, 255) 100%)"
   },
   "texts": {
      "title": "My title",
      "subtitle": "My subtitle.",
      "segmentsTitle": "Segment title",
      "segmentsSubtitle": "Segment subtitle."
   },
   "settings": { "defaultChannel": "video" },
   "orgName": "Company Name",
   "services": ["on-demand"]
}
```

Esta estructura de parámetros te permite modificar logotipo, colores, textos, ajustes y servicios a visibilizar.

{% hint style="warning" %}
Lee a continuación antes de modificar la estructura del ajuste.
{% endhint %}

### Logo

* `url` deberás colocar una URL válida de tu logotipo
* `height` deberás ingresar el tamaño del logotipo como número (sin unidades)

### Colors

{% hint style="info" %}
Es posible en HEX, HSL, pero no es recomendado.
{% endhint %}

* `background` deberás ingresar un color en formato RGB.
* `font` deberás ingresar un color en formato RGB.
* `gradient` deberás ingresar un gradiente en formato RGB o un solo color RGB.

### Texts

{% hint style="info" %}
Si deseas ocultar un título o subtitulo, simplemente puedes dejarlo como vacío, des decir, **`""`**.
{% endhint %}

* `title` deberás ingresar el título de la cabecera del widget.
* `subtitle` deberás ingresar el subtitulo de cabecera del widget.
* `segmentTitle` deberás ingresar el título que estará sobre el listado de segmentos.
* `segmentSubtitle` deberás ingresar el subtitulo que estará sobre el listado de segmentos.

### Settings

* `defaultChannel` permite seleccionar valor por defecto entre `video` o `audio`.

{% hint style="info" %}
Esta opción solo marcará una opción (micrófono o cámara) por defecto, pero tu cliente podrá igualmente escoger el que desee.
{% endhint %}

### OrgName

Ingresa el nombre de tu negocio en este campo.

### Services

Deberás escoger qué tipos de servicios están activos para tu widget, ya sea entre `on-demand` que representa tus segmentos y `schedule` para calendarios. Podrás escoger entre uno u otro.

{% hint style="danger" %}
**No añadas un servicio al listado si no posees al menos 1 segmento o calendario activo en tu cuenta.**



El comportamiento del widget podría ser inesperado.
{% endhint %}

## Aplicar estilos

Luego que haz modificado los parámetros del widget deberás aplicar este cambio añadiendo un poco de código a tu sitio web.

{% hint style="info" %}
La técnica a utilizar a continuación la puedes aplicar desde Devtools en tu navegador para pre-visualizar el diseño antes de aplicarlo en tu sitio.
{% endhint %}

```javascript
const widgetStyle = {...};
window.localStorage.setItem('widget-custom-style', JSON.stringify(widgetStyle));
```

`widgetStyle` corresponde a los parámetros configurados previamente. Si obtienes un error de `parsing` verifica que haz escrito correctamente en formato `JSON` o como objeto.

{% hint style="info" %}
Refresca tu sitio y verás los cambios.
{% endhint %}

{% hint style="warning" %}
No modifiques el nombre clave `widget-custom-style`, de esta manera identificamos los parámetros personalizados.
{% endhint %}
