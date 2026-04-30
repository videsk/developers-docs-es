---
description: >-
  Las apps permiten incrustar una interfaz web propia dentro de la consola de
  agente de Videsk durante una llamada o reunión.
---

# Introducción

Una **app** (también llamada _extension_) es una página web tuya que Videsk renderiza dentro de la consola del agente, normalmente al lado del panel de llamada. Te permite mostrar información contextual (CRM, ticketera, formularios internos), automatizar acciones del agente o llevar el flujo de tu propio backend al puesto de trabajo, sin que el agente cambie de pestaña.

## Cómo funciona, en una vista

```
┌──────────────────── Consola Videsk ────────────────────┐
│                                                        │
│  Panel de llamada      ┌────────── App ────────────┐   │
│  ─ Estado              │                           │   │
│  ─ Cliente             │   tu web embebida         │   │
│  ─ Acciones            │   (https://tu-app.com)    │   │
│                        │                           │   │
│                        └───────────────────────────┘   │
└────────────────────────────────────────────────────────┘
```

Cuando el agente acepta una llamada o reunión, Videsk:

1. Resuelve la URL de tu app sustituyendo variables del contexto (Handlebars).
2. Monta tu web en un `<iframe>` con un `sandbox` y un `allow` predefinidos.
3. Te envía el contexto inicial (datos del agente, segmento, llamada, formulario) por `postMessage` mediante el **broker**.
4. Tu app puede responder con eventos: emitir datos al host, pedir un resize de altura, etc.

## Lo que necesitas saber para construir una app

Estas son las cuatro piezas. Léelas en orden la primera vez:

1. [**Configuración**](configuracion.md): qué campos llenas en consola al registrar la app.
2. [**Plantillas y contexto**](plantillas.md): qué variables puedes inyectar en la URL antes de cargarla.
3. [**Broker (postMessage)**](broker.md): el protocolo para hablar con la consola en tiempo real.
4. [**Ejemplos**](ejemplos/): código copy/paste para los casos más comunes.

## Tipos de app y dónde se renderizan

Hoy se documenta el tipo **iframe**, en el que tu app es una URL servida por ti. Existen tres ubicaciones (_placements_) donde puede aparecer:

| Placement | Dónde se ve | Cuándo conviene |
| --- | --- | --- |
| `call-panel` | Inline dentro del panel de la llamada | Información compacta que el agente debe ver de un vistazo. |
| `sidebar` | Drawer lateral (ancho configurable) | Apps con más UI, búsquedas, formularios. |
| `standalone` | Se abre en una pestaña nueva (`window.open`) | Herramientas que necesitan toda la pantalla o no encajan dentro de la consola. |

{% hint style="info" %}
Las apps `standalone` no usan el broker: la URL se resuelve y se abre en una pestaña nueva, sin canal `postMessage`. El resto de esta documentación aplica a `call-panel` y `sidebar`.
{% endhint %}

## Ciclo de vida

1. **Mount**: el agente entra a una llamada/reunión y abre tu app. La URL se resuelve **una sola vez** con el contexto disponible en ese momento.
2. **Init**: cuando el `iframe` termina de cargar, el host envía un mensaje `videsk:init` con el contexto al `contentWindow` de tu app.
3. **Operación**: tu app y el host pueden intercambiar mensajes vía broker (resize, eventos de negocio, etc.).
4. **Reload manual**: el agente puede recargar la app desde el botón del header. Esto vuelve a resolver la URL con el contexto actualizado.
5. **Unmount**: al cerrar la llamada/reunión, o si la app deja de aplicar al segmento, el `iframe` se destruye.

{% hint style="warning" %}
La URL **no** se vuelve a resolver automáticamente cuando el contexto cambia (por ejemplo, cuando el agente llena un campo del formulario después del mount). Si necesitas datos que cambian en vivo, recíbelos por el broker en lugar de codificarlos en la URL.
{% endhint %}
