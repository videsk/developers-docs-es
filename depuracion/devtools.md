---
description: >-
  A continuación te explicaremos la mejor manera de depurar errores ya sean al
  utilizar nuestros SDKs o APIs.
---

# Devtools

Esta guía te permitirá identificar los errores que puedan surgir utilizando alguno de nuestros productos, estos ya sean errores legítimos por implementación o incompatibilidad con navegadores.

{% hint style="success" %}
En general nuestros productos intentan ser lo más descriptivos posibles y en su mayoría presentan la capacidad de manejar los errores y reportarlo a nuestros sistemas.
{% endhint %}

Lo primero que deberás conocer como mejor herramienta del navegador para depurar ya sea en etapa de desarrollo o producción es **Devtools** o **Inspector de Elementos**.



## ¿Cómo acceder a Devtools?

Para acceder a él existen varias maneras y dependerá de cada navegador:

| Navegador           | Shortcut                                                | Por menú                                                                                                |
| ------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Chrome/Edge/Firefox | <ul><li>Ctrl + Shift + i</li></ul><ul><li>F12</li></ul> | Clic derecho + Inspeccionar                                                                             |
| Safari              | Option + ⌘ + C                                          | Safari > Preferencias > Avanzado, y selecciona la opción “Mostrar menú Desarrollo en la barra de menús” |

{% hint style="info" %}
**El clic derecho lo podrás realizar en cualquier lugar del sitio web.**
{% endhint %}

![Menú emergente al hacer clic derecho en el sitio](<../.gitbook/assets/image (66).png>)

{% hint style="info" %}
Si te hemos solicitado mantener abierto Devtools, por errores que nuestros sistemas de monitoreo no han logrado capturar, lee a continuación.
{% endhint %}

Si necesitas caputrar información ya sea de errores de código, red, etc. te sugerimos redimencionar la ventana Devtools para que no estorbe con la interfaz o bien utilizar la opción de desacoplar en una ventana independiente.

### Vista acoplada

![Vista acoplada](<../.gitbook/assets/image (27).png>)

### Vista desacoplada

Para acceder a la vista desacoplada deberás hacer clic en los tres puntos ![](<../.gitbook/assets/image (53).png>) ubicado en la parte superior derecha, y luego selecciona el ícono ![](<../.gitbook/assets/image (58).png>).

Luego de esto la ventana quedará completamente desacoplada y podrás minimizarla.

![Vista como ventana desacoplada](<../.gitbook/assets/image (57) (1).png>)

## Visualizar errores

La mejor forma de obtener los errores es hacer clic en la pestaña con el nombre **Console**, ubicado en la parte izquierda superior. Luego verás el listado de eventuales errores que hayan surgido durante la sesión.

{% hint style="info" %}
Si nuestro equipo técnico te ha solicitado que abras Devtools o Inspector de elementos, dirígete a la sección de exportar registros de errores.
{% endhint %}

![Vista de "console" con errores y advertencias](<../.gitbook/assets/image (54).png>)

Existen mensajes con distintos colores de fondo, los más comunes serán rojo y amarillo, siendo errores y advertencias, respectivamente.

En su mayoría los mensajes de advertencia no son relevantes, mientras que los mensajes en rojo son errores los cuales hay que prestar atención. En la anterior imagen, la mayoría de los errores visibles son bloqueo de recursos por extensiones de bloqueadores de anuncios, pero cuando algo ande mal verás mensajes más extensos con información en inglés sobre lo que ha sucedido.

## Exportar registros

Es probable que nuestro equipo técnico te solicite realizar una descarga de los registros de erorres que hayan surgido durante la sesión de una pestaña, debido a que en ocasiones ciertos errores no son registrados por nuestros sistemas, como errores de red, firewall, etc.

Para ello deberás estar en la [vista Console](devtools.md#visualizar-errores) y luego en cualquier lugar de la consola (Console) haz clic derecho, para finalmente dar clic en la opción **`Save as...`**.

![Menú emergente al hacer clic derecho en console](<../.gitbook/assets/image (67).png>)

El archivo que descarges deberás enviarlo a [support@videsk.io](mailto:support@videsk.io), con el asunto **Registros de errores**, adjuntando el archivo con registros que habitualmente se llamará **{website}-{date}.log**.

[Haz clic aquí para crear un correo automáticamente](mailto:support@videsk.io?subject=Registros%20de%20errores\&body=Empresa:%20XXXXX,%20Usuario:%20XXXX).
