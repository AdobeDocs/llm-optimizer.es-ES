---
title: 'Optimizar en Edge: Akamai (BYOCDN)'
description: Obtenga información sobre cómo configurar Akamai BYOCDN para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 26%

---


# Akamai (BYOCDN)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas del Administrador de propiedades de Akamai, asegúrese de lo siguiente:

* Acceso al Administrador de propiedades de Akamai para su dominio.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Configuración**

La siguiente regla del Administrador de propiedades de Akamai enruta los agentes de usuario LLM a Edge Optimize. La configuración incluye los pasos siguientes:

**1. Establecer criterios de enrutamiento (coincidencia de usuario y agente)**

Establecer enrutamiento para los siguientes user-agents:image.png

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![Establecer criterios de enrutamiento](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Establecer origen y comportamiento de SSL**

Establecer origen como `live.edgeoptimize.net` y hacer coincidir SAN con `*.edgeoptimize.net`

![Establecer origen y comportamiento de SSL](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Establecer variable de clave de caché**

Establecer la variable de clave de caché `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` en `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![Establecer variable de clave de caché](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Reglas de almacenamiento en caché**

![Reglas de almacenamiento en caché](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modificar encabezados de solicitud entrantes**

Establezca los siguientes encabezados de solicitud entrantes:
`x-edgeoptimize-api-key` a la clave de API recuperada de LMO
`x-edgeoptimize-config` a `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` a `{{builtin.AK_URL}}`

![Modificar encabezados de solicitud entrantes](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Modificar encabezados de respuesta entrantes**

![Modificar encabezados de respuesta entrantes](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Modificación de ID de caché**

![Modificación de ID de caché](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modificar encabezados de solicitud salientes**

Establecer el encabezado `x-forwarded-host` en `{{builtin.AK_HOST}}`

![Modificar encabezados de solicitud de salida](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Conmutación por error del sitio**

![Conmutación por error del sitio](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![Comportamientos de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![Reglas de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

La conmutación por error del sitio garantiza que si Edge Optimize devuelve un error `4XX` o `5XX`, la solicitud se redirigirá automáticamente a su origen predeterminado para que el usuario final siga recibiendo una respuesta.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` | La respuesta optimizada se sirve al cliente. |
| Edge Optimize devuelve `4XX` o `5XX` | La solicitud se redirige de nuevo al origen predeterminado. |

{{verify-setup-byocdn}}

{{return-to-overview}}
