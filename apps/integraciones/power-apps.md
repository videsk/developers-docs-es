---
description: >-
  Esta guía explica paso a paso cómo integrar tu Power App en Videsk utilizando
  una URL de embebido.
---

# Power Apps

## Prerrequisitos

* Tener una Power App funcional
* Acceso de administrador a tu entorno de Power Apps
* Cuenta de Videsk con permisos de configuración

### Paso 1: Configurar Power App para embebido

1. Accede al portal de Power Apps (https://make.powerapps.com)
2. Selecciona la Power App que deseas integrar
3. Ve a la sección "Configuración" de tu aplicación
4. Busca la opción "Configuración de acceso web"
5. Habilita la opción "Permitir que esta aplicación se ejecute en un iframe"

### Paso 2: Obtener la URL de embebido

1. En la misma pantalla de configuración
2. Localiza la sección "URL de embebido"
3. Copia la URL completa proporcionada
   * La URL debe comenzar con: `https://apps.powerapps.com/play/...`
   * Asegúrate de copiar la URL completa incluyendo todos los parámetros

### Paso 3: Integrar en Videsk

1. Inicia sesión en tu panel de administración de Videsk
2. Ve a la sección "Configuración de Apps"
3. Selecciona "Agregar nueva aplicación"
4. En el campo de URL, pega la URL de embebido copiada de Power Apps
5. Guarda los cambios

## Verificación

Para asegurar que la integración fue exitosa:

1. Accede a tu interfaz de agente en Videsk
2. Verifica que puedas ver y acceder a tu Power App
3. Comprueba que todas las funcionalidades operen correctamente

## Solución de problemas comunes

Si la Power App no se muestra correctamente:

* Verifica que la opción "Permitir que esta aplicación se ejecute en un iframe" esté habilitada
* Confirma que la URL de embebido sea correcta y completa
* Asegúrate de que los usuarios tengan los permisos necesarios tanto en Power Apps como en Videsk

***

_Nota: Esta integración permite mantener todas las funcionalidades de tu Power App mientras la utilizas dentro del ambiente de Videsk._
