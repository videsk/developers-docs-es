# Google Tag Manager

Puedes integrar Videsk mediante Google Tag Manager en menos de 5 minutos! A continuación te explicamos como realizarlo.

{% hint style="warning" %}
Es posible que no visualices tu widget mediante GTM (Google Tag Manager), si estás usando un bloqueador de anuncios. Esto debido a que los bloqueadores de anuncios como extensiones o nativos del navegador bloquean la carga de GTM y en su defecto el widget.
{% endhint %}

{% embed url="https://www.loom.com/share/5815ca21319c4c71895116020e5e102e" %}

## 1. Crear nueva etiqueta

Deberás ingresar al espacio de trabajo asociado al sitio web que deseas integrar Videsk. Luego dar clic en **Añadir nueva etiqueta**.

![](<../../.gitbook/assets/image (44).png>)

Se desplegará una ventana lateral derecha, donde deberás dar clic en el rectángulo blanco con título **Configuración de la etiqueta**.

![](<../../.gitbook/assets/image (37).png>)

## 2. Instalar etiqueta de Videsk

A continuación, deberás seleccionar la integración mediante plantillas comunitarias.

![](<../../.gitbook/assets/image (43).png>)

Luego que cargue el listado deberás buscar "**Videsk**" mediante el buscador ubicado en la parte superior derecha.

![](<../../.gitbook/assets/image (42).png>)

Luego dar clic en el botón azul, **Añadir a espacio de trabajo**.

![](<../../.gitbook/assets/image (68).png>)

Finalmente deberás dar clic en **Añadir**.

![](<../../.gitbook/assets/image (1) (2).png>)

{% hint style="info" %}
La secuencia de comendas a insertar es el mismo el cual puedes obtener desde tu cuenta dashboard.
{% endhint %}

## 3. Configurar token de cuenta

Ahora ya configurada la etiqueta debemos ingresar el token de nuestro widget.

![](<../../.gitbook/assets/image (24).png>)

Para ello debemos ir a nuestra cuenta dashboard, luego en **Integraciones** y finalmente la pestaña **Integración**.

![](<../../.gitbook/assets/image (22) (1).png>)

Deberás dar clic en el segundo botón de **Copiar**, y luego pegarlo en el campo **Public Token**.

## 4. Definir activadores

Ahora ya tienes integrado Videsk, basta con definir cuales serán los activadores para que sea visible el widget.

Dependiendo de tu caso podrás hacer uso de activadores preestablecidos en tu cuenta, definir acciones del usuario o solo en ciertas páginas.

Puedes ver nuestro video en la parte superior donde explicamos cómo definir un activador para ciertas páginas de nuestro sitio web.

![](<../../.gitbook/assets/image (46).png>)

## Medición de `custom events`

Para realizar medición de eventos equivalentes a interacciones de un usuario con el widget a través de Google Tag Manager debes seguir los siguientes pasos:

### 1. Crear `trigger`

Debe ir al menú lateral llamado **Triggers**.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Luego deberás dar crear un nuevo trigger desde el botón ![](<../../.gitbook/assets/image (71).png>). A continuación, selecciona el tipo de triger llamado `Custom Event` en la categoría de Other.

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Luego en el campo Event name debes escribir `videsk.*` lo que capturará todos los eventos. Recuerda que deberás activar la opción Use regex matching.

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
En caso que no desees escuchar todos los eventos, deberás escribir el evento manualmente como `videsk.toggle`, `videsk.load`, `videsk.selected`, etc.
{% endhint %}

#### Nomenclatura de eventos

A diferencia de los [eventos capturables a través de Javascript en tu sitio web](../api/eventos.md), con Google Tag Manager la nomentaclatura es similar pero sin el prefijo `on` y en minúsculas, es decir:

| Event name nativo | Event name GTM  |
| ----------------- | --------------- |
| onLoad            | videsk.load     |
| onSelected        | videsk.selected |
| onQueued          | videsk.queued   |

Puedes encontrar el listado de eventos disponibles en la siguiente página:

{% content-ref url="../api/eventos.md" %}
[eventos.md](../api/eventos.md)
{% endcontent-ref %}

Finalmente, debes asegurarte de que el trigger se ha creado correctamente:

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

### 2. Crear etiqueta (tag)

Ahora simplemente deberás crear tu etiqueta pero en el caso de trigger deberás seleccionar el tigger custom event que haz creado previamente.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Finalmente, basado en tus necesidad podrás enviar esta información hacia Google Analytics o cualquier otra plataforma/integración que requieras.
