# Reuniones

## Obtener reuniones

<mark style="color:green;">`POST`</mark> `/reports/exports/appointments`

Podrás usar este endpoint para exportar los registros de reuniones de tu cuenta.

**Headers**

| Name          | Value                |
| ------------- | -------------------- |
| Content-Type  | `application/json`   |
| Authorization | `Bearer <api-token>` |

**Body**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Requerido</th></tr></thead><tbody><tr><td><code>$sort</code></td><td>número</td><td>Orden más antiguo (<code>1</code>), más nuevo (<code>-1</code>)</td><td>true</td></tr><tr><td><code>start</code></td><td>fecha</td><td>Rango inicial en formato ISO</td><td>true</td></tr><tr><td><code>end</code></td><td>fecha</td><td>Rango final en formato ISO</td><td>true</td></tr><tr><td><code>keys</code> </td><td>objeto</td><td>Listado con el nombre de columnas</td><td>false</td></tr><tr><td><code>timezone</code></td><td>texto</td><td>Nombre de la zona horaria (<a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a>)</td><td>true</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201 Created" %}
```json
{
    "$limit": 5000,
    "columns": [
        "Identificador",
        "Service",
        "Agente",
        "Inicio",
        "Fin",
        "Duración",
        "ID Encuesta",
        "Meta Data",
        "Comentarios",
        "Etiquetas",
        "Cliente cortó",
        "ID formulario agente",
        "ID formulario cliente",
        "Type",
        "Status",
        "Cancellation Date",
        "Canceled By",
        "Razón Cancelación",
        "Rescheduled Appointment ID",
        "Creado por"
    ],
    "data": [
        {
            "Identificador": "6808ff4bdfd67ff66bc9940b",
            "Service": "Demos",
            "Agente": "john@videsk.io",
            "Inicio": "2023-04-23 11:15:00",
            "Fin": "2023-04-23 11:45:00",
            "Duración": 18.62773333333333,
            "Meta Data": "6808ff4bdfd67ff66bc99409",
            "Etiquetas": "",
            "Cliente cortó": null,
            "ID formulario cliente": "6808ff4bdfd67ff66bc993f8",
            "Type": "scheduled",
            "Status": "attended",
            "Cancellation Date": null
        }
    ]
}
```
{% endtab %}
{% endtabs %}
