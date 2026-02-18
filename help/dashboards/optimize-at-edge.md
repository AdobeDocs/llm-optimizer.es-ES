---
title: Optimizar en Edge
description: Obtenga información sobre cómo entregar optimizaciones en LLM Optimizer en el perímetro de la CDN sin necesidad de realizar cambios en la creación.
feature: Opportunities
source-git-commit: 1f665bd14349c15d92f8274742606abcf9b02000
workflow-type: tm+mt
source-wordcount: '4708'
ht-degree: 44%

---


# Optimizar en Edge

Esta página proporciona información general detallada sobre cómo entregar optimizaciones en el perímetro de CDN sin ningún cambio en la creación. Abarca el proceso de incorporación, las oportunidades de optimización disponibles y cómo optimizar automáticamente en Edge.

>[!NOTE]
>Actualmente, esta funcionalidad se encuentra en Acceso anticipado. Puede obtener más información acerca de los programas de Acceso anticipado [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## ¿Qué es Optimizar en Edge?

Optimizar en Edge es una capacidad de implementación basada en Edge en LLM Optimizer que proporciona cambios compatibles con la IA a los agentes de usuario de LLM. En el contexto actual, “Edge” significa que la optimización se aplica en la capa de CDN. Dado que ofrece optimizaciones en la capa de CDN, no se requieren cambios de creación en el sistema de administración de contenido (CMS), por lo que el CMS de origen permanece sin cambios. Esta separación le permite mejorar la visibilidad de LLM sin alterar los flujos de trabajo de publicación existentes. Se dirige únicamente al tráfico agéntico y no afecta ni a los usuarios humanos ni a los bots de SEO. Cuando LLM Optimizer detecta oportunidades para optimizar una página, los usuarios pueden implementar correcciones directamente en el perímetro de la CDN.

Optimizar en Edge es una alternativa más rápida y sencilla que las correcciones tradicionales que requieren esfuerzos de ingeniería complejos. Como se ha mencionado, una vez que complete una configuración única, no se requieren cambios de plataforma ni ciclos de desarrollo largos para aplicar los cambios. Puede publicar mejoras en minutos sin necesidad de participación del desarrollador. Es una forma sin código de optimizar el sitio web para los agentes de IA.

Optimizar en Edge está concebido para usuarios empresariales en equipos de marketing, SEO, contenido y estrategia digital. Permite a los usuarios empresariales completar el recorrido completo en LLM Optimizer como identificar oportunidades, comprender sugerencias e implementar fácilmente las correcciones. Con Optimizar en Edge, los usuarios obtienen una vista previa de los cambios que se implementan rápidamente en CDN, también validan que las optimizaciones estén activas. Se puede realizar un seguimiento del rendimiento en el ecosistema de LLM Optimizer.

### Ventajas principales

* **Envío solo de IA:** sirve HTML optimizado solo a agentes de IA sin afectar a los visitantes humanos ni a los bots de SEO.
* **Ciclos más rápidos:** publique cambios en minutos, no en semanas. No se requieren cambios de plataforma ni ciclos de ingeniería largos.
* **Reversible:** compatibilidad con una capacidad de reversión en un clic para revertir la página en minutos.
* **Sin impacto en el rendimiento:** las optimizaciones y el almacenamiento en caché basados en Edge no afectan la latencia del sitio.
* **No depende de CDN ni de CMS:** funciona con cualquier configuración de CDN y configuración de front-end, independientemente del sistema de administración de contenido.

### ¿Qué oportunidades se admiten con Optimizar en Edge?

Las oportunidades que pueden mejorar la experiencia web auténtica se admiten con Optimizar en Edge. Obtenga más información acerca de cada oportunidad en la página [Panel de control de oportunidades](/help/dashboards/opportunities.md) y en la sección de oportunidades de la página actual.

## Incorporación

Póngase en contacto con el equipo de cuentas de Adobe o con el equipo de FDE para iniciar el proceso de incorporación. Su equipo de TI o CDN también tiene que completar los requisitos previos y el proceso de configuración. Además, también puede ponerse en contacto con `llmo-at-edge@adobe.com` para obtener más ayuda para la incorporación.

Requisitos previos para la incorporación a Optimizar en Edge:

* Complete el proceso de incorporación a LLM Optimizer.
* Complete el proceso de reenvío de registros para los registros de CDN.

Requisitos para su equipo de TI/CDN:
* Agregue `*AdobeEdgeOptimize/1.0*` user-agent a la Lista de permitidos del archivo robots.txt del sitio o a las reglas de administración del tráfico de bots.
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o de CDN.
* Añadir las reglas de enrutamiento de Optimizar en Edge en la CDN.
* Confirmar Optimizar en Edge en la interfaz de LLM Optimizer.

Para guiar el proceso de configuración, que se presenta a continuación, hay configuraciones de muestra para una serie de configuraciones de CDN. Tenga en cuenta que estos ejemplos deben adaptarse a la configuración real en directo. Se recomienda aplicar primero los cambios en los entornos inferiores.

>[!BEGINTABS]

>[!TAB CDN administrada por AEM Cloud Service (rápidamente)]

**Optimizar Edge: CDN administrada por AEM Cloud Service (rápidamente)**

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Para empezar a enrutar el tráfico auténtico a Edge Optimize:

1. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. En **Enrutamiento del tráfico de IA para implementar optimizaciones**, marque la casilla de verificación **Implementar optimizaciones en agentes de IA**. El equipo de Adobe se encargará de la configuración de enrutamiento en su nombre.

   ![Marque Implementar optimizaciones en agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Después de activar la casilla de verificación, el estado mostrará que la configuración está en curso. El equipo de Adobe completará la configuración de enrutamiento por usted.

   ![Configuración de enrutamiento de tráfico de IA en curso](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   Una vez configurado y activo el enrutamiento, el estado se actualizará para mostrar una marca de verificación verde que indique que el enrutamiento se ha habilitado correctamente. No se requiere ninguna otra acción por su parte.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

**Enrutamiento de autoservicio a través de la canalización de Cloud Manager**

Si prefiere configurar el enrutamiento por su cuenta a través de la canalización de Cloud Manager, siga los pasos a continuación. La configuración de enrutamiento se realiza mediante una [regla de CDN originSelector](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). Los requisitos previos son los siguientes:

* Decida el dominio que desea distribuir.
* Decida las rutas que desea enrutar.
* Decida los agentes de usuario que desea enrutar (regex recomendada).

Para poder implementar la regla, debe hacer lo siguiente:

* Crear una [canalización de configuración](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/operations/config-pipeline).
* Confirme el archivo de configuración `cdn.yaml` en el repositorio.
* Ejecute la canalización de configuración.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"
```

**Verificar la configuración**

Para probar la configuración, ejecute un curl y espere lo siguiente:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

>[!TAB Fastly (BYOCDN)]

**Optimizar Edge - Rápidamente (BYOCDN)**

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de VCL de Fastly, asegúrese de lo siguiente:

* Acceso a Fastly para su dominio.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.

**Pasos para recuperar la clave de API:**

1. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. En **Enrutamiento del tráfico de IA para implementar optimizaciones**, marque la casilla de verificación **Implementar optimizaciones en agentes de IA**.

   ![Marque Implementar optimizaciones en agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie la clave de API y continúe con los pasos de configuración de enrutamiento a continuación.

   ![Copiar la clave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >En esta fase, el estado puede mostrar una cruz roja que indique que la configuración aún no ha finalizado. Esto es de esperar: una vez que complete la configuración de enrutamiento a continuación y el tráfico de bots de IA comience a fluir, el estado se actualizará a una marca de verificación verde que confirme que el enrutamiento se ha habilitado correctamente.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

**Configuración**

Agregue los tres fragmentos de VCL siguientes al servicio Fastly. Estos fragmentos administran el enrutamiento de solicitudes auténticas a Edge Optimize, la separación de claves de caché y la conmutación por error al origen predeterminado.

![VCL de Fastly](/help/assets/optimize-at-edge/fastly-vcl.png)

![Añadir fragmentos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**fragmento vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**fragmento vcl_hash**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**fragmento vcl_deliver**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**Conmutación por error**

El fragmento `vcl_deliver` administra la conmutación por error automáticamente. Si Edge Optimize devuelve un error `4XX` o `5XX`, la solicitud se reinicia y se redirige de nuevo al origen predeterminado para que el usuario final siga recibiendo una respuesta. Las respuestas de conmutación por error incluyen el encabezado `x-edgeoptimize-fo: 1`.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` | La respuesta optimizada se sirve al cliente. |
| Edge Optimize devuelve `4XX` o `5XX` | La solicitud se reinicia y se sirve desde el origen predeterminado. |
| Respuesta de conmutación por error | Incluye el encabezado `x-edgeoptimize-fo: 1`. |

**Verificar la configuración**

Para probar la configuración, ejecute un curl y espere lo siguiente:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Akamai (BYOCDN)]

**Optimizar Edge - Akamai (BYOCDN)**

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas del Administrador de propiedades de Akamai, asegúrese de lo siguiente:

* Acceso al Administrador de propiedades de Akamai para su dominio.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.

**Pasos para recuperar la clave de API:**

1. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. En **Enrutamiento del tráfico de IA para implementar optimizaciones**, marque la casilla de verificación **Implementar optimizaciones en agentes de IA**.

   ![Marque Implementar optimizaciones en agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie la clave de API y continúe con los pasos de configuración de enrutamiento a continuación.

   ![Copiar la clave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >En esta fase, el estado puede mostrar una cruz roja que indique que la configuración aún no ha finalizado. Esto es de esperar: una vez que complete la configuración de enrutamiento a continuación y el tráfico de bots de IA comience a fluir, el estado se actualizará a una marca de verificación verde que confirme que el enrutamiento se ha habilitado correctamente.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

**Configuración**

La siguiente regla del Administrador de propiedades de Akamai enruta los agentes de usuario LLM a Edge Optimize. La configuración incluye los pasos siguientes:

**1. Establecer criterios de enrutamiento (coincidencia de usuario y agente)**

Establezca el enrutamiento para los siguientes user-agents:

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

**Verificar la configuración**

Para probar la configuración, ejecute un curl y espere lo siguiente:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Llamada de nube (BYOCDN)]

**Optimizar Edge - Cloudflare (BYOCDN)**

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de enrutamiento de Cloud Flare Worker, asegúrese de lo siguiente:

* Cuenta de Cloudflare con trabajadores habilitados en su dominio.
* Acceso a la configuración DNS de su dominio en Cloudflare.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.

**Pasos para recuperar la clave de API:**

1. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. En **Enrutamiento del tráfico de IA para implementar optimizaciones**, marque la casilla de verificación **Implementar optimizaciones en agentes de IA**.

   ![Marque Implementar optimizaciones en agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie la clave de API y continúe con los pasos de configuración de enrutamiento a continuación.

   ![Copiar la clave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >En esta fase, el estado puede mostrar una cruz roja que indique que la configuración aún no ha finalizado. Esto es de esperar: una vez que complete la configuración de enrutamiento a continuación y el tráfico de bots de IA comience a fluir, el estado se actualizará a una marca de verificación verde que confirme que el enrutamiento se ha habilitado correctamente.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

**Funcionamiento del enrutamiento**

Cuando se configura correctamente, una solicitud a su dominio (por ejemplo, `www.example.com/page.html`) desde un agente de usuario auténtico es interceptada por el trabajador de Cloudflare y enrutada al servidor de Edge Optimize. La solicitud de back-end incluye los encabezados necesarios.

**Probando la solicitud de servidor**

Puede verificar el enrutamiento realizando una solicitud directa al back-end de Edge Optimize.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Encabezados obligatorios**

Se deben configurar los siguientes encabezados en las solicitudes al back-end de Edge Optimize:

| Encabezado | Descripción | Ejemplos |
|--------|-------------|---------|
| `x-forwarded-host` | El host original de la solicitud. Necesario para identificar el dominio del sitio. | `www.example.com` |
| `x-edgeoptimize-url` | Ruta de URL y cadena de consulta originales de la solicitud. | `/page.html` o `/products?id=123` |
| `x-edgeoptimize-api-key` | La clave de API proporcionada por Adobe para su dominio. | `your-api-key-here` |
| `x-edgeoptimize-config` | Cadena de configuración para diferenciación de clave de caché. | `LLMCLIENT=TRUE;` |

**Paso 1: Crear el trabajo de Cloudflare**

1. Inicie sesión en su tablero de Cloudflare.
2. Vaya a **Trabajadores y páginas** en la barra lateral.
3. Haga clic en **Crear aplicación** y luego en **Crear trabajador**.
4. Asigne un nombre al trabajador (por ejemplo, `edge-optimize-router`).
5. Haga clic en **Implementar** para crear el trabajador con el código predeterminado.

![Panel de trabajadores de Cloudflare](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Paso 2: Agregar el código de trabajador**

Después de crear el trabajador, haga clic en **Editar código** y reemplace el código predeterminado por el siguiente:

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Haga clic en **Guardar e implementar** para publicar el trabajador.

![Editor de código de trabajo de Cloudflare](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Paso 3: Configurar variables de entorno**

Las variables de entorno almacenan la configuración confidencial como la clave de API de forma segura.

1. En la configuración del trabajador, vaya a **Configuración** > **Variables**.
2. En **Variables de entorno**, haga clic en **Agregar variable**.
3. Añada las siguientes variables:

   | Nombre de la variable | Descripción | Necesario |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | La clave de API de optimización de Edge proporcionada por Adobe. | Sí |
   | `EDGE_OPTIMIZE_TARGET_HOST` | Host de destino para solicitudes de Edge Optimize (enviadas como encabezado `x-forwarded-host`) y dominio de origen para conmutación por error. Debe ser el dominio solamente sin protocolo (por ejemplo, `www.example.com`, no `https://www.example.com`). | Sí |

4. Para la clave de API, haz clic en **Cifrar** para almacenarla de forma segura.
5. Haga clic en **Guardar e implementar**.

![Variables de entorno de Cloudflare](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Paso 4: Agregar una ruta a su dominio**

Para activar el trabajador en su dominio:

1. Vaya a **Configuración** > **Déclencheur** del trabajador.
2. En **Rutas**, haga clic en **Agregar ruta**.
3. Escriba el patrón de dominio (por ejemplo, `www.example.com/*` o `example.com/*`).
4. Seleccione la zona en la lista desplegable.
5. Haga clic en **Guardar**.

También puede configurar rutas en el nivel de zona:

1. Vaya a su dominio en Cloudflare.
2. Vaya a **Rutas de trabajadores**.
3. Haga clic en **Agregar ruta** y especifique el patrón y el trabajador.

![Rutas de trabajo de Cloudflare](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Paso 5: Verificar la configuración**

Después del despliegue, pruebe la configuración realizando una solicitud con un agente de usuario auténtico.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Una respuesta correcta incluye el encabezado `x-edgeoptimize-request-id`:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

También puede comprobar que el tráfico normal sigue funcionando:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0"
```

Esta solicitud debe servirse desde su origen sin el encabezado `x-edgeoptimize-request-id`.

**Comprobando comportamiento de conmutación por error**

Si Edge Optimize no está disponible o devuelve un error, el trabajador conmuta automáticamente por error al origen. Las respuestas de conmutación por error incluyen el encabezado `x-edgeoptimize-fo`:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Puede supervisar los eventos de conmutación por error en los registros de los trabajadores de Cloudflare para solucionar problemas.

**Explicación de la lógica de trabajo**

Cloudflare Worker implementa la siguiente lógica:

1. **Detección de agente de usuario:** Comprueba si el agente de usuario de la solicitud entrante coincide con alguno de los bots agénticos definidos (sin distinción de mayúsculas y minúsculas).

2. **Destino de ruta:** filtra de forma opcional las solicitudes basadas en rutas de destino. De manera predeterminada, todas las páginas de HTML (direcciones URL que terminan con `/`, sin extensión o `.html`) se enrutan. Puede especificar rutas de acceso específicas utilizando la matriz `TARGETED_PATHS`.

3. **Protección de bucle:** El encabezado `x-edgeoptimize-request` evita bucles infinitos. Cuando Edge Optimize devuelve las solicitudes al origen, este encabezado se establece en `"1"` y el trabajador pasa la solicitud sin devolverla al servidor de Edge Optimize.

4. **Seguridad del encabezado:** Antes de establecer encabezados de Edge Optimize, el trabajador quita los encabezados `x-edgeoptimize-*` existentes de la solicitud entrante para evitar ataques de inyección de encabezado.

5. **Asignación de encabezados:** El trabajador establece los encabezados necesarios para Optimizar Edge:
   * `x-forwarded-host` - Identifica el dominio del sitio original.
   * `x-edgeoptimize-url` - Conserva la ruta de acceso de la solicitud y la cadena de consulta originales.
   * `x-edgeoptimize-api-key`: autentica la solicitud con Edge Optimize.
   * `x-edgeoptimize-config`: proporciona la configuración de clave de caché.

6. **Lógica de conmutación por error:** Si Edge Optimize devuelve código de estado de error (errores de cliente 4XX o errores de servidor 5XX) o la solicitud falla debido a un error de red, el trabajador conmuta automáticamente por error al origen mediante `EDGE_OPTIMIZE_TARGET_HOST`. La respuesta de conmutación por error incluye el encabezado `x-edgeoptimize-fo: 1` para indicar que se produjo la conmutación por error.

7. **Administración de redireccionamiento:** La opción `redirect: "manual"` garantiza que las respuestas de redireccionamiento de Edge Optimize se pasen al cliente sin que el trabajador las siga.

**Personalizando la configuración**

Puede personalizar el comportamiento del trabajador modificando las constantes de configuración en la parte superior del código:

**Lista de bots agente**

Modifique la matriz `AGENTIC_BOTS` para agregar o quitar agentes de usuario:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**Rutas de destino**

De forma predeterminada, todas las páginas de HTML se dirigen a Edge Optimize. Para limitar el enrutamiento a rutas de acceso específicas, modifique la matriz `TARGETED_PATHS`:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**Configuración de conmutación por error**

De forma predeterminada, el trabajador conmuta por error cualquier error 4XX o 5XX de Edge Optimize. Personalice este comportamiento:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Consideraciones importantes**

* **Comportamiento de conmutación por error:** El trabajador conmuta automáticamente por error al origen si Edge Optimize devuelve algún error (códigos de estado 4XX o 5XX) o si la solicitud falla debido a un error de red. La conmutación por error usa `EDGE_OPTIMIZE_TARGET_HOST` como dominio de origen (similar a `F_Default_Origin` de Fastly o `Default_Origin` de CloudFront). Las respuestas de conmutación por error incluyen el encabezado `x-edgeoptimize-fo: 1`, que puede utilizar para la supervisión y la depuración.

* **Almacenamiento en caché:** Cloudflare almacena en caché las respuestas según la dirección URL de forma predeterminada. Dado que el tráfico real recibe un contenido diferente al tráfico humano, asegúrese de que la configuración de la caché se corresponde con esto. Considere utilizar la API de caché o los encabezados de caché para diferenciar el contenido almacenado en caché. El encabezado `x-edgeoptimize-config` debe incluirse en la clave de caché.

* **Limitación de velocidad:** Monitorice su uso de Edge Optimize y considere implementar una limitación de velocidad para el tráfico real si es necesario.

* **Pruebas:** Pruebe siempre la configuración en un entorno de ensayo antes de implementarla en producción. Compruebe que el tráfico humano y el tráfico agéntico se comportan según lo esperado. Pruebe el comportamiento de la conmutación por error simulando los errores de Edge Optimize.

* **Registro:** Habilite el registro de trabajadores de Cloudflare para supervisar solicitudes y solucionar problemas. Vaya a **Trabajadores** > **su trabajador** > **Registros** para ver los registros en tiempo real. El trabajador registra eventos de conmutación por error para la depuración.

**Solución de problemas**

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| No hay ningún encabezado `x-edgeoptimize-request-id` en respuesta | La ruta de trabajo no coincide o el agente de usuario no está en la lista de bots agénticos. | Compruebe que el patrón de ruta coincida con la dirección URL de la solicitud. Compruebe que el agente de usuario se encuentra en la matriz `AGENTIC_BOTS`. |
| Errores 401 o 403 de Edge Optimize | Falta la clave API o no es válida. | Compruebe que `EDGE_OPTIMIZE_API_KEY` esté configurado correctamente en las variables de entorno. Póngase en contacto con Adobe para confirmar que su clave de API está activa. |
| Redirecciones o bucles infinitos | El encabezado de protección de bucle no está configurado o comprobado correctamente. | Asegúrese de que la comprobación del encabezado `x-edgeoptimize-request` esté completada. |
| Tráfico humano afectado | La lógica de enrutamiento de trabajo es demasiado amplia. | Compruebe que la lógica de coincidencia del agente de usuario sea correcta y que no distingue entre mayúsculas y minúsculas. Compruebe que `TARGETED_PATHS` esté configurado correctamente. |
| Tiempos de respuesta bajos | Latencia de red para optimizar el servidor de Edge. | Esto es lo que se espera para la primera solicitud; las solicitudes posteriores se almacenan en la caché en Edge Optimize. |
| `x-edgeoptimize-fo: 1` encabezado en respuesta | Edge Optimize devolvió un error y se produjo una conmutación por error al origen. | Consulte los registros de Cloud Flare Workers para ver el código de error específico. Verifique el estado del servicio Optimizar de Edge con Adobe. |
| La conmutación por error no funciona | Indicadores de conmutación por error deshabilitados o error en la lógica de conmutación por error. | Compruebe que `FAILOVER_ON_4XX` y `FAILOVER_ON_5XX` estén establecidos en `true`. Compruebe los registros de trabajo para ver si hay mensajes de error. |
| Algunas rutas no se optimizan | Ruta que no coincide con las rutas de destino o el patrón de página de HTML. | Compruebe que la ruta de acceso esté en `TARGETED_PATHS` (si se especifica) y que coincida con el patrón regex de la página de HTML. |
| Solicitudes que fallan con un host no válido | `EDGE_OPTIMIZE_TARGET_HOST` incluye el protocolo (por ejemplo, `https://`). | Use solamente el nombre de dominio sin protocolo (por ejemplo, `example.com`, no `https://example.com`). |
| Error 530 durante la conmutación por error | Cloudflare no se puede conectar al origen o la solicitud de conmutación por error tiene encabezados no válidos. | Asegúrese de que la función de conmutación por error elimine los encabezados de Edge Optimize. Compruebe que el origen es accesible y que DNS está configurado correctamente. |

>[!ENDTABS]

>[!NOTE]
>Para otros proveedores de CDN, póngase en contacto con `llmo-at-edge@adobe.com` para ayudar a sus equipos de TI/CDN en la incorporación. Una vez completadas las configuraciones, puede implementar sugerencias para las oportunidades de Optimizar en Edge en LLM Optimizer.

## Oportunidades

En la tabla siguiente se presentan las oportunidades que pueden mejorar la experiencia web agéntica y que son compatibles con Optimizar en Edge.

| Oportunidad | Tipo | Identificación automática | Sugerencia automática | Optimización automática |
|---------|----------|----------|----------|----------|
| Recuperar visibilidad del contenido | Optimización técnica del motor generativo | Detecta páginas donde se oculta contenido crítico a los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Resalta el contenido que puede estar disponible para los agentes de IA y recomienda habilitar el procesamiento previo para esas páginas. | Proporciona una instantánea de HTML totalmente procesada y compatible con IA al tráfico agéntico que recupera el contenido oculto anteriormente. |
| Añadir resúmenes compatibles con LLM | Optimización de contenido | Identifica páginas largas o complejas que carecen de resúmenes concisos a nivel de página o sección, lo que dificulta que la inteligencia artificial las escanee y comprenda rápidamente. | Recomienda resúmenes cortos generados por IA a nivel de página y sección que capturan contenido clave. | Inserta los resúmenes en las secciones relevantes de HTML, lo que mejora la forma en que los modelos interpretan y describen el contenido de la página. |
| Añadir preguntas frecuentes relevantes | Optimización de contenido | Detecta lagunas de intención en el contenido de la página existente que podrían beneficiarse de las preguntas frecuentes. | Sugiere contenido de preguntas frecuentes generado por IA alineado con la intención del usuario y los temas existentes. | Inserta contenido de preguntas frecuentes en el HTML, lo que hace que las páginas sean más detectables y relevantes en las respuestas basadas en IA. |
| Simplificar contenido complejo | Optimización de contenido | Indica las páginas con texto complejo que puede dificultar la comprensión de la IA. | Proporciona versiones simplificadas de texto complejo generadas por IA preservando al mismo tiempo el significado original. | Reescribe secciones complejas en la página, lo que mejora la legibilidad de la IA. |

### Herramientas adicionales

[Adobe LLM Optimizer: ¿su página web se puede citar?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) La extensión de Chrome muestra la cantidad de contenido web al que pueden acceder los LLM y lo que permanece oculto. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración.

Con un solo clic, puede evaluar la legibilidad automática de cualquier sitio. Puede ver una comparación en paralelo de lo que ven los agentes de IA frente a lo que ven las personas y realizar un cálculo estimado de cuánto contenido se puede recuperar mediante LLM Optimizer. Consulte la página [¿Puede la IA leer su sitio web?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obtener más información.

## Oportunidades detalladas

En las secciones siguientes, puede ver detalles adicionales de cada oportunidad compatible con Optimizar en Edge.

### Recuperar visibilidad del contenido

Esta oportunidad indica las páginas donde el contenido clave está oculto para los agentes de IA debido al procesamiento en el lado del cliente. Para cada página identificada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta los huecos de visibilidad y le permite aplicar cambios directamente para recuperar el contenido oculto. Al implementar esta oportunidad con Optimizar en Edge, se proporciona una versión de la página procesada previamente y optimizada con IA para los agentes de usuario de LLM para que puedan acceder al contexto completo sin ejecutar JavaScript.
Esto garantiza que la página sea primero totalmente visible para los agentes de IA. Además de ese HTML preprocesado, se aplican mejoras adicionales.

>[!IMPORTANT]
>Esta funcionalidad de procesamiento previo se aplica automáticamente a todas las oportunidades que se presentan a continuación cuando se implementa con Optimizar en Edge para garantizar que la página sea totalmente visible para los agentes de IA.

### Añadir resúmenes compatibles con LLM

Esta oportunidad identifica las páginas que pueden beneficiarse de resúmenes concisos para ayudar a los LLM a comprender rápidamente de qué trata el contenido de la página. Para cada página, la oportunidad detecta dónde más se necesita un resumen y crea resúmenes generados por IA a nivel de página o de sección. Cuando se implementa con Optimizar en Edge, estos resúmenes se insertan en el HTML que recuperan los agentes de IA, lo que mejora las posibilidades de que el contenido se describa con mayor precisión.

### Añadir preguntas frecuentes relevantes

Esta oportunidad indica las páginas en las que el contenido adicional de preguntas y respuestas podría ajustarse mejor a la intención del usuario y las indicaciones en la detección basada en la IA. Para cada página, propone bloques de preguntas frecuentes generados por IA vinculados a la intención del usuario y al contenido de la página. Con Optimizar en Edge, estas preguntas frecuentes se insertan en el HTML, lo que hace que su página sea más compatible con la IA y aumenta la probabilidad de que las respuestas con IA reflejen directamente sus indicaciones.

### Simplificar contenido complejo

Esta oportunidad encuentra páginas con párrafos largos y complejos que pueden reducir la comprensión de la IA. Para cada página que supera los umbrales de legibilidad, crea contenido generado por IA que es más sencillo y fácil de analizar, conservando al mismo tiempo el significado original. Cuando se implementa en el perímetro, el contenido simplificado que se entrega al tráfico agéntico ayuda a los LLM a interpretar y resumir el contenido con mayor fiabilidad.

## Optimización automática en Edge

Para cada oportunidad, puede obtener una vista previa, editar, implementar, ver en directo y restablecer las optimizaciones en el perímetro.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Vista previa

La **Vista previa** le permite ver el impacto de una sugerencia antes de que se ponga en marcha. Muestra una comparación en paralelo entre la página actual y la versión optimizada por IA que se espera después de aplicar la sugerencia. Esta vista utiliza la misma lógica de Optimizar en Edge que activará el tráfico en directo, pero en un modo de vista previa aislado. Esto no afecta al tráfico en directo, ya que es una simulación de solo lectura para la revisión.

![Vista previa](/help/assets/optimize-at-edge/preview.png)

### Editar

**Editar** le permite perfeccionar o reescribir por completo la sugerencia generada automáticamente antes de implementarla. En lugar de aceptar la sugerencia, mantiene un control total a través del flujo de trabajo de edición. La vista muestra los cambios propuestos en un editor estructurado, donde puede modificar el texto para que se ajuste mejor a la intención original. A continuación, la versión editada se proporcionará a los agentes de IA una vez implementada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implementar

**Implementar** publica las sugerencias seleccionadas para que las experiencias optimizadas se puedan ofrecer desde el perímetro a los agentes de IA. Si la CDN está completamente enrutada, todas las páginas del dominio suelen estar disponibles con los nuevos cambios en cuestión de minutos. Si el enrutamiento solo se ha configurado para rutas seleccionadas, solo las páginas incluidas en la lista de permitidos se publicarán con las optimizaciones.

![Implementar](/help/assets/optimize-at-edge/deploy.png)

### Ver en directo

**Ver en directo** le permite verificar que la optimización está activa y que se comporta según lo esperado para el tráfico agéntico, una vista a la que de otra manera sería difícil acceder. Puede ver la página activa en Sugerencias fijas, que procesa la página tal como se muestra a los agentes de IA.

![Ver en directo](/help/assets/optimize-at-edge/view-live.png)

### Reversión

Una reversión de forma segura revierte una optimización implementada anteriormente. La versión de solo IA de la página suele volver a su estado anterior en cuestión de minutos, lo que permite experimentar con optimizaciones cuando es necesario.

![Reversión](/help/assets/optimize-at-edge/rollback.png)

## Preguntas frecuentes

P. ¿A qué tipos de LLM se dirige con Optimizar en Edge?

Usted es quien define la lista de agentes de usuario a los que dirigirse durante el proceso de incorporación.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

P. ¿Qué sucede si todavía no me he incorporado a Optimizar en Edge?

Si hace clic en **Implementar optimizaciones** antes de completar la configuración necesaria, no se aplicará nada al sitio. En su lugar, un cuadro de diálogo emergente le solicitará que se ponga en contacto con nuestro equipo en `llmo-at-edge@adobe.com` para obtener ayuda sobre la incorporación. Hasta que se complete la incorporación, aún puede explorar las oportunidades y sugerencias detectadas, pero el flujo de trabajo de implementación con un solo clic permanecerá inactivo.

P: ¿Qué sucede cuando el contenido se actualiza en la fuente?

Servimos la versión optimizada de su página desde la caché siempre y cuando la página de origen subyacente no haya cambiado. Sin embargo, cuando el origen cambia para **Recuperar Visibilidad del contenido**, nuestro sistema se actualiza automáticamente para que los agentes de IA siempre reciban el contenido más actualizado. Esto se debe a que utilizamos la configuración de tiempo de duración de caché (TTL) bajo (por orden de minutos) para que cualquier actualización de contenido en su sitio déclencheur una nueva optimización dentro de esa ventana. Para oportunidades de contenido como **Agregar resúmenes compatibles con LLM**, LLM Optimizer supervisa la página de origen en busca de cambios. Si se detecta un cambio, pausamos la optimización y la marcamos para que sea analizada por humanos a fin de evitar que el contenido se desplace entre la página visible del agente y la página visible por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. ¿Optimize at Edge solo es para sitios que utilizan Adobe Edge Delivery Service (EDS)?

No. Optimizar en Edge no depende de la red de distribución de contenido (CDN) y funciona con cualquier arquitectura front-end, no solo con las implementadas en la pila EDS de Adobe.

P. ¿En qué se diferencia el procesamiento previo de Optimizar en Edge del procesamiento tradicional del lado del servidor (SSR)?

Ambos resuelven diferentes problemas y pueden trabajar juntos. El SSR tradicional procesa contenido del lado del servidor, pero no incluye contenido cargado posteriormente en el explorador. El procesamiento previo de Optimizar en Edge captura la página después de que JavaScript y los datos del lado del cliente se hayan cargado, lo que produce la versión completamente ensamblada en el perímetro de CDN. SSR se centra en mejorar la experiencia humana y Optimizar en Edge mejora la experiencia web para los LLM.

P. ¿Qué sucede si implemento optimizaciones para algunas direcciones URL de mi dominio, pero no para todas?

Solo se modifican las direcciones URL que se hayan optimizado explícitamente. Para las direcciones URL con oportunidades implementadas, los agentes de IA reciben la versión optimizada. Para las URL sin oportunidades implementadas, nuestro servicio simplemente envía la página original tal cual sin aplicar cambios ni almacenarla en nuestra capa de caché de optimización. Esto garantiza que pueda implementar las optimizaciones de forma selectiva sin afectar al resto del sitio.
