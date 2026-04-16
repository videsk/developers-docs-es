---
description: >-
  Las extensiones permiten embeber aplicaciones externas (iframe o web
  components) dentro de los productos de Videsk, configurables por segmento
  y servicio (calendario).
---

# Extensiones

Las extensiones son aplicaciones embebidas que se renderizan dentro de la Consola de Videsk. Pueden ser de dos tipos:

| Tipo | Descripcion | Aislamiento |
| --- | --- | --- |
| **iframe** | Carga una URL externa en un iframe con sandbox | Completo (proceso separado) |
| **web-component** | Carga un modulo JS que define un Custom Element | Parcial (mismo contexto) |

## Caracteristicas

- **Asociables por entidad**: cada extension se asocia desde el segmento o servicio (calendario) que la necesita, mediante su campo `extensions[]`. Esto permite configuraciones flexibles por equipo o tipo de calendario.
- **Placement flexible**: pueden renderizarse en el panel de llamada (`call-panel`), la barra lateral (`sidebar`) o como pagina independiente (`standalone`).
- **Permisos controlados**: los iframes reciben atributos `sandbox` y `allow` validados contra una lista blanca del backend.
- **Contexto de host**: la extension recibe datos del contexto actual (usuario, segmento, llamada, contacto) segun los scopes configurados.

## Flujo de configuracion

1. Crear la extension via `POST /extensions` (define que es: nombre, tipo, URL, permisos).
2. Asociar la extension al segmento o servicio via `PATCH /segments/:id` o `PATCH /services/:id` agregando el ID al campo `extensions[]`.

## Tipos de extension

### Iframe

Ideal para aplicaciones que necesitan aislamiento completo. La pagina embebida corre en un proceso separado del navegador, con permisos controlados por `sandbox` y `allow`.

{% content-ref url="iframe.md" %}
[iframe.md](iframe.md)
{% endcontent-ref %}

### Web Component

Ideal para integraciones ligeras que necesitan acceso directo al DOM del host. El modulo JS registra un Custom Element que se monta directamente en la consola.

{% content-ref url="web-components.md" %}
[web-components.md](web-components.md)
{% endcontent-ref %}

## Protocolo de comunicacion

Ambos tipos de extension se comunican con el host mediante un protocolo basado en `postMessage` (iframes) o `CustomEvent` (web components).

{% content-ref url="postmessage.md" %}
[postmessage.md](postmessage.md)
{% endcontent-ref %}
