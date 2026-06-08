---
title: 'Optimizar en Edge: Akamai (BYOCDN)'
description: Obtenga información sobre cómo configurar Akamai BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:34:47.891Z'
TQID: 'https://experienceleague.adobe.com/oGtqsnvHYn0BSNLl40-KpVl0TjCZHESRgH1LcVmjOiY'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: c5a8f033aac85913b56a40bb1560537da04847f2
workflow-type: tm+mt
source-wordcount: 810
ht-degree: 98%

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

La configuración de la conmutación por error del sitio consta de dos partes: el comportamiento de la conmutación por error (configurado dentro de la regla de enrutamiento principal de Optimizar en Edge) y una regla de encabezado de prueba de conmutación por error independiente.

**9a. Comportamiento de conmutación por error del sitio (dentro de la regla de enrutamiento principal de Optimizar en Edge)**

Dentro de la regla de enrutamiento principal, configure el comportamiento de conmutación por error del sitio y el fragmento XML avanzado de la siguiente manera:

>[!IMPORTANT]
>
>El fragmento XML de este paso requiere el comportamiento **Avanzado**. En algunos entornos de Akamai, este comportamiento no está disponible para la edición de autoservicio. Si no visualiza la opción **Avanzado**, póngase en contacto con el equipo de cuentas de Akamai o con el servicio de asistencia de Akamai para habilitar la configuración necesaria.

![Conmutación por error del sitio](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Añada el encabezado de la solicitud `x-edgeoptimize-request` con el valor `fo` mediante XML avanzado:

```
<forward:availability.fail-action2>
<add-header>
<status>on</status>
<name>x-edgeoptimize-request</name>
<value>fo</value>
</add-header>
</forward:availability.fail-action2>
```

![Comportamientos de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

**9b. Regla del encabezado de la prueba de conmutación por error (regla del mismo nivel)**

>[!IMPORTANT]
>
>Cree la regla **Conmutación por error de Edge Optimize: encabezado de la prueba** como **similar** (en el mismo nivel) de las reglas de enrutamiento: **no** anidadas en ellas. En el árbol de reglas del Administrador de propiedades de Akamai, la jerarquía debe tener un aspecto similar al siguiente:
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>Esto garantiza que la regla del encabezado de la prueba de conmutación por error se evalúe para **todas** las reglas de enrutamiento, no solo una.
>
>Asegúrese también de que la regla **Enrutamiento de Optimizar en Edge** no se anule con ninguna regla posterior que coincida y que cambie el origen, el comportamiento del almacenamiento en caché o el ID de caché para las mismas solicitudes. Si otra regla coincidente restablece estos comportamientos, es posible que el enrutamiento o el almacenamiento en caché de Optimizar en Edge no funcione según lo previsto.

Si el valor del encabezado de la solicitud `x-edgeoptimize-request` es `fo`, establezca el encabezado de la respuesta saliente `x-edgeoptimize-fo` en `true`.

![Reglas de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

La conmutación por error del sitio garantiza que si Edge Optimize devuelve un error `4XX` o `5XX`, la solicitud se redirigirá de nuevo automáticamente a su origen predeterminado para que el usuario final siga recibiendo una respuesta.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` | Se sirve una respuesta optimizada al cliente. |
| Edge Optimize devuelve `4XX` o `5XX` | La solicitud se redirige de nuevo al origen predeterminado. |

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
| `x-edgeoptimize-fo` | Solo está presente si se produjo la conmutación por error (valor: `1`) | Ausente |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
