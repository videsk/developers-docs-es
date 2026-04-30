---
description: >-
  Cómo embeber una Power App en Videsk usando su URL de embebido.
---

# Power Apps

## Prerrequisitos

* Power App publicada y funcional.
* Acceso de administrador a tu entorno de Power Apps.
* Cuenta de Videsk con permisos para registrar apps.

## Paso 1 — Habilitar el embebido en Power Apps

1. Entra al portal: [https://make.powerapps.com](https://make.powerapps.com).
2. Selecciona la Power App que quieres integrar.
3. Ve a **Configuración → Configuración de acceso web**.
4. Habilita **Permitir que esta aplicación se ejecute en un iframe**.

## Paso 2 — Obtener la URL de embebido

1. En la misma pantalla de configuración, ubica la sección **URL de embebido**.
2. Copia la URL completa (debe comenzar con `https://apps.powerapps.com/play/...`).

## Paso 3 — Registrar la app en Videsk

1. Entra a tu panel de administración en Videsk.
2. Abre **Configuración de Apps** y selecciona **Agregar nueva aplicación**.
3. Pega la URL de embebido en el campo correspondiente.
4. Guarda los cambios.

## Verificación

1. Entra a la consola de agente.
2. Acepta una llamada de prueba.
3. Verifica que la Power App aparezca y opere normalmente.

## Solución de problemas

| Síntoma | Verifica |
| --- | --- |
| La Power App no se renderiza | Que la opción **Permitir que esta aplicación se ejecute en un iframe** esté habilitada. |
| URL inválida | Que copiaste la URL de embebido completa, incluidos sus parámetros. |
| El usuario no puede acceder | Que tenga permisos tanto en Power Apps como en Videsk. |
