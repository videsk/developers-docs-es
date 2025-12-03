---
description: Detalles de como crear salas a través de nuestra VPaaS API.
---

# Rooms API

{% embed url="https://docs.videsk.io/" fullWidth="false" %}

## Autorización

Todos los endpoints descritos a continuación utilizan la cabecera `Authorization` con esquema Bearer.&#x20;

Un API token lo puedes obtener desde nuestro dashboard. Este deberá ser de tipo `api-token` el cual es el único permitido para VPaaS.

{% hint style="info" %}
Si estás en ambiente de desarrollo, te recomendamos crear un token sin lista blanca de IPs; esto evitará problemas de bloqueos por IP dinámica.
{% endhint %}

Obtén el tuyo aquí, [inciar sesión](https://app.videsk.io/).

***

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms" method="get" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms" method="post" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms/{roomId}" method="get" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms/{roomId}" method="delete" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms/{roomId}" method="patch" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms/{roomId}/join" method="post" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52c68e3965a519f6eb2f93d9d5484b4c6160fa9ef8609fb95c97d92c0f78ce2b.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251203%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251203T005037Z&X-Amz-Expires=172800&X-Amz-Signature=f1cb474d900d69f80c6424f7b2d8c17770c14de8c3d326235f3a2b90fab7aa51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
