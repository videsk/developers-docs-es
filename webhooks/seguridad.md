---
description: >-
  Te explicamos cómo funcionan nuestros webhooks desde una perspectiva de
  seguridad.
---

# 🔒 Seguridad

Nuestra tecnología de webhooks permite máxima flexibilidad y compatibilidad con cualquier plataformas moderna y legadas. Esto al mismo tiempo conlleva que la seguridad sea un pilar fundamental a la hora de utilizar esta función.

Por eso, te sugerimos leer con detención las siguientes recomendaciones e información sobre como opera nuestra tecnología.

## Secretos

Los secretos permiten almacenar de forma segura información sensible como llaves privadas, tokens, nombre de usuarios, contraseñas, etc. Es decir, toda información que no debería ser visible por nadie, **nunca**.

Por ello, dispones de la opción de añadir una cantidad ilimitada de secretos, siendo de tu responsabilidad determinar cuando debe ser un secreto o no.

{% hint style="info" %}
El uso de secretos no impacta en el rendimiento a la hora de enviar los datos de un evento a una plataforma.
{% endhint %}

**Una vez que los secretos se crean, no podrán ser vistos por nadie nunca más, ni si quiera por el usuario que lo haya creado.**

Si requieres ver el valor de un secreto, deberás intentar obtenerla desde la plataforma emisora. Por seguridad los secretos son cifrados en reposo y solo son descifrados en tiempo de ejecución al momento de ser enviados.

**Las llaves de cifrado son almacenadas de forma seguras y nadie del personal de Videsk tiene acceso a ellas.**

El cifrado utilizado para el almacenamiento de secretos en reposo es AES-256-CBC.

{% hint style="info" %}
Los secretos tienen un límite de 2000 caracteres como máximo.



Si requieres aumentar este tamaño contáctanos a **support@videsk.io**.
{% endhint %}

## Autenticación o autorización

Te recomendamos utilizar plataformas que dispongan mecanismos de autenticación o autorización mediante tokens o claves únicas.

{% hint style="info" %}
Videsk es compatible con cabeceras de autorización básica _usuario:contraseña_.
{% endhint %}

Para ello, visita la documentación de desarrolladores de la plataforma que deseas integrar y busca la sección de autenticación o autorización. Por ejemplo, la mayoría de las plataformas te entregarán una API Key la cual debe ser enviada en la cabecera de la petición o en algunos casos como parámetro en la URL.

La forma más común es crear una cabecera llamada `Authorization` la cual deberá contener el valor de autorización.

{% hint style="info" %}
No entregamos rangos IP ya que estas son dinámicas y globales lo que nos permite escalar y evitar bloqueos por parte de las plataformas de todos nuestros clientes.
{% endhint %}

## Buenas prácticas

{% hint style="danger" %}
Está prohibido el uso de nuestra API en la URL, se suspenderá tu cuenta de manera indefinida si intentas generar un ataque self-inflected DoS.
{% endhint %}

### Autenticación o autorización

No utilices nuestras IPs para autorizar o validar envío de datos, ya que estas son dinámicas y eventualmente podrían ser utilizadas por otros servicios ajenos a Videsk.

{% hint style="info" %}
Siempre prefiere utilizar claves públicas/privadas.
{% endhint %}

### Límite de ratio

Verifica con la plataforma que deseas integrar cual es el límite de peticiones por unidad de tiempo. Videsk no puede controlar la cantidad de peticiones por unidad de tiempo, ya que en gran medida dependerá de la actividad de las llamadas, filas, etc.

{% hint style="info" %}
Intentamos enviar peticiones desde diferentes IPs para evitar bloqueos masivos.
{% endhint %}

### Errores

Podrás depurar los errores que puedan surgir durante el envío de webhooks mediante el registros de errores que tenemos incorporado. Por defecto, intentamos sanear los datos como cabeceras, parámetros, condicional, cuerpo de la petición, etc. reemplazando los valores de los secretos por asteriscos `******`.

{% hint style="warning" %}
Por seguridad, no saneamos las respuestas de la aplicación. Por lo que si esta retorna información sensible deberás informarlo a ellos.
{% endhint %}

### Pruebas

