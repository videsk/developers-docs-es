---
description: Aprende a usar las variables para integrar Videsk con terceros.
---

# 🦱 Variables

Las variables como debes conocer permiten almacenar datos para luego utilizarlos en partes del código y hacer referencia a ellas.

En el caso de nuestros Webhooks, permiten que puedas inyectar variables que dependerán de condiciones, estados, etc.

Por ejemplo, esta oración que indica una orden posee dos variables:

```handlebars
Computadora ejecuta {{action}} dentro de {{period}} días.
```

Dependiendo del valor de `action` y `period` la oración podrá tener distintos resultados, pero siempre obtendrás una oración con acción y periodo.

## Variables por evento

En caso de webhooks, cada evento posee sus propias variables, algo similar a un diccionario de variables por evento.

Estos eventos los podrás encontrar directamente en el modo editor cuando creas un nuevo webhook, que están ubicados en la parte lateral junto con la pestaña de documentación.

![Ejemplo de diccionario](<../.gitbook/assets/image (70).png>)

Como cada evento posee sus propias variables, podrás obtener información de cada una de ellas como tipo, descripción y nombre.

* `type` corresponde al tipo de dato ya sea `array`, `string`, `boolean`, `object`.
* `description` corresponde al contexto de la variable.
* `name` corresponde al nombre de la variable.

{% hint style="warning" %}
Para el caso de variables tipo `array`, solo es posible acceder mediante helpers de tipo `#array` o indicando el indice que deseas obtener en sintaxis handlebars.
{% endhint %}
