---
description: Te explicamos como usar nuestro SDK de Calendario
---

# 📅 Calendario

Con este SDK podrás embeber y diseñar de forma programática calendarios para agendar, sin necesidad de preocuparte por las conexiones, parámetros, excepciones, etc.

Es decir, hemos creado este "enchufe" para llegar y usar de forma sencilla y una estructura de rápido aprendizaje, pero sin dejar de lado la flexibilidad y poder de nuestra API.

{% hint style="info" %}
Este SDK no provee interfaz, es decir, no hay código HTML, por lo que deberás manejar tu propia interfaz, ya sea en HTML puro, Javascript o con frameworks como Vue, React, Angular, Svelte, etc.
{% endhint %}

## Instalación

Para comenzar deberás instalar nuestro recurso en tu sitio web o aplicación móvil. Tienes las siguientes alternativas.

{% tabs %}
{% tab title="HTML" %}
```html
<script src="https://cdn.videsk.io/sdk/calendar.min.js"></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement('script');
script.src = "https://cdn.videsk.io/sdk/calendar.min.js";
document.body.appendChild('body'); // O reemplaza con el nodo DOM que desees
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
No almacenes el contenido del script en tu servidor, **esto infringe nuestros términos de uso**.
{% endhint %}

{% hint style="danger" %}
Por seguridad y calidad de servicio tenemos un límite de peticiones por segundo por IP/Token, que consta de 20 peticiones en 1 segundo. Evita superar este límite, ya que nuestra Rest API bloqueará las peticiones de tus clientes.
{% endhint %}

## Instanciar

Lo primero que debes hacer es instanciar una clase `Calendar`. El primer argumento corresponden al token de integración que obtienes de tu cuenta.

```javascript
const calendar = new Calendar(token);
```

Posteriormente puedes acceder a sus métodos y propiedades.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Métodos</strong></td><td>Conoce cómo usar los métodos de Calendar SDK.</td><td></td><td><a href="metodos.md">metodos.md</a></td><td></td></tr><tr><td><strong>Propiedades</strong></td><td>Conoce cuáles son las propiedades de Calendar SDK.</td><td></td><td><a href="propiedades.md">propiedades.md</a></td><td></td></tr></tbody></table>

## Flujos

A continuación, puedes observar los dos tipos de flujos existentes, agendamiento y modificación. Te sugerimos leer con detención de esta manera tendrás una visión global de cada uno de los pasos involucrados en el agendamiento.

### Agendamiento

Este flujo corresponde al inicial, cuando un cliente desea agendar una reunión por primera vez.

{% hint style="warning" %}
El envío de recordatorios puede suceder hasta 4 veces en diferentes periodos según la configuración realizada, ambas para cliente y agente.
{% endhint %}

{% hint style="info" %}
Los posibles errores que pueden surgir es agendar unos segundos antes de la hora seleccionada, por ejemplo: Agendar para las 14:05:00 a las 14:04:59.



También es posible que se niege el agendamiento si alguien más ha toma la hora al mismo tiempo, solo si hay 1 agente u hora disponible.
{% endhint %}

```mermaid
flowchart LR
    A["Listado de servicios\n(calendarios)"]
    B["Listado de agentes\npor servicio"]
    C1["Cargar días del mes"]
    C2["Cargar horas del día"]
    D["Formulario de datos"]
    E["Confirmación"]
    F1["Envío correo\nconfirmación-cliente"]
    F2["Envío correo\nconfirmación-agente"]
    G1["Envío correo\nrecordatorio-cliente"]
    G2["Envío correo\nrecordatorio-agente"]

    A --> B
    B -->|"Selección manual"| C1
    B -->|"Selección manual"| C2
    C1 --> D
    C2 --> D
    D -->|"No error"| E
    D -->|"Si error"| A
    E -.-> F1
    E -.-> F2
    F1 -.->|"Previo reunión"| G1
    F2 -.-> G2
    G1 -.-> E
    G2 -.-> E

    A -->|"Selección inteligente"| C2
    D -->|"Error disponibilidad"| C2
```



### Modificación

Este flujo corresponde al momento en que un cliente desea cancelar o reagendar una cita previamente solicitada.

{% hint style="warning" %}
Este flujo siempre se debe realizar con los tokens enviados por correo electrónico u otro medio seleccionado. Por seguridad no existen PINs, claves o búsqueda por correo para efectuar modificaciones.
{% endhint %}

```mermaid
flowchart LR
    A1["Reagendar"]
    A2["Cancelar"]
    B1["Cargar días del mes"]
    B2["Cargar horas del día"]
    C["Confirmación"]
    D1["Envío correo\nconfirmación-cliente"]
    D2["Envío correo\nconfirmación-agente"]
    E1["Envío correo\ncancelación-cliente"]
    E2["Envío correo\ncancelación-agente"]
    F1["Envío correo\nrecordatorio-cliente"]
    F2["Envío correo\nrecordatorio-agente"]

    A1 --> B1
    A1 --> B2
    B1 --> C
    B2 --> C
    A2 --> E1
    A2 --> E2
    C -.-> D1
    C -.-> D2
    D1 -.->|"Previo reunión"| F1
    D2 -.-> F2
    F1 -.-> C
    F2 -.-> C
```

