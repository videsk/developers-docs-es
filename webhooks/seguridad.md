---
description: >-
  Te explicamos c贸mo funcionan nuestros webhooks desde una perspectiva de
  seguridad.
---

# 馃敀 Seguridad

Nuestra tecnolog铆a de webhooks permite m谩xima flexibilidad y compatibilidad con cualquier plataformas moderna y legadas. Esto al mismo tiempo conlleva que la seguridad sea un pilar fundamental a la hora de utilizar esta funci贸n.

Por eso te sugerimos leer con detenci贸n las siguientes recomendaciones e informaci贸n sobre como opera nuestra tecnolog铆a.

## Secretos

Los secretos permiten almacenar de forma segura informaci贸n sensible como llaves privadas, tokens, nombre de usuarios, contrase帽as, etc. Es decir, toda informaci贸n que no deber铆a ser visible por nadie, **nunca**.

Por ello, dispones de la opci贸n de a帽adir una cantidad ilimitada de secretos, siendo de tu responsabilidad determinar cuando debe ser un secreto o no.

El uso de secretos no impacta en el rendimiento a la hora de enviar los datos de un evento a una plataforma.

**Una vez que los secretos se crean, no podr谩n ser vistos por nadie nunca m谩s, ni si quiera por el usuario que lo haya creado.**

Si requieres ver el valor de un secreto, deber谩s intentar obtenerla desde la plataforma emisora. Por seguridad los secretos son cifrados en reposo y solo son descifrados en tiempo de ejecuci贸n al momento de ser enviados.

**Las llaves de cifrado son almacenadas de forma seguras y nadie del personal de Videsk tiene acceso a ellas.**

El cifrado y descifrado utilizado para el almacenamiento de secretos en texto plano y en reposo es AES-256-CBC.

{% hint style="info" %}
Los secretos tienen un l铆mite de 2000 caracteres como m谩ximo.



Si requieres aumentar este tama帽o cont谩ctanos a **support@videsk.io**.
{% endhint %}

## Autenticaci贸n o autorizaci贸n

Te recomendamos utilizar plataformas que dispongan mecanismos de autenticaci贸n o autorizaci贸n mediante tokens o claves 煤nicas.

{% hint style="info" %}
Videsk es compatible con cabeceras de autorizaci贸n b谩sica _usuario:contrase帽a_.
{% endhint %}

Para ello visita la documentaci贸n de desarrolladores de la plataforma que deseas integrar y busca la secci贸n de autenticaci贸n o autorizaci贸n. Por ejemplo, la mayor铆a de las plataformas te entregar谩n una API Key la cual debe ser enviada en la cabecera de la petici贸n o en algunos casos como par谩metro en la URL.

La forma m谩s com煤n es crear una cabecera llamada `Authorization` la cual deber谩 contener el valor de autorizaci贸n.

{% hint style="info" %}
No entregamos rangos IP ya que estas son din谩micas y globales lo que nos permite escalar y evitar bloqueos por parte de las plataformas de todos nuestros clientes.
{% endhint %}

## Buenas pr谩cticas

{% hint style="danger" %}
Est谩 prohibido el uso de nuestra API en la URL, se suspender谩 tu cuenta de manera indefinida si intentas generar un ataque self-inflected DoS.
{% endhint %}

### Autenticaci贸n o autorizaci贸n

No utilices nuestras IPs para autorizar o validar env铆o de datos, ya que estas son din谩micas y eventualmente podr铆an ser utilizadas por otros servicios ajenos a Videsk.

{% hint style="info" %}
Siempre prefiere utilizar claves p煤blicas/privadas.
{% endhint %}

### L铆mite de ratio

Verifica con la plataforma que deseas integrar cual es el l铆mite de peticiones por unidad de tiempo. Videsk no puede controlar la cantidad de peticiones por unidad de tiempo, ya que en gran medida depender谩 de la actividad de las llamadas, filas, etc.

{% hint style="info" %}
Intentamos enviar peticiones desde diferentes IPs para evitar bloqueos masivos.
{% endhint %}

### Errores

Podr谩s depurar los errores que puedan surgir durante el env铆o de webhooks mediante el registros de errores que tenemos incorporado. Por defecto, intentamos sanear los datos como cabeceras, par谩metros, condicional, cuerpo de la petici贸n, etc. reemplazando los valores de los secretos por asteriscos `******`.

{% hint style="warning" %}
Por seguridad, no saneamos las respuestas de la aplicaci贸n. Por lo que si esta retorna informaci贸n sensible deber谩s informarlo a ellos.
{% endhint %}

### Pruebas

Verifica el formato generado en nuestro editor incorporado antes de enviar a la plataforma original, de esta forma evitaras bloqueos o eventualmente marquen tu cuenta como sospechosa.

Adicional te sugerimos utilizar plataformas playground como las mencionadas ac谩 para evitar constantes peticiones con errores.

{% content-ref url="integraciones/" %}
[integraciones](integraciones/)
{% endcontent-ref %}

### SSL

Una opci贸n disponible en webhooks es desactivar la validaci贸n de SSL. Por defecto, verificamos que el SSL del punto final sea v谩lida por medida de seguridad, de esta forma te podemos asegurar que el transporte de datos sea cifrada entre nuestros servidores y los de la plataforma en cuesti贸n.

Si necesitas puedes desactivar la verificaci贸n pero esto provocar谩 que el transporte de datos eventualmente no sea seguro si el SSL de la plataforma no es v谩lido.

{% hint style="info" %}
Si tienes activada la opci贸n de verificar SSL y ves errores de certificado deber谩s comunicarte con la plataforma para verificar que su certificado es v谩lido.
{% endhint %}

{% hint style="success" %}
Te recomendamos siempre verificar que el protocolo de comunicaci贸n en la URL comience con `https://`, de lo contrario la comunicaci贸n no ser谩 cifrada.&#x20;
{% endhint %}

## Infraestructura

La infraestructura de nuestros webhooks fueron dise帽ados con la seguridad como pilar n煤mero uno. Utilizamos tecnolog铆a serverless lo que nos permite escalar a millones de peticiones por segundo y generando una aislaci贸n de todas las peticiones que se realizan en nuestra plataforma.

Este dise帽o fue pensado frente a eventuales ataques provenientes de nuestra misma plataforma hacia terceros o inclusive ejecuci贸n de c贸digo remoto.

Nuestras instancias serverless solo se ejecutan por un m谩ximo de 60 segundos destruyendo toda informaci贸n en tiempo de ejecuci贸n, no habiendo relaci贸n de memoria entre peticiones. En caso que una petici贸n demore m谩s de 30 segundos en responder se cancelar谩 y retornar谩 un error que podr谩s visualizar en los registros.

Todo se ejecuta dentro de nuestra red VPC y sale de ella una vez que la petici贸n est谩 completamente lista.

{% hint style="info" %}
La velocidad promedio de transferencia de datos entre plataformas comerciales no supera los 250 milisegundos.
{% endhint %}
