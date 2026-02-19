---
title: 'Optimizar en Edge: Akamai (BYOCDN)'
description: Obtenga información sobre cómo configurar Akamai BYOCDN para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 14%

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

La configuración de la conmutación por error del sitio consta de dos partes: el comportamiento de la conmutación por error (configurado dentro de la regla de enrutamiento principal de optimización en el perímetro) y una regla de encabezado de prueba de conmutación por error independiente.

**9a. Comportamiento de conmutación por error del sitio (dentro de la regla de enrutamiento principal de optimización en el perímetro)**

Dentro de la regla de enrutamiento principal, configure el comportamiento de conmutación por error del sitio y el fragmento XML avanzado de la siguiente manera:

![Conmutación por error del sitio](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Agregue el encabezado de solicitud `x-edgeoptimize-request` con el valor `fo` mediante XML avanzado:

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

**9b. Regla de encabezado de prueba de conmutación por error (regla del mismo nivel)**

>[!IMPORTANT]
>
>Cree la regla **EdgeOptimize Failover - Test Header** como **hermano** (en el mismo nivel) de las reglas de enrutamiento: **no** anidadas en ellas. En el árbol de reglas del Administrador de propiedades de Akamai, la jerarquía debe tener un aspecto similar al siguiente:
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>Esto garantiza que la regla de encabezado de prueba de conmutación por error se evalúe para **todas** las reglas de enrutamiento, no solo una.

Si el valor del encabezado de solicitud `x-edgeoptimize-request` es `fo`, establezca el encabezado de respuesta saliente `x-edgeoptimize-fo` en `true`.

![Reglas de conmutación por error](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

La conmutación por error del sitio garantiza que si Edge Optimize devuelve un error `4XX` o `5XX`, la solicitud se redirigirá automáticamente a su origen predeterminado para que el usuario final siga recibiendo una respuesta.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` | La respuesta optimizada se sirve al cliente. |
| Edge Optimize devuelve `4XX` o `5XX` | La solicitud se redirige de nuevo al origen predeterminado. |

**Verificar la configuración**

Una vez completada la configuración, compruebe que el tráfico de bots se enrute a Edge Optimize y que el tráfico humano no se vea afectado.

**1. Probar el tráfico de bots (debe optimizarse)**

Simule una solicitud de bot de IA con un user-agent auténtico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Una respuesta correcta incluye el encabezado `x-edgeoptimize-request-id`, que confirma que la solicitud se enrutó a través de Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Probar el tráfico humano (NO debería verse afectado)**

Simule una solicitud normal de explorador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

La respuesta **no** debe contener el encabezado `x-edgeoptimize-request-id`. El contenido de la página y el tiempo de respuesta deben ser idénticos al de antes de habilitar Optimizar en Edge.

**3. Cómo diferenciar los dos escenarios**

| Encabezado | Tráfico de bots (optimizado) | Tráfico humano (no afectado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente: contiene un ID de solicitud único. | Ausente |
| `x-edgeoptimize-fo` | Solo está presente si se produjo la conmutación por error (valor: `1`) | Ausente |

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
