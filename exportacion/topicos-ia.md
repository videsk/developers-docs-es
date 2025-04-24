# Tópicos IA

## Obtener tópicos IA

<mark style="color:green;">`POST`</mark> `/reports/exports/ai/topics`

Podrás usar este endpoint para exportar los registros de tópicos IA de tu cuenta.

**Headers**

| Name          | Value                |
| ------------- | -------------------- |
| Content-Type  | `application/json`   |
| Authorization | `Bearer <api-token>` |

**Body**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Requerido</th></tr></thead><tbody><tr><td><code>$sort</code></td><td>número</td><td>Orden más antiguo (<code>1</code>), más nuevo (<code>-1</code>)</td><td>true</td></tr><tr><td><code>start</code></td><td>fecha</td><td>Rango inicial en formato ISO</td><td>true</td></tr><tr><td><code>end</code></td><td>fecha</td><td>Rango final en formato ISO</td><td>true</td></tr><tr><td><code>keys</code> </td><td>objeto (opcional)</td><td>Listado con el nombre de columnas</td><td>false</td></tr><tr><td><code>timezone</code></td><td>texto</td><td>Nombre de la zona horaria (<a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a>)</td><td>true</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201 Created" %}
```json
{
    "$limit": 5000,
    "columns": [
        "Identificador",
        "Entity Type",
        "Fecha",
        "Nombre del Topico",
        "Puntuación del Topico",
    ],
    "data": [
        {
            "Identificador": "67fd221efc5f3630ed2d7f8e",
            "Entity Type": "calls",
            "Nombre del Topico": "venta",
            "Puntuación del Topico": 0.75,
            "Fecha": "14/04/2023, 10:58:06"
        }
    ]
}
```
{% endtab %}
{% endtabs %}
