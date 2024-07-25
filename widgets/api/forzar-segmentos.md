# Forzar segmentos

Con esta función podrás forzar la enumeración de segmentos en tu widget de forma muy simple. Es decir, sobreescribirá el listado de segmentos públicos que se muestran en el widget por los que definas mediante este método.

## Cómo usar

Lo primero de debes hacer es buscar el o los ID de los segmentos en tu cuenta dashboard. Luego deberás generar un listado (`Array`) con ellos:

```javascript
[
    { name: "Nombre del segmento", id: "635c836300f9e8246a0f95f2" },
    { name: "Nombre del segmento 2", id: "635c837e2f38b41ad2143b71" },
]
```

{% hint style="info" %}
Deberás reemplazar el nombre en `name` y pegar el ID del segmento en `id`.
{% endhint %}

Finalmente deberás usar el listado y guardarlo en el almacenamiento local `localStorage`.

```javascript
const segments = [...];
window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
```

{% hint style="warning" %}
Este script personalizado debe ser añadido y cargado antes que el script del widget, de lo contrario no lo reconocerá y cargaron los segmentos configurados en la cuenta.
{% endhint %}

## Ejemplo

Este ejemplo es funcional por lo que solo deberás cambiar el nombre del segmento y pegar el ID correspondiente.

{% hint style="info" %}
Recuerda que puedes usar uno o más segmentos.
{% endhint %}

{% tabs %}
{% tab title="Javascript" %}
{% code title="Pure javascript" lineNumbers="true" %}
```javascript
const segments = [
    { name: "Mi segmento", id: "635c843f35f1254a417612d9" }
];
window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
```html
<script>
const segments = [
    { name: "Mi segmento", id: "635c843f35f1254a417612d9" }
];
window.localStorage.setItem('videsk-custom-segments', JSON.stringify(segments));
</script>
```
{% endtab %}
{% endtabs %}