Verifica el formato generado en nuestro editor incorporado antes de enviar a la plataforma original, de esta forma evitaras bloqueos o eventualmente marquen tu cuenta como sospechosa.

Adicionalmente, te sugerimos utilizar plataformas playground como las mencionadas acá para evitar constantes peticiones con errores.

{% content-ref url="integraciones/" %}
[integraciones](integraciones/)
{% endcontent-ref %}

### SSL

Una opción disponible en webhooks es desactivar la validación de SSL. Por defecto, verificamos que el SSL del punto final sea válida por medida de seguridad, de esta forma te podemos asegurar que el transporte de datos sea cifrada entre nuestros servidores y los de la plataforma en cuestión.

Si necesitas puedes desactivar la verificación pero esto provocará que el transporte de datos eventualmente no sea seguro si el SSL de la plataforma no es válido.

{% hint style="info" %}
Si tienes activada la opción de verificar SSL y ves errores de certificado deberás comunicarte con la plataforma para verificar que su certificado es válido.
{% endhint %}

{% hint style="success" %}
Te recomendamos siempre verificar que el protocolo de comunicación en la URL comience con `https://`, de lo contrario la comunicación no será cifrada.&#x20;
{% endhint %}

## Infraestructura

La infraestructura de nuestros webhooks fueron diseñados con la seguridad como pilar número uno. Utilizamos tecnología serverless lo que nos permite escalar a millones de peticiones por segundo y generando una aislación de todas las peticiones que se realizan en nuestra plataforma.

Este diseño fue pensado frente a eventuales ataques provenientes de nuestra misma plataforma hacia terceros o inclusive ejecución de código remoto.

Nuestras instancias serverless solo se ejecutan por un máximo de 60 segundos destruyendo toda información en tiempo de ejecución, no habiendo relación de memoria entre peticiones. En caso que una petición demore más de 30 segundos en responder se cancelará y retornará un error que podrás visualizar en los registros.

Todo se ejecuta dentro de nuestra red VPC y sale de ella una vez que la petición está completamente lista.

{% hint style="info" %}
La velocidad promedio de transferencia entre plataformas comerciales, no supera los 250 milisegundos.
{% endhint %}

## Compartir secretos

{% hint style="warning" %}
Nuestro protocolo dicta que la prioridad es que nuestros clientes deben cargar sus secretos de plataformas terceras directamente en su propia cuenta, evite compartirnos credenciales por la seguridad de su propio negocio.
{% endhint %}

En caso que estés realizando una integración asistida por nuestro equipo y requieras compartir credenciales de acceso a cuentas de tus proveedores, deberá seguir nuestros protocolos, evitando siempre a toda costa enviar información sensible como credenciales en texto plano sin mecanismos de protección.

Nuestro protocolo dicta que toda información será almacenada internamente en baúles de credenciales diseñadas especificamente para estas situaciones con tiempo de expiración.

### Protocolo (credential sharing)

1. <mark style="color:red;">**Analice si realmente es necesario compartir credenciales con nuestro equipo de soporte, API keys, tokens, etc. pueden ser cargados directamente a través de la plataforma.**</mark>
2. Ingrese a Doppler Share: [https://share.doppler.com/](https://share.doppler.com/)
3. Ajuste el tiempo de expiración en 1 vista (1 view) y 1 día (1 day).
4. Copie y pegue la información a compartir
5. Copie la URL generada
6. Envíe un correo a [security@videsk.io](mailto:security@videsk.io) con el asunto: <mark style="background-color:yellow;">Customers integration credentials sharing</mark>
7. En el cuerpo del correo debe enviar la siguiente estructura:

<pre><code>Empresa: (Nombre del negocio)
Detalles: (Describa el tipo de información sensible a compartir)
<strong>Clasificación: (Crítica, Alta, Media o Baja)
</strong>Tiempo de expiración: (Indique cuánto tiempo se deberá retener esta información, por defecto: 3 meses)
Contacto de seguridad: (Correo del personal de su negocio encargado de notificaciones de seguridad)
</code></pre>

{% hint style="danger" %}
No comparta credenciales a ningún otro correo que no corresponda a **security@videsk.io**.
{% endhint %}
