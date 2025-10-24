# Qué es?

VPaaS (Video Platform as a Service) es la solución de infraestructura de video empresarial de Videsk que permite a los desarrolladores integrar capacidades de comunicación por video de alta calidad y escalables directamente en sus aplicaciones. Construido sobre tecnología WebRTC, VPaaS proporciona la infraestructura de video fundamental sin la complejidad de gestionar servidores de señalización, servidores TURN/STUN o enrutamiento de medios.

***

## Para desarrolladores

* **Integración Rápida**: Video funcionando en minutos, no meses
* **Cero Gestión de Infraestructura**: Enfócate en tu producto core mientras nosotros manejamos la complejidad del video
* **Listo para Producción**: Infraestructura probada en batalla que escala automáticamente
* **Agnóstico de Framework**: Funciona con cualquier stack tecnológico web

## Para empresas

* **Costo-Efectivo**: Paga solo por lo que usas con precios transparentes por minuto
* **Alcance Global**: Infraestructura distribuida asegura baja latencia mundialmente
* **Seguridad Empresarial**: Encriptación end-to-end y arquitectura lista para compliance
* **Escalado Predecible**: Escalado automático desde 1 hasta 1000+ participantes concurrentes

***

## Arquitectura Técnica

#### Componentes Core

**Gestión de Salas**

* Creación dinámica de salas y gestión del ciclo de vida
* Políticas flexibles de expiración y controles de acceso
* Autorización y seguimiento de participantes en tiempo real

**Infraestructura de Señalización**

* Servidores de señalización WebRTC de alto rendimiento
* Failover automático y balanceo de carga
* Red edge global para calidad óptima de conexión

**Enrutamiento de Medios**

* Selección inteligente de servidores TURN basada en geografía
* Selección adaptativa de bitrate y codec
* Optimización de condiciones de red

#### Diseño API-First

* [API RESTful](rooms-api.md) para gestión y configuración de salas
* Autenticación basada en JWT con permisos granulares
* Seguimiento de eventos en tiempo real y analytics
* Sistema integral de webhooks para integración

***

## Casos de Uso

#### Plataformas de Soporte al Cliente

Transforma el soporte basado en texto en conversaciones cara a cara con salas de video embebidas que se lanzan instantáneamente desde tickets de soporte.

#### Aplicaciones de Telemedicina

Habilita consultas de video seguras y compatibles con funciones como salas de espera, grabación de sesiones y controles de privacidad del paciente.

#### Soluciones EdTech

Potencia aulas virtuales, sesiones de tutoría 1:1 y experiencias de aprendizaje interactivo con infraestructura de video confiable.

#### Mejora de Productos SaaS

Agrega funciones de video colaborativo a productos existentes - desde revisiones de diseño hasta standups de equipo - sin reconstruir tu arquitectura.

#### Apps de Comunicación Personalizadas

Construye aplicaciones de video especializadas para industrias o flujos de trabajo específicos mientras aprovechas infraestructura probada.

***

## Integración zero-headache

Patrón de integración simple en cuatro pasos:

{% code lineNumbers="true" %}
```javascript
// 1. Crear una sala via API
const room = await fetch('/vpaas/rooms', {
  method: 'POST',
  headers: { 'Authorization': 'Bearer tu-api-token' },
  body: JSON.stringify({
    name: 'Sesión de Soporte al Cliente',
    externalId: 'ticket-soporte-12345'
  })
});

// 2. Unir participantes con tokens generados
const joinResponse = await fetch(`/vpaas/rooms/${room.id}/join`, {
  method: 'POST',
  headers: { 'Authorization': 'Bearer tu-api-token' }
});

// 3. Usar access token en tu cliente de video
const { accessToken } = joinResponse.json();

// 4. Usar SDK Browser
const webrtc = new WebRTC();
await webrtc.create(accessToken);
```
{% endcode %}

#### Ciclo de Vida Flexible de Salas

* **Creación Bajo Demanda**: Salas creadas cuando se necesitan, limpieza automática
* **Sesiones Programadas**: Pre-crear salas con horas específicas de inicio/fin
* **Salas Persistentes**: Salas de larga duración para colaboración continua
* **Mapeo de ID Externos**: Vincular salas a tus entidades de negocio existentes

***

## Modelo de Precios

**Precios Transparentes Basados en Uso**

* Cobro por minuto-participante de uso activo de video
* Sin tarifas de configuración o mínimos mensuales
* Descuentos por volumen disponibles para uso empresarial
* Seguimiento y reporte de uso en tiempo real

**Funciones Incluidas**

* Creación y gestión ilimitada de salas
* Infraestructura global TURN/STUN
* Analytics y monitoreo básico
* Soporte estándar y documentación

***

## Seguridad y Compliance

#### Seguridad de Nivel Empresarial

* Autenticación basada en JWT con expiración configurable
* Restricciones de acceso basadas en IP y geofencing
* Encriptación WebRTC end-to-end
* Infraestructura compatible con SOC 2 Type II

#### Controles de Privacidad

* Ningún contenido de video/audio almacenado en servidores Videsk
* Controles de permisos granulares por integración
* Marcos de compliance GDPR y HIPAA disponibles
* Logs de auditoría completos para todas las interacciones API

***

## Por Qué elegir nuestro VPaaS

**Tecnología probada: construida sobre la misma infraestructura que potencia la plataforma de comunicación empresarial de Videsk, manejando millones de minutos de video mensualmente.**

**Experiencia de Desarrollador**: Diseñada por desarrolladores, para desarrolladores. APIs limpias, excelente documentación y comportamiento predecible.

**Continuidad de Negocio:** Elimina el video como punto único de falla en la arquitectura de tu aplicación con nuestro SLA de 99,9% de disponibilidad.

**A Prueba de Futuro**: Actualizaciones regulares con nuevas funciones WebRTC y optimizaciones, asegurando que tu integración se mantenga actualizada con estándares web.
