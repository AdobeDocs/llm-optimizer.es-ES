---
source-git-commit: e9309dc8f8d1d81b953483f17dcb424e46d5cd3b
workflow-type: tm+mt
source-wordcount: '457'
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

## Opcional: Pruebe el enrutamiento en un nombre de host de ensayo {#retrieve-staging-edge-optimize-api-key}

**Opcional: probar enrutamiento en un nombre de host provisional**

Si desea validar el enrutamiento en un entorno inferior antes de habilitar el enrutamiento de producción, puede configurar un nombre de host de ensayo.

**Requisitos**

* El nombre de host de ensayo debe estar en el **mismo dominio registrable** que el de producción (por ejemplo, `https://staging.example.com` cuando la producción es `https://www.example.com`).
* Solo **un** dominio de ensayo por sitio. Una vez guardado, no se puede cambiar sin ponerse en contacto con Adobe.

**Obtenga su clave de API de ensayo**

1. Abra **Configuración del cliente** y seleccione **Configuración de CDN**.
2. En **Implementar optimizaciones en agentes de IA**, seleccione **Agregar dominio de ensayo** (o **Dominio de ensayo** si ya se ha configurado un dominio de ensayo).
3. Escriba la dirección URL de ensayo completa (incluido `https://`) y seleccione **Establecer dominio**.
4. Copie la clave de API **staging** del cuadro de diálogo de confirmación.

![Clave de API de dominio de ensayo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Implemente las mismas reglas de enrutamiento en el entorno de ensayo mediante la clave de API de ensayo.

**Probar tráfico de bots de ensayo**

Reemplace `https://staging.example.com/page.html` por su dirección URL y ruta de ensayo real. **Éxito:** La respuesta incluye el encabezado `x-edgeoptimize-request-id`.

Si necesita ayuda, comuníquese con `llmo-at-edge@adobe.com`.

## Comprobación del estado del enrutamiento en LLM Optimizer {#verify-routing-status-in-ui}

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Permitir la optimización en Edge mediante reglas de cortafuegos (opcional) {#waf-allowlist-setup}

Si su CDN utiliza un WAF o un Bot Manager:

* Lista de permitidos el agente de usuario `*AdobeEdgeOptimize/1.0*` en su WAF o Administrador de bots para que el servicio Optimizar en Edge pueda recuperar el contenido de origen.
* Si el firewall requiere una verificación adicional más allá del agente de usuario, genere un secreto (por ejemplo, `openssl rand -hex 32`) y:
   * Agregue `x-edgeoptimize-fetcher-key` con el secreto en sus reglas de enrutamiento junto con los otros `x-edgeoptimize-*` encabezados.
   * Agregue una regla de WAF o Bot Manager para permitir solicitudes en las que `x-edgeoptimize-fetcher-key` coincida con el mismo secreto.
* Optimizar en Edge reenvía este encabezado tal cual: usted es el propietario del ciclo de vida completo de la clave.

## Volver a la descripción general {#return-to-overview}

Para obtener más información sobre Optimizar en Edge, incluidas las oportunidades disponibles, los flujos de trabajo de optimización automática y las preguntas frecuentes, vuelve a [Optimizar en la descripción general de Edge](/help/dashboards/optimize-at-edge/overview.md).
