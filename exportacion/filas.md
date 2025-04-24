# Filas

## Obtener filas

<mark style="color:green;">`POST`</mark> `/reports/exports/queues`

Podrás usar este endpoint para exportar los registros de fila de tu cuenta.

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
        "Segmento",
        "Inicio",
        "Fin",
        "Rechazada",
        "Abandonada",
        "Asignada",
        "Duración",
        "Razón Cancelación",
        "ID formulario cliente",
        "Meta Data",
        "Conexiones",
        "Desconexiones",
        "Integration Data"
    ],
    "data": [
        {
            "Identificador": "67ed331f6969ca55b8acaa04",
            "Segmento": "Customer service",
            "Inicio": "2023-04-02 09:52:47",
            "Fin": "2023-04-02 09:52:56",
            "Rechazada": false,
            "Abandonada": false,
            "Asignada": true,
            "Duración": 0.139,
            "Razón Cancelación": "queue-assigned",
            "Meta Data": "67ed331f6969ca55b8acaa02",
            "Conexiones": 1,
            "Desconexiones": 1
        }
    ]
}
```
{% endtab %}
{% endtabs %}
