---
description: Descubre como realizar la integración con kioskos físicos
---

# Kioscos

Disponemos de recursos para que puedas utilizar Videsk en kioscos bajo diferentes ambientes.

{% content-ref url="modo-kiosko.md" %}
[modo-kiosko.md](modo-kiosko.md)
{% endcontent-ref %}

## Arquitectura

Para el caso de los kioscos debes considerar que dependiendo de tu necesidad podrías requerir ajustar la forma de generar llamadas o agendamientos.

## Sin segmentación

```mermaid
graph TD
    %% Kioskos
    K1[🖥️ Kiosco 1<br/>Cliente inicia videollamada]
    K2[🖥️ Kiosco 2<br/>Cliente inicia videollamada]
    K3[🖥️ Kiosco 3<br/>Cliente inicia videollamada]
    K4[🖥️ Kiosco 4<br/>Cliente inicia videollamada]
    
    %% Sistema Videsk
    V[🔄 VIDESK<br/>Sistema de enrutamiento<br/>automático]
    
    %% Pool de ejecutivos
    E1[👤 Ejecutivo 1<br/>Disponible]
    E2[👤 Ejecutivo 2<br/>Ocupado]
    E3[👤 Ejecutivo 3<br/>Disponible]
    E4[👤 Ejecutivo 4<br/>Disponible]
    E5[👤 Ejecutivo 5<br/>Ocupado]
    
    %% Conexiones desde kioskos a Videsk
    K1 --> V
    K2 --> V
    K3 --> V
    K4 --> V
    
    %% Conexiones desde Videsk a ejecutivos
    V --> E1
    V --> E3
    V --> E4
    
    %% Ejecutivos ocupados (líneas punteadas)
    V -.-> E2
    V -.-> E5
    
    %% Estilos
    classDef kiosko fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    classDef videsk fill:#f3e5f5,stroke:#7b1fa2,stroke-width:3px
    classDef disponible fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef ocupado fill:#ffebee,stroke:#c62828,stroke-width:2px
    
    class K1,K2,K3,K4 kiosko
    class V videsk
    class E1,E3,E4 disponible
    class E2,E5 ocupado
    
    %% Notas explicativas
    subgraph Pool["🏢 Pool de Ejecutivos"]
        E1
        E2
        E3
        E4
        E5
    end
    
    subgraph Kioskos["📍 Ubicaciones con Kioskos"]
        K1
        K2
        K3
        K4
    end
```

En el caso de kioscos sin realizar segmentación por ubicación o propósito específico simplemente deberás usar nuestros widgets, SDKs o APIs para generar las llamadas o agendamientos, Videsk se encargará de derivar a quien corresponda.

## Con segmentación

```mermaid
graph TD
    %% Tótems con ID de segmento
    T1[🖥️ Kiosco 1<br/>ID: SEG-A<br/>Cliente inicia videollamada]
    T2[🖥️ Kiosco 2<br/>ID: SEG-B<br/>Cliente inicia videollamada]
    T3[🖥️ Kiosco 3<br/>ID: SEG-C<br/>Cliente inicia videollamada]
    
    %% Sistema Videsk con lógica de enrutamiento
    V[🔄 VIDESK<br/>Sistema de enrutamiento<br/>por segmento<br/>Analiza ID en el tótem]
    
    %% Pools de ejecutivos por segmento
    subgraph PoolA["🏢 Pool Segmento A<br/>Ejecutivos Premium"]
        EA1[👤 Ejecutivo A1<br/>Disponible]
        EA2[👤 Ejecutivo A2<br/>Ocupado]
    end
    
    subgraph PoolB["🏢 Pool Segmento B<br/>Ejecutivos Estándar"]
        EB1[👤 Ejecutivo B1<br/>Disponible]
        EB2[👤 Ejecutivo B2<br/>Ocupado]
    end
    
    subgraph PoolC["🏢 Pool Segmento C<br/>Ejecutivos Básicos"]
        EC1[👤 Ejecutivo C1<br/>Disponible]
        EC2[👤 Ejecutivo C2<br/>Disponible]
    end
    
    %% Conexiones desde tótems a Videsk
    T1 --> V
    T2 --> V
    T3 --> V
    
    %% Enrutamiento por segmento
    V -->|ID: SEG-A| EA1
    V -.->|ID: SEG-A| EA2
    
    V -->|ID: SEG-B| EB1
    V -.->|ID: SEG-B| EB2
    
    V -->|ID: SEG-C| EC1
    V -->|ID: SEG-C| EC2
    
    %% Estilos
    classDef totemA fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef totemB fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef totemC fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef videsk fill:#e8f5e8,stroke:#388e3c,stroke-width:3px
    classDef disponible fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef ocupado fill:#ffebee,stroke:#c62828,stroke-width:2px
    classDef poolA fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef poolB fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef poolC fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    
    class T1 totemA
    class T2 totemB
    class T3 totemC
    class V videsk
    class EA1,EB1,EC1,EC2 disponible
    class EA2,EB2 ocupado
    class PoolA poolA
    class PoolB poolB
    class PoolC poolC
```

Para estos casos que requieren una clara segmentación ya sea por tipo de cliente, productos, servicios o ubicación geográfica, deberás asignar los IDs de los segmentos correspondientes en cada kiosco, de manera que al momento de realizar la llamada se identifique el origen. Para realizar esto tienes varias maneras dependiendo de las capacidades y formas de integración de tus kioscos:

{% hint style="info" %}
Recuerda que puedes obtener manualmente los IDs de segmento y calendarios desde el dashboard, también usando nuestra [Rest API](broken-reference).
{% endhint %}

### Widgets

Si estás usando nuestros widgets en tus kioscos, basta con usar el modelo de diferenciación por URL, descrita a continuación:

{% content-ref url="../../widgets/url-triggers.md" %}
[url-triggers.md](../../widgets/url-triggers.md)
{% endcontent-ref %}

### SDKs y Rest API

Si estás usando nuestros SDKs y/o Rest API en tus kioscos, tendrás que obtener el ID de segmento ya sea manualmente desde nuestro dashboard o bien programáticamente con el SDK ([Phone](../../sdks/phone/) o [Calendar](../../sdks/calendario/)) o vía [Rest API](broken-reference). Por lo tanto los pasos son:

1. Obtener ID segmento(s) o calendario(s)
2. Almacenar vía URL, localStorage, etc. **La forma que obtengan y guardes estos IDs dependerá de tu elección técnica**.
3. Usar el ID de segmento o calendario a través de nuestros SDKs o Rest API.

{% hint style="info" %}
Recuerda que la manera de almacenar los IDs dependerá de tu decisión técnica.
{% endhint %}

#### Ejemplo de almacenamiento/obtención:

{% hint style="warning" %}
Si necesitas obtener ID dinámicos, deberás diseñar tu propia solución donde recomendamos utilizar nuestra Rest API.
{% endhint %}

{% code lineNumbers="true" %}
```javascript
class Storage {
  
  static storageKey = 'kiosk-id';
  
  static get fromWindow() {
    return window[this.storageKey];
  }
  
  static get fromUrl() {
    return new URLSearchParams(window.location.search).get(this.storageKey);
  }
  
  static save(id) {
    localStorage.setItem(this.storageKey, id);
  }
  
  static get id() {
    return localStorage.getItem(this.storageKey) || this.fromUrl || this.fromWindow;
  }
  
}

Storage.id // Obtener ID de segmento automáticamente por storage, URL y window
Storage.save(id) // Almancenar en storage local del navegador
```
{% endcode %}
