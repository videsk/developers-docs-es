---
description: Te explicamos porqué es obligatorio contar un SSL válido en tu sitio web.
---

# 🔐 SSL

**Secure Sockets Layer** es un protocolo importante para aumentar la seguridad y autenticación de datos en el internet. A causa de los movimientos como [Encrypt All The Things](https://encryptallthethings.net/) y el impulso de Google para la adopción más generalizada de SSL, por lo que ha sido un tema popular.

Además de lo anterior, existen ciertas tecnologías, como las que utiliza Videsk que requieren que exista de manera obligatoria un SSL válido, con el objetivo de garantizar la seguridad del transporte de datos entre tus clientes y tu equipo.

## ¿Porqué necesito uno?

Videsk utiliza tecnología en tiempo real, una de ellas es WebRTC que requiere de conexiones seguras mediante tu certificado SSL, asegurando que la conexión entre tu cliente y con alguien de tu equipo sea 100% cifrada evitando fugas de datos ya sea de video, audio, chat, archivos, etc.

{% hint style="warning" %}
Recuerda, **no es opcional** contar con un certificado SSL.
{% endhint %}

## ¿Que sucede si caduca mi SSL?

Esto es un grave problema, ya que la mayoría de tus clientes no podrán ingresar a tu sitio web debido a un mensaje del navegador indicándoles este problema.

Te sugerimos rápidamente adquirir uno nuevo ya sea de pago o gratuito.

{% hint style="info" %}
La forma de escoger un certificado de pago o gratuito dependerá de las necesidades y características de tu negocio. La mayor parte de los sitios web solo requieren un certificado gratuito.
{% endhint %}

## ¿Es compatible con SSL wildcard, multidominio, EV, etc.?

Sí. Lo único relevante es que ese SSL, sea válido para el dominio donde esté instalado, que esté vigente y te asegures que haya sido emitido de forma correcta por un proveedor reconocido.

## ¿Puedo hacer pruebas en local o localhost sin SSL?

Sí, pero deberás utilizar tu IP local o bien `127.0.0.1` ya que `localhost` está reservado para pruebas locales de nuestro equipo de desarrollo. Además, dependiendo de tu navegador deberás forzar `https://` al inicio de la URL y luego haz clic en Avanzado y continuar.
