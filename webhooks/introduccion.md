---
description: >-
  Aprenderás de los conceptos básicos y avanzados sobre nuestra tecnología
  basada en Webhooks como integración.
---

# 👓 Introducción

Webhooks son eventos en una plataforma que permiten ejecutar una acción cuando estos suceden y enviar datos a terceros. Por ejemplo, cuando una nueva llamada sucede dentro de Videsk se pueden enviar esos datos a otras plataformas para sincronizarla.

Es decir, estas acciones son peticiones HTTP que se ejecutarán cuando ciertos eventos determinados ocurran y serán enviados a una Rest API que tu determinas.

Si bien, esto permite que las plataformas sean integrables con terceros que posean una Rest API, en su mayoría requieren un paso intermedio que habitualmente conlleva invertir tiempo y dinero. Este paso intermedio lo denominamos `mutador/traductor`. Apliquemos un ejemplo para entenderlo de mejor manera.

## ¿Cómo funcionan las plataformas hoy?

Si queremos integrarnos con la plataforma [Airtable](https://airtable.com) desde nuestra plataforma SuperCall _(nombre ficticio)_, deberemos entender qué y cómo recibe los datos la Rest API de [Airtable](https://airtable.com).

[Airtable](https://airtable.com) nos indica que debemos enviar los datos a su Rest API, bajo la siguiente estructura:

```json
{
    "fields": {
        "Nombre": "John",
        "Apellido": "Doe",
        "Email": "john.doe@example.com"
    }
}
```

Pero nuestra plataforma SuperCall _(nombre ficticio)_, envía los datos en esta otra estructura:

```java
[
    { name: "Nombre", value: "John" },
    { name: "Apellido", value: "Doe" },
    { name: "Email", value: "john.doe@example.com" }
]
```

**No son iguales! Y esto es un problema!** Ya que SuperCall _(nombre ficticio)_ nos ofrece enviar los datos, pero en su propia estructura, no como Airtable debe recibirlos! En otras palabras, **ambas plataformas hablan en distintos idiomas**.

Aquí es donde surgen dos soluciones:

1. Que SuperCall _(nombre ficticio)_ se integre de forma nativa con Airtable. (Pero dependerá del tiempo del equipo de SuperCall para hacer esto) 🥱😴
2. Crear un servidor intermedio que pueda mutar/traducir la estructura y enviarla de forma correcta. 💵🥵

Estas dos soluciones en la vida real, toman mucho tiempo y dinero, y habitualmente se descartan fallando con las integraciones en corto plazo. 😫

{% hint style="info" %}
En su mayoría Webhooks tienen como función enviar datos a un destinatario, pero **no asegurar** que el destinatario entienda esos datos y estructura.
{% endhint %}

**Pero, aquí es donde Videsk ha innovado!** :tada:

## Webhooks como integraciones 😎

Si bien Webhooks o intercambio de datos basados en eventos existe hace tiempo, nos hemos centrado en el dolor más grande para muchos negocios. La interoperabilidad de plataformas sin mayor esfuerzo.

Para ello, **hemos creado un mutador y traductor que permite que nuestros clientes puedan mutar y traducir los datos, y sean enviados en el formato y estructura que la plataforma destinataria debería recibir.**&#x20;

Es así, que Videsk es compatible con prácticamente cualquier plataforma que posea una Rest API, SOAP, GraphQL o en su defecto que logre recepcionar peticiones HTTP.

Utilizando el ejemplo anterior de Airtable, es así como funcionaría:

```handlebars
⏬ Formato que espera recibir Airtable
{
    "fields": {
        "Nombre": "John",
        "Apellido": "Doe",
        "Email": "john.doe@example.com"
    }
}
-----------------------------------------------
⏬ Formato original Videsk
[
    { name: "Nombre", value: "John" },
    { name: "Apellido", value: "Doe" },
    { name: "Email", value: "john.doe@example.com" }
]

⏬ Formato Webhooks Videsk (Aquí ocurre la magia) <<<<<<
{
    "fields": {{#object fields}}name,value{{/object}}
}
------------------------------------------------
⏬ Formato enviado a Airtable
{
    "fields": {
        "Nombre": "John",
        "Apellido": "Doe",
        "Email": "john.doe@example.com"
    }
}
```

Lo que puedes visualizar es que desde una estructura complemente diferente, utilizando nuestra sintaxis de mutación y traducción, puedes lograr enviar los datos como Airtable o cualquier otra plataforma lo requiera.

Es decir, que el cuerpo de la petición (`body`) formato original de Videsk, será mutado y traducido basado en la plantilla de datos que tú escribas.

**Y es así, de forma sencilla sabrás que podrás prácticamente integrar Videsk con lo que sea!**
