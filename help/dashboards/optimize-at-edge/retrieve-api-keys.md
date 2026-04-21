---
title: Recuperación de las claves API
description: Cómo recuperar las claves de la API de optimización de Edge de producción y ensayo desde LLM Optimizer.
feature: Opportunities
source-git-commit: 3b6dc163f4488a22937916beb6778de4abc5a20c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Recuperación de las claves API

Antes de configurar la CDN, recupere las claves API de Edge Optimize de la interfaz de usuario de LLM Optimizer. Necesita una clave de API **production** para el tráfico en vivo. De forma opcional, también puede recuperar una clave de API **staging** para probar primero el enrutamiento en un nombre de host de ensayo.

## Clave de API de producción

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Busque la sección **Implementar optimizaciones en agentes de IA**. Marque la casilla de verificación **Activar motor de optimización**.

   ![Implementar optimizaciones en agentes de IA — pendientes](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. En el cuadro de diálogo de confirmación, seleccione **Habilitar**.

   ![Activar diálogo de confirmación del motor de optimización](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Seleccione **Ver detalles**. En el cuadro de diálogo **Implementar detalles de optimizaciones**, copie la **clave de API de producción** (use **Copiar** junto al campo).

   ![Clave de API de producción en Detalles de optimizaciones de implementación](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >El cuadro de diálogo puede mostrar que la configuración no se ha completado. Esto es lo que se espera hasta que se verifique el enrutamiento: aún puede copiar la clave de API para que su equipo de TI o CDN pueda finalizar la configuración.

Si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o `llmo-at-edge@adobe.com`.

## Clave de API de ensayo (opcional)

Para validar el enrutamiento en un entorno inferior antes de habilitar el enrutamiento de producción, puede configurar un nombre de host de ensayo.

**Requisitos**

* El nombre de host de ensayo debe estar en el **mismo dominio registrable** que el de producción (por ejemplo, `https://staging.example.com` cuando la producción es `https://www.example.com`).
* Solo **un** dominio de ensayo por sitio. Una vez guardado, no se puede cambiar sin ponerse en contacto con Adobe.

**Pasos**

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.
2. En **Implementar optimizaciones en agentes de IA**, seleccione **Agregar dominio de ensayo** (o **Dominio de ensayo** si ya se ha configurado un dominio de ensayo).
3. Escriba la dirección URL de ensayo completa (incluido `https://`) y seleccione **Establecer dominio**.
4. Copie la clave de API **staging** del cuadro de diálogo de confirmación.

   ![Clave de API de dominio de ensayo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Implemente las mismas reglas de enrutamiento en el entorno de ensayo mediante la clave de API de ensayo.

Si necesita ayuda, comuníquese con `llmo-at-edge@adobe.com`.

## Pasos siguientes

Después de recuperar las claves API, vuelva a la [guía de configuración de CDN](/help/dashboards/optimize-at-edge/overview.md#cdn-configuration-guides) para configurar el enrutamiento.
