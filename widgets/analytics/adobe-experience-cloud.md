---
cover: ../../.gitbook/assets/Adobe-Experience-Cloud-logo.jpg
coverY: 14.035092002467106
---

# Adobe Experience Cloud

## Compatibilidad

<table><thead><tr><th width="381.77783203125">Nombre</th><th data-type="checkbox">Compatibilidad</th></tr></thead><tbody><tr><td>Adobe Experience Platform (Web SDK)</td><td>true</td></tr><tr><td>Adobe Launch (Experience Platform Tags)</td><td>true</td></tr><tr><td>Adobe Analytics (AppMeasurement)</td><td>true</td></tr><tr><td>Adobe DTM (Dynamic Tag Manager)</td><td>true</td></tr><tr><td>Adobe Target</td><td>false</td></tr><tr><td>Adobe Audience Manager</td><td>false</td></tr><tr><td>Adobe Campaign</td><td>false</td></tr></tbody></table>

{% hint style="success" %}
Las **incompatibilidades** hacen referencia a integración nativa, la cual puedes [suplir usando la propia API del widget](../api/).
{% endhint %}

## Configuración

El widget de Videsk detecta automáticamente su implementación de Adobe Experience Cloud y envía eventos de interacción sin configuración adicional en la mayoría de los casos. Sin embargo, para recibir y procesar estos eventos correctamente en sus reportes, puede ser necesaria una configuración mínima.

Puedes encontrar los eventos emitidos por nuestro widget acá:

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

### Implementación por versión

<table><thead><tr><th width="232.5555419921875">Implementación Adobe</th><th width="201">Requiere Configuración</th><th>Estado</th><th>Tiempo Setup</th></tr></thead><tbody><tr><td><strong>Adobe Analytics Directo (s_code)</strong></td><td>❌ No</td><td>🟢 Automático</td><td>0 minutos</td></tr><tr><td><strong>Adobe Launch/Experience Platform Tags</strong></td><td>⚠️ Básica</td><td>🟡 Manual</td><td>15-30 minutos</td></tr><tr><td><strong>Adobe Experience Platform Web SDK</strong></td><td>✅ Avanzada</td><td>🔴 Técnica</td><td>1-2 horas</td></tr><tr><td><strong>Adobe DTM (Legacy)</strong></td><td>⚠️ Básica</td><td>🟡 Manual</td><td>20-45 minutos</td></tr></tbody></table>

***

#### 🟢 Adobe Analytics Directo (s\_code)

**✅ No requiere configuración adicional**

Los eventos se envían automáticamente usando `s.tl()` y aparecerán en sus reportes inmediatamente.

**Variables utilizadas por defecto:**

* **eVar20**: Nombre del evento Videsk
* **event20**: Contador de interacciones Videsk

***

#### 🟡 Adobe Launch/Experience Platform Tags

**⚠️ Requiere configuración básica**

**Paso 1: Crear Elementos de Datos**

1. Vaya a **Data Elements** en Adobe Launch
2. Cree los siguientes elementos de datos:

| Nombre                   | Tipo        | Configuración                                       |
| ------------------------ | ----------- | --------------------------------------------------- |
| `Videsk - Event Name`    | Custom Code | `return _satellite.getVar('videsk.event');`         |
| `Videsk - Widget Action` | Custom Code | `return _satellite.getVar('videsk.widget_action');` |
| `Videsk - Event Source`  | Custom Code | `return _satellite.getVar('videsk.event_source');`  |

**Paso 2: Crear Regla para Eventos Videsk**

1. Vaya a **Rules** → **Add Rule**
2. **Name**: "Videsk Widget Events"

**Event Configuration:**

* **Extension**: Core
* **Event Type**: Direct Call
* **Identifier**: `videsk_interaction`

**Action Configuration:**

* **Extension**: Adobe Analytics
* **Action Type**: Send Beacon
* **Tracking**: Link
* **Link Name**: `Videsk - %Videsk - Event Name%`

**Paso 3: Mapear Variables en Adobe Analytics**

En la acción de Adobe Analytics, configure:

