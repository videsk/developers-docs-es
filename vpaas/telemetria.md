---
description: Conoce nuestra API de telemetría y estadísticas.
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Telemetría

Obtén el análisis de calidad WebRTC de una sala (sesión) bajo demanda: un reporte determinístico con puntajes y recomendaciones, un _snapshot_ en vivo, o el resumen persistido de la sesión.

### Autorización

Todos los endpoints descritos a continuación utilizan la cabecera `Authorization` con esquema Bearer.

Un API token lo puedes obtener desde nuestro dashboard. Este deberá ser de tipo `api-token`, el cual es el único permitido para VPaaS.

{% hint style="info" %}
Si estás en ambiente de desarrollo, te recomendamos crear un token sin lista blanca de IPs; esto evitará problemas de bloqueos por IP dinámica.
{% endhint %}

***

### Vistas disponibles (`view`)

| `report` _(default)_ | Análisis completo de la sesión: puntaje de calidad, métricas clave, patrones detectados y recomendaciones accionables.         | Cacheado    |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| `snapshot`           | Rollup calculado en tiempo real desde la telemetría cruda. Útil mientras la sesión sigue activa ("qué ha pasado hasta ahora"). | No persiste |
| `summary`            | Rollup persistido de la sesión (por peer y por minuto). Disponible una vez que la sesión fue compilada.                        | Persistido  |

***

{% openapi-operation spec="videsk-docs-api" path="/vpaas/rooms/{roomId}/stats" method="get" %}
[OpenAPI videsk-docs-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/c60064c655cc68ef7eac554ec7250aa2e660b568a6c890dbd7be138f2f6e0d66.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260625T081142Z&X-Amz-Expires=172800&X-Amz-Signature=eeb1edd48d14f4d384246a4525eba757c12299344bce48ad32e2a2340a9d7e6e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
