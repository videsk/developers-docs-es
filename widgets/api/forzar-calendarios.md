# Forzar calendarios

Con esta función podrás forzar la enumeración de calendarios en tu widget de forma muy simple. Es decir, sobreescribirá el listado de calendarios públicos que se muestran en el widget por los que definas mediante este método.

## Cómo usar

Lo primero de debes hacer es buscar el o los ID de los calendrios en tu cuenta dashboard, desde el menú **Calendarios**. Luego deberás generar un listado (`Array`) con ellos:

```javascript
[
    { name: "Nombre del calendario", id: "635c836300f9e8246a0f95f2" },
    { name: "Nombre del calendario 2", id: "635c837e2f38b41ad2143b71" },
]
```

{% hint style="info" %}
Deberás reemplazar el nombre en `name` y pegar el ID del calendario en `id`.
{% endhint %}

Finalmente deberás usar el listado y guardarlo en el almacenamiento local `localStorage`.

```javascript
const segments = [...];
window.localStorage.setItem('videsk-custom-calendars', JSON.stringify(segments));
```

{% hint style="warning" %}
Este script personalizado debe ser añadido y cargado antes que el script del widget, de lo contrario no lo reconocerá, cargando normalmente.
{% endhint %}

## Ejemplo

Este ejemplo es funcional por lo que solo deberás cambiar el nombre del calendario y pegar el ID correspondiente.

{% hint style="info" %}
Recuerda que puedes usar uno o más calendarios.
{% endhint %}

{% tabs %}
{% tab title="Javascript" %}
{% code title="Pure javascript" lineNumbers="true" %}
```javascript
const calendars = [
    { name: "Mi calendario", id: "635c843f35f1254a417612d9" }
];
window.localStorage.setItem('videsk-custom-calendars', JSON.stringify(calendars));
```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
```html
<script>
const calendars = [
    { name: "Mi calendario", id: "635c843f35f1254a417612d9" }
];
window.localStorage.setItem('videsk-custom-calendars', JSON.stringify(calendars));
</script>
```
{% endtab %}
{% endtabs %}

