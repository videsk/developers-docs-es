---
description: Aprende a usar las variables para integrar Videsk con terceros.
---

# 馃Ρ Variables

Las variables como debes conocer permiten almacenar datos para luego utilizarlos en partes del c贸digo y hacer referencia a ellas.

En el caso de nuestros Webhooks, permiten que puedas inyectar variables que depender谩n de condiciones, estados, etc.

Por ejemplo, esta oraci贸n que indica una orden posee dos variables:

```handlebars
Computadora ejecuta {{action}} dentro de {{period}} d铆as.
```

Dependiendo del valor de `action` y `period` la oraci贸n podr谩 tener distintos resultados, pero siempre obtendr谩s una oraci贸n con acci贸n y periodo.

## Variables por evento

En caso de webhooks, cada evento posee sus propias variables, algo similar a un diccionario de variables por evento.

Estos eventos los podr谩s encontrar directamente en el modo editor cuando creas un nuevo webhook, que est谩n ubicados en la parte lateral junto con la pesta帽a de documentaci贸n.

![Ejemplo de diccionario](<../.gitbook/assets/image (52).png>)

Como cada evento posee sus propias variables, podr谩s obtener informaci贸n de cada una de ellas como tipo, descripci贸n y nombre.

* `type` corresponde al tipo de dato ya sea `array`, `string`, `boolean`, `object`.
* `description` corresponde al contexto de la variable.
* `name` corresponde al nombre de la variable.

{% hint style="warning" %}
Para el caso de variables tipo `array`, solo es posible acceder mediante helpers de tipo `#array` o indicando el indice que deseas obtener en sintaxis handlebars.
{% endhint %}
