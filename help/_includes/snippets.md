---
source-git-commit: da789100d814004687de2f46e18a295671dec4b8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---
# Fragmentos

## Pasos de recuperación de claves API {#retrieve-byocdn-api-key}

**Pasos para recuperar la clave de API de optimización de Edge de producción:**

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

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

## Clave de API del dominio de ensayo (opcional) {#retrieve-staging-edge-optimize-api-key}

Utilice un nombre de host de ensayo cuando desee probar Optimizar en Edge en un entorno inferior antes de que el tráfico de producción utilice las reglas de enrutamiento.

**Requisitos previos**

* El nombre de host de ensayo debe pertenecer al **mismo dominio registrable** que el sitio de producción (por ejemplo, `https://staging.example.com` cuando la producción es `https://www.example.com`).
* Solo se puede configurar **un** dominio de ensayo para el sitio. Una vez guardado, no se puede cambiar sin ayuda.

**Pasos**

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

2. En la sección **Implementar optimizaciones en agentes de IA**, seleccione **Agregar dominio de ensayo** (o **Dominio de ensayo** si ya se ha configurado un dominio de ensayo).

3. En el cuadro de diálogo **Dominio de ensayo**, escriba la dirección URL de ensayo completa incluyendo `https://` y seleccione **Establecer dominio**.

   ![Cuadro de diálogo de entrada del dominio de ensayo](/help/assets/optimize-at-edge/byocdn-staging-domain-input.png)

4. Confirme el dominio en la siguiente solicitud. Cuando finaliza el flujo de trabajo, el cuadro de diálogo **Dominios de ensayo** muestra el dominio configurado y su **clave de API**. Seleccione **Copiar** para copiar la clave de API de ensayo.

   ![Clave de API de dominio de ensayo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Si necesita ayuda, comuníquese con `llmo-at-edge@adobe.com`.

## Comprobación del estado del enrutamiento en LLM Optimizer {#verify-routing-status-in-ui}

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Volver a la descripción general {#return-to-overview}

Para obtener más información sobre Optimizar en Edge, incluidas las oportunidades disponibles, los flujos de trabajo de optimización automática y las preguntas frecuentes, vuelve a [Optimizar en la descripción general de Edge](/help/dashboards/optimize-at-edge/overview.md).
