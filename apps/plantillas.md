---
description: >-
  La URL de tu app se resuelve con Handlebars antes de cargarse. Aquí están
  todas las variables disponibles y los helpers que puedes usar.
---

# Plantillas y contexto

La `iframe.url` que defines en la app se compila con [Handlebars](https://handlebarsjs.com/) en el navegador del agente, justo antes de montar el iframe. Eso te permite inyectar datos del contexto (id de llamada, email del cliente, segmento, etc.) directamente en la URL.

```jsonc
{
  "iframe": {
    "url": "https://apps.example.com/lookup?call={{call.id}}&email={{encode form.email}}"
  }
}
```

{% hint style="info" %}
La URL se resuelve **una sola vez** al montar el iframe. Si necesitas datos que cambian durante la llamada, recíbelos por el [broker](broker.md), no por la URL.
{% endhint %}

## Helpers

Además de la sintaxis estándar de Handlebars, tienes disponibles:

| Helper | Uso | Notas |
| --- | --- | --- |
| `encode` | `{{encode user.email}}` | Aplica `encodeURIComponent`. Úsalo siempre en valores que van a query string. |
| `urlEncode` | `{{urlEncode user.email}}` | Alias de `encode`. |
| Helpers de [`@videsk/handlebars-helpers`](https://www.npmjs.com/package/@videsk/handlebars-helpers) | fechas, strings, math | Ver el README del paquete. |

La plantilla se compila con `noEscape: true`, es decir, **no** se hace HTML-escape automático. Para query strings usa `encode` explícito.

Si una variable no existe en el contexto actual, Handlebars la renderiza como string vacío (sin error).

## Variables comunes (llamadas y reuniones)

| Variable | Tipo | Descripción |
| --- | --- | --- |
| `{{user.id}}` | string | Id del agente autenticado. |
| `{{user.email}}` | string | Email del agente. |
| `{{user.firstname}}` | string | Nombre del agente (desde metadata). |
| `{{user.lastname}}` | string | Apellido del agente. |
| `{{user.<campo>}}` | mixed | Cualquier otro campo de la metadata del agente. |
| `{{account.id}}` | string | Id de la cuenta (tenant). |

## Llamadas

Disponible cuando la app se renderiza durante una llamada (cuando el agente acepta una atención de cola, se reconecta, o acepta una invitación a una llamada activa).

| Variable | Tipo | Descripción |
| --- | --- | --- |
| `{{call.id}}` | string | Id de la llamada. |
| `{{call.startedAt}}` | ISO date | Fecha de creación de la llamada. |
| `{{call.duration}}` | number | Minutos en cola (solo en reconexión). |
| `{{call.ticketId}}` | string | Id de ticket de integración, si aplica. |
| `{{segment.id}}` | string | Id del segmento. |
| `{{segment.name}}` | string | Nombre del segmento. |
| `{{branch.id}}` | string | Id de la sucursal QMS, si aplica. |
| `{{branch.label}}` | string | Etiqueta de la sucursal. |
| `{{poc.id}}` | string | Id del POC, si aplica. |
| `{{poc.label}}` | string | Etiqueta del POC. |
| `{{tags}}` | array | Etiquetas configuradas en el segmento. |
| `{{selectedTags}}` | array | Etiquetas seleccionadas en la llamada (solo en reconexión). |
| `{{extraData.<campo>}}` | mixed | Cualquier campo del payload `extraData` del widget. |
| `{{integrationData.<campo>}}` | mixed | Datos de integraciones, si aplican. |

## Reuniones

Disponible cuando la app se renderiza durante una reunión agendada.

| Variable | Tipo | Descripción |
| --- | --- | --- |
| `{{appointment.id}}` | string | Id de la cita. |
| `{{appointment.startAt}}` | ISO date | Inicio agendado. |
| `{{appointment.endAt}}` | ISO date | Fin agendado. |
| `{{appointment.scheduledFor}}` | string | Usuario/cliente para quien se agendó. |
| `{{appointment.customer}}` | object | Perfil del cliente, si está adjunto. |
| `{{service.id}}` | string | Id del servicio (calendario). |
| `{{service.name}}` | string | Nombre del servicio. |
| `{{tags}}` | array | Etiquetas configuradas en el servicio. |
| `{{selectedTags}}` | array | Etiquetas seleccionadas en la reunión. |

## Formularios: `form` y `agentForm`

Los campos de formulario se exponen como **objetos clave-valor**, indexados por el nombre que les diste al configurarlos. Eso te permite referenciar cualquier campo directamente.

### Formulario del cliente: `form`

Respuestas que el cliente final envió antes de entrar a la cola o reunión.

```
{{form.<nombreDelCampo>}}
```

### Formulario del agente: `agentForm`

Valores que llena el agente durante la atención (o que llegan pre-llenados por una integración).

```
{{agentForm.<nombreDelCampo>}}
```

### Iteración por todos los campos

Si necesitas recorrer todos los campos del formulario (por ejemplo, para construir un query string dinámico), también están disponibles como arrays:

```handlebars
{{#each formFields}}{{name}}={{encode value}}&{{/each}}
{{#each agentFormFields}}{{name}}={{encode value}}&{{/each}}
```

Cada item del array tiene como mínimo: `name`, `value`, `type`.

## Ejemplos

```handlebars
# Buscar un contacto en tu CRM por el email del formulario del cliente
https://crm.example.com/contacts?email={{encode form.email}}

# Pasar un RUT (cédula) escrito por el agente a un sistema externo
https://api.example.com/validate?rut={{encode agentForm.rut}}&call={{call.id}}

# Combinar varios bloques
https://apps.example.com/case?customer={{encode form.email}}&agent={{user.id}}&segment={{encode segment.name}}
```
