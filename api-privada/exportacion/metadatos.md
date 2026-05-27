# Metadatos

## Obtener metadatos

<mark style="color:green;">`POST`</mark> `/reports/exports/extra-data`

Podrás usar este endpoint para exportar los registros de metadatos de tu cuenta.

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
        "Usuario agente",
        "Sistema operativo (nombre)",
        "Sistema operativo (version)",
        "Navegador (nombre)",
        "Navegador (version)",
        "IP",
        "Tipo IP",
        "Referido",
        "Zona horaria",
        "Idioma (code)",
        "Idioma",
        "Idioma (nombre)",
        "ISP",
        "ISP (domain)",
        "Continente (nombre)",
        "Continente (code)",
        "País",
        "País (code)",
        "Region",
        "Region (code)",
        "Ciudad",
        "Coordenadas",
        "Dispositivo",
        "Fecha",
        "Longitude",
        "Latitude",
        "GPS accuracy"
    ],
    "data": [
        {
            "Identificador": "67ed331f6969ca55b8acaa02",
            "Usuario agente": "Mozilla/5.0 (IU; OS) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36",
            "Sistema operativo (nombre)": "IU",
            "Sistema operativo (version)": "OS",
            "Navegador (nombre)": "Chrome",
            "Navegador (version)": "121.0.0.0",
            "IP": "2a4f:5656:3f6f:884e:6d20:ec33:275d:5838",
            "Tipo IP": "IPv6",
            "Referido": "https://videsk.io/",
            "Zona horaria": "America/Santiago",
            "Idioma (code)": "es",
            "Idioma": "español",
            "Idioma (nombre)": "Spanish",
            "ISP": "ENTEL CHILE S.A.",
            "ISP (domain)": "entel.cl",
            "Continente (nombre)": "South America",
            "Continente (code)": "SA",
            "País": "Chile",
            "País (code)": "CL",
            "Region": "Región Metropolitana de Santiago",
            "Region (code)": "CL-RM",
            "Ciudad": "Santiago",
            "Coordenadas": "-33.45251,-70.65273",
            "Dispositivo": "desktop",
            "Fecha": "2023-04-02 09:52:47",
            "Longitude": -70.65273,
            "Latitude": -33.45251,
            "GPS accuracy": 999999
        }
    ]
}
```
{% endtab %}
{% endtabs %}
