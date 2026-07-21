---
title: 'Optimizar en Edge: Akamai (BYOCDN)'
description: Obtenga información sobre cómo configurar Akamai BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:40:02.356Z'
TQID: 'https://experienceleague.adobe.com/XlHpXbtxqPl-XQQKWeQc3rbsizCT7U0TF1bQkyv0iM8'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 9d2324e23e07f01e16c4fc16c96213d03214918f
workflow-type: tm+mt
source-wordcount: 795
ht-degree: 76%

---


# Akamai (BYOCDN)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas del Administrador de propiedades de Akamai, asegúrese de lo siguiente:

* Acceso al Administrador de propiedades de Akamai para su dominio.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Configuración**

La siguiente regla del Administrador de propiedades de Akamai dirige el tráfico de páginas HTML agénticas a Edge Optimize. La configuración incluye los pasos siguientes:

**1. Establecer criterios de enrutamiento (coincidencia de usuario-agente y tráfico de HTML)**

Establecer el enrutamiento de los siguientes agentes de usuario:

```
 *AdobeEdgeOptimize-AI*
 *ChatGPT-User*
 *GPTBot*
 *OAI-SearchBot*
 *PerplexityBot*
 *Perplexity-User*
 *ClaudeBot*
 *Claude-User*
 *Claude-SearchBot*
```

>[!NOTE]
>
>Aplique la regla de enrutamiento Optimizar en Edge solo al tráfico de páginas HTML agénticas. Una configuración común es usar criterios del lado de la solicitud como, por ejemplo, **Extensión de archivo** para que coincida con `html` y `EMPTY_STRING` para direcciones URL de páginas sin extensión. Si su sitio sirve HTML desde otros patrones de URL o incluye rutas sin extensión que no sean de página, como los puntos finales de API, perfeccione la regla con criterios adicionales basados en rutas.