| Variable Adobe | Valor                      |
| -------------- | -------------------------- |
| eVar20         | `%Videsk - Event Name%`    |
| eVar21         | `%Videsk - Widget Action%` |
| eVar22         | `%Videsk - Event Source%`  |
| event20        | `Videsk Interaction`       |

**Paso 4: Publicar Cambios**

1. **Save** la regla
2. Vaya a **Publishing** → **Add All Changed Resources**
3. **Build & Publish to Production**

***

#### 🔴 Adobe Experience Platform Web SDK

**❌ Requiere configuración técnica avanzada**

**Paso 1: Configurar Schema XDM**

Su schema XDM debe incluir los siguientes campos:

```json
{
  "_videsk": {
    "widget": {
      "version": "string",
      "action": "string", 
      "status": "boolean",
      "type": "string"
    },
    "interaction": {
      "timestamp": "datetime",
      "user_id": "string",
      "session_id": "string"
    },
    "call": {
      "id": "string",
      "type": "string",
      "duration": "integer",
      "quality": "string",
      "agent_id": "string",
      "queue_position": "integer"
    }
  }
}
```

**Paso 2: Configurar Datastream**

1. En Adobe Experience Platform, vaya a **Datastreams**
2. Seleccione su datastream
3. En **Adobe Analytics**, configure el mapeo:

| Campo XDM                       | Variable Analytics |
| ------------------------------- | ------------------ |
| `_videsk.widget.action`         | eVar20             |
| `_videsk.interaction.timestamp` | eVar21             |
| `eventType`                     | event20            |

**Paso 3: Verificar Configuración**

Ejecute en la consola del navegador:

```javascript
// Verificar que alloy está configurado
console.log('Alloy configured:', typeof window.alloy === 'function');

// Enviar evento de prueba
window.alloy('sendEvent', {
  type: 'videsk.test',
  data: { test: true }
});
```

***

### Verificación de Configuración

#### Método 1: Consola del Navegador

Abra las herramientas de desarrollador y ejecute:

```javascript
// Verificar detección automática
document.addEventListener('videsk-load', () => {
  const { adobe } = videsk.analytics;
  
  const config = adobe.getConfiguration();
  console.log('Adobe Configuration:', config);
  
  const testResult = adobe.test('onToggle', { test: true });
  console.log('Test Result:', testResult);
});
```

#### Método 2: Adobe Launch Debugger

1. Instale la extensión "Adobe Experience Platform Debugger"
2. Recargue su página
3. Interactúe con el widget de Videsk
4. Verifique en el debugger que aparezcan eventos con prefijo "videsk."

#### Método 3: Adobe Analytics Debugger

1. Instale "Adobe Analytics Debugger"
2. Active el debugger
3. Interactúe con el widget
4. Verifique que aparezcan llamadas `s.tl()` con datos de Videsk

***

### Resolución de Problemas

#### Problema: No veo eventos en los reportes

**Posibles causas:**

* Adobe Launch: Reglas no configuradas o no publicadas
* Web SDK: Schema XDM incompleto o datastream mal configurado
* Analytics directo: Código de seguimiento no actualizado

**Solución:**

1. Verifique la configuración según su tipo de implementación
2. Use las herramientas de verificación mencionadas arriba
3. Contacte al equipo de Videsk con los resultados de las pruebas

#### Problema: Eventos duplicados

**Causa:** Múltiples implementaciones de Adobe ejecutándose simultáneamente

**Solución:**

1. Verifique que solo tenga una implementación activa
2. Si necesita múltiples implementaciones, contacte soporte técnico

#### Problema: Variables en ubicaciones incorrectas

**Causa:** Mapeo de variables personalizado necesario

**Solución:**

1. Modifique el mapeo en su configuración de Adobe Launch
2. Para Analytics directo, proporcione configuración personalizada a Videsk

***

### Variables Personalizadas

Si necesita usar variables diferentes a las predeterminadas (eVar20, event20), puede configurarlas:

#### Adobe Launch

Modifique los elementos de datos y acciones según sus necesidades.

#### Adobe Analytics Directo

Contáctanos a [support@videsk.io](mailto:support@videsk.io) para configurar variables personalizadas en el widget.

#### Web SDK

Ajuste el mapeo en su configuración de datastream.
