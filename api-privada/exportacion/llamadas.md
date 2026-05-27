# Llamadas

## Obtener llamadas

<mark style="color:green;">`POST`</mark> `/reports/exports/calls`

Podrás usar este endpoint para exportar las llamadas de tu cuenta.

**Headers**

| Name         | Value                |
| ------------ | -------------------- |
| Content-Type | `application/json`   |
| X-API-Token  | `Bearer <api-token>` |

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
        "Agente",
        "Inicio",
        "Fin",
        "Duración",
        "Encuesta",
        "Meta Data",
        "Cliente cortó",
        "Transferido a agente",
        "Transferido a segmento",
        "Fila",
        "ID Encuesta",
        "ID formulario agente",
        "ID formulario cliente",
        "After Call Work (ACW)",
        "Effective Duration",
        "Etiquetas",
        "Comentarios"
    ],
    "data": [
        {
            "Identificador": "67ed33276969ca55b8acacce",
            "Segmento": "Customer service",
            "Agente": "john@videsk.io",
            "Inicio": "2023-04-02 09:52:55",
            "Fin": "2023-04-02 10:14:14",
            "Duración": 21.322,
            "Meta Data": "67ed331f6969ca55b8acaa02",
            "Cliente cortó": "2023-04-02 10:14:14",
            "Transferido a agente": false,
            "Transferido a segmento": false,
            "Fila": "67ed331f6969ca55b8acaa04",
            "After Call Work (ACW)": 0,
            "Effective Duration": 21.321383333333333,
            "Etiquetas": [
                "6266b4a541ba018109df4633",
                "63237387e78f41135aeefc21"
            ],
            "Comentarios": "67ed33e1cacce048288f937f"
        }
    ]
}
```
{% endtab %}
{% endtabs %}