![Establecer criterios de enrutamiento](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Establecer origen y comportamiento de SSL**

Establecer origen como `live.edgeoptimize.net` y hacer coincidir SAN con `*.edgeoptimize.net`

>[!NOTE]
>
>Si la activación de la propiedad falla después de añadir la regla Optimizar en Edge, compruebe si la regla utiliza un modo de verificación SSL del servidor de origen diferente al de la regla predeterminada. Si es así, actualice la regla Optimizar en Edge para que coincida con la regla predeterminada. Por ejemplo, si la regla predeterminada utiliza **Configuración de la plataforma**, utilice **Configuración de la plataforma** aquí también. Si no puede utilizar la configuración requerida, póngase en contacto con el servicio de asistencia de Akamai.

![Establecer origen y comportamiento de SSL](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Establecer variable de clave de caché**

Establecer la variable de la clave de caché `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` en `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![Establecer variable de clave de caché](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Reglas de almacenamiento en caché**

![Reglas de almacenamiento en caché](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modificar encabezados de solicitud entrantes**

Establezca los siguientes encabezados de solicitud entrantes:
`x-edgeoptimize-api-key` para la clave de API recuperada de LLMO
`x-edgeoptimize-config` a `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` a `{{builtin.AK_URL}}`

![Modificar encabezados de solicitud entrantes](/help/assets/optimize-at-edge/akamai-step5-request.png)

**Permitir Optimizar en Edge mediante reglas de cortafuegos (opcional)**

{{waf-allowlist-setup}}

![Establecer el encabezado x-edgeoptimize-fetcher-key en el Administrador de propiedades](/help/assets/optimize-at-edge/akamai-step10-fetcher-key.png)

>[!NOTE]
>
>Añada también a la lista de permitidos el agente de usuario `*AdobeEdgeOptimize/1.0*` y el encabezado `x-edgeoptimize-fetcher-key` en el administrador de bots de Akamai.

**6. Modificar encabezados de respuesta entrantes**

![Modificar encabezados de respuesta entrantes](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Modificación de ID de caché**

![Modificación de ID de caché](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modificar los encabezados de solicitud salientes**

Establecer el encabezado `x-forwarded-host` en `{{builtin.AK_HOST}}`

![Modificar encabezados de solicitudes salientes](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Conmutación por error del sitio**

La configuración de conmutación por error del sitio consta de dos partes: un comportamiento de conmutación por error dentro de la regla de enrutamiento principal Optimizar en Edge y una regla del mismo nivel que agrega un encabezado de respuesta cuando se produce una reserva.

**9a. Configurar el comportamiento de conmutación por error del sitio**

Dentro de la regla de enrutamiento principal Optimizar en Edge, cree una regla secundaria llamada **Comportamiento de conmutación por error del sitio**. Configúrelo en **Coincidir con cualquiera** y agregue estos criterios:

* **El código de estado de respuesta** está en el intervalo de `400` a `599`.
* **Tiempo de espera de origen** es `Yes`.

![Conmutación por error del sitio](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![Configurar el comportamiento de conmutación por error del sitio](/help/assets/optimize-at-edge/akamai-step9-failover-settings.png)

**9b. Configurar la regla de encabezado de respuesta de conmutación por error**

>[!IMPORTANT]
>
>Cree la regla **Conmutación por error de Edge Optimize: encabezado de la prueba** como **similar** (en el mismo nivel) de las reglas de enrutamiento: **no** anidadas en ellas. En el árbol de reglas del Administrador de propiedades de Akamai, la jerarquía debe tener un aspecto similar al siguiente:
>
>```
>▼ Optimize at Edge                         ← parent rule group
>   ▼ Optimize at Edge Routing               ← routing child
>       Site Failover Behavior                 ← nested child
>   EdgeOptimize Failover - Test Header      ← sibling of routing child
>```
>
>La regla del mismo nivel se evalúa cuando Akamai vuelve a crear la solicitud fallida para el nombre de host original. El criterio de clave de API en la regla de enrutamiento evita que esa solicitud se envíe de nuevo a Edge Optimize.
>
>Asegúrese también de que la regla **Enrutamiento de Optimizar en Edge** no se anule con ninguna regla posterior que coincida y que cambie el origen, el comportamiento del almacenamiento en caché o el ID de caché para las mismas solicitudes. Si otra regla coincidente restablece estos comportamientos, es posible que el enrutamiento o el almacenamiento en caché de Optimizar en Edge no funcione según lo previsto.

![Configurar la regla de encabezado de respuesta de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-header.png)

La conmutación por error del sitio garantiza que, si Edge Optimize devuelve un error o un tiempo de espera agotado, Akamai vuelva a crear la solicitud para el nombre de host original de modo que el visitante siga recibiendo la respuesta normal del sitio.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` o `3XX` | Se proporciona la respuesta optimizada. `x-edgeoptimize-request-id` está presente. |
| Edge Optimize devuelve `4XX`-`5XX` o se agota el tiempo de espera del origen | La solicitud se vuelve a crear para el nombre de host original. La respuesta incluye `x-edgeoptimize-fo: true`. |

**Verificar la configuración**

Una vez completada la configuración, compruebe que el tráfico de bots se enrute a Edge Optimize y que el tráfico humano no se vea afectado.

**1. Probar el tráfico de bots (debe optimizarse)**

Simule una solicitud de bot de IA con un agente de usuario agéntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Una respuesta correcta incluye el encabezado `x-edgeoptimize-request-id`, que confirma que la solicitud se enrutó mediante Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Probar el tráfico humano (NO debería verse afectado)**

Simule una solicitud normal de un explorador:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

La respuesta **no** debe contener el encabezado `x-edgeoptimize-request-id`. El contenido de la página y el tiempo de respuesta deben ser idénticos al de antes de habilitar Optimizar en Edge.

**3. Cómo diferenciar entre dos escenarios**

| Encabezado | Tráfico de bots (optimizado) | Tráfico humano (no afectado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente: contiene un ID de solicitud único | Ausente |
| `x-edgeoptimize-fo` | Solo está presente si se produjo la conmutación por error (valor: `true`) | Ausente |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
