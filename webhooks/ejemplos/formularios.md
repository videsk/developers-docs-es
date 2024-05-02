---
description: >-
  A continuación, verás ejemplos de cómo extraer campos de un formulario o
  convertir a un nuevo formato dependiendo de tus necesidades.
---

# Formularios

Los formularios tienen una estructura fija pero con cantidad de campos variables lo que dependerá de cada formulario creado. Esta es la estructura estándar con todos los keys:

```json
{
    "name": "My form",
    "description": "My form for receive customers data",
    "fields": [
      {
        "name": "quia-eveniet-perspiciatis",
        "label": "quo dolorem quaerat?",
        "hint": "voluptatem eveniet consequatur",
        "type": "date",
        "value": "autem modi omnis",
        "options": [
          {
            "value": "Option value",
            "label": "Option label"
          }
        ],
        "colors": "#882E3F",
        "properties": {}
      }
    ]
  }
```

Habitualmente los formularios rellenados por clientes o ejecutivos usan esta estructura, por lo que existe una nomenclatura estándar para acceder a cualquier campo independiente de la key.

Las keys que contienen el formulario actualmente son: `baseForm`, `agentForm`, `submittedForm`, `contactForm`.

Si quisiera extraer u obtener el valor de un campo de un formulario individualmente, por ejemplo el nombre del cliente, debería hacer lo siguiente usando los helpers `get` y `find`.

```handlebars
{{#get 'value'}}
    {{#find @root.submittedForm}}
      {{#isEqual this.name}}customer_name{{/isEqual}}
    {{/find}}
{{/get}}
```

Esto devolvería el nombre del cliente a través el `name` como ID para filtrar en los campos del formulario usando el helper `#find` y luego usando el helper `#get` indicando que la key `value` del formulario es la que necesitamos extraer.

Esto ya que el helper `#find` busca el elemento dentro del listado de campos, y finalmente con `#get` extraemos la key específica del campo que sería `value`.
