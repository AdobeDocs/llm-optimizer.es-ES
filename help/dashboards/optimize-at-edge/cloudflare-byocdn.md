---
title: 'Optimizar en Edge: Cloud Flare (BYOCDN)'
description: Obtenga información sobre cómo configurar CloudFlare para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 14dbee36f39b0d993d448edccb63fb8a519704a1
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 1%

---


# Cloudflare (BYOCDN)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de enrutamiento de Cloud Flare Worker, asegúrese de lo siguiente:

* Cuenta de Cloudflare con trabajadores habilitados en su dominio.
* Acceso a la configuración DNS de su dominio en Cloudflare.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.
* (Opcional) Una clave de API de optimización de Edge de ensayo si prueba primero el enrutamiento en un nombre de host de ensayo.

{{retrieve-byocdn-api-key}}

{{retrieve-staging-edge-optimize-api-key}}

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

## Opciones de configuración

Existen dos formas de configurar el trabajo de Cloudflare para optimizar Edge:

* [**Opción 1: implementar en Cloudflare (recomendado)**](#option-1-deploy-to-cloudflare): crea automáticamente un nuevo trabajador y le solicita las variables de entorno y los secretos necesarios. Utilice esta opción si no tiene un Cloudflare Worker existente para este dominio.
* [**Opción 2: configuración manual**](#option-2-manual-setup): instrucciones paso a paso para crear y configurar el trabajador. Utilice esta opción si ya tiene un Cloudflare Worker existente que desea ampliar o si prefiere un control total sobre la implementación.

Independientemente de la opción que elija, debe vincular manualmente el trabajador a su dominio (consulte [Paso: agregar una ruta a su dominio](#add-a-route-to-your-domain)).

## Opción 1: Implementar en Cloudflare

Esta opción usa el botón **Implementar en Cloudflare** para crear automáticamente el trabajador y configurar las variables de entorno y los secretos requeridos en su cuenta de Cloudflare. Esta es la forma más rápida de empezar si va a configurar un nuevo trabajador.

>[!IMPORTANT]
>
>Use esta opción solo si **no** tiene un Cloudflare Worker existente en su dominio. Si ya tiene un trabajador, use [Opción 2: Configuración manual](#option-2-manual-setup) para agregar la lógica de enrutamiento Optimizar de Edge al trabajador existente.

**Paso 1: Implementar el trabajador**

Haga clic en el botón siguiente para implementar el trabajador de optimización de Edge en su cuenta de Cloudflare:

[![Implementar en Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/cloudflare/automation)

**Paso 2: complete el formulario de implementación**

Al hacer clic en el botón, se abre la página Configuración de trabajadores. Rellene el formulario como se indica a continuación:

![Página de configuración de los trabajadores de Cloudflare](/help/assets/optimize-at-edge/cloudflare-deploy-form.png)

1. **Cuenta de Git**: seleccione su cuenta de GitHub o GitLab en el menú desplegable. Cloudflare ramifica el código de trabajo en un repositorio de su cuenta. Si no aparece ninguna cuenta, puede agregar una nueva conexión directamente desde el menú desplegable seleccionando **+ Nueva conexión de GitHub** o **+ Nueva conexión de GitLab**. Para obtener más información, consulte la [Guía de integración de Git de Cloudflare](https://developers.cloudflare.com/workers/ci-cd/builds/git-integration/github-integration/).

   ![Menú desplegable de cuenta Git que muestra las opciones Nueva conexión de GitHub y Nueva conexión de GitLab](/help/assets/optimize-at-edge/cloudflare-git-connection.png)
2. **Crear repositorio Git privado**: déjelo marcado (predeterminado).
3. **Nombre del proyecto** — Déjelo como `edge-optimize-router` o escriba un nombre de su elección.
4. **EDGE_OPTIMIZE_API_KEY**: pegue la clave de API de optimización de Edge proporcionada por Adobe. Este valor se almacena como un secreto cifrado.
5. **EDGE_OPTIMIZE_TARGET_HOST**: escriba el dominio del sitio sin el protocolo (por ejemplo, `www.example.com`).
6. **Comando de compilación** — Dejar vacío.
7. **Implementar comando** — Dejar como `npm run deploy` (precargada).
8. **Compilaciones para ramas que no son de producción** — Dejar sin marcar. Se trata de una función del flujo de trabajo del desarrollador y no es necesaria para esta implementación.
9. Haga clic en **Crear e implementar**.

Una vez implementado el trabajador, continúe con [Agregue una ruta a su dominio](#add-a-route-to-your-domain) para vincular el trabajador con su dominio. El enrutamiento no se configura automáticamente y debe completarse manualmente.

## Opción 2: configuración manual

Siga estos pasos para crear y configurar el trabajador manualmente.

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

**Paso 3: Configurar variables y secretos de entorno**

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

## Agregar una ruta al dominio {#add-a-route-to-your-domain}

Independientemente de la opción de configuración utilizada, debe vincular manualmente el trabajador al dominio. Este paso activa el trabajador en su tráfico.

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
| Errores 401 o 403 de Edge Optimize | Falta la clave API o no es válida. | Compruebe que `EDGE_OPTIMIZE_API_KEY` esté configurado correctamente en las variables y los secretos del entorno. Póngase en contacto con Adobe para confirmar que su clave de API está activa. |
| Redirecciones o bucles infinitos | El encabezado de protección de bucle no está configurado o comprobado correctamente. | Asegúrese de que la comprobación del encabezado `x-edgeoptimize-request` esté completada. |
| Tráfico humano afectado | La lógica de enrutamiento de trabajo es demasiado amplia. | Compruebe que la lógica de coincidencia del agente de usuario sea correcta y que no distingue entre mayúsculas y minúsculas. Compruebe que `TARGETED_PATHS` esté configurado correctamente. |
| Tiempos de respuesta bajos | Latencia de red para optimizar el servidor de Edge. | Esto es lo que se espera para la primera solicitud; las solicitudes posteriores se almacenan en la caché en Edge Optimize. |
| `x-edgeoptimize-fo: 1` encabezado en respuesta | Edge Optimize devolvió un error y se produjo una conmutación por error al origen. | Consulte los registros de Cloud Flare Workers para ver el código de error específico. Verifique el estado del servicio Optimizar de Edge con Adobe. |
| La conmutación por error no funciona | Indicadores de conmutación por error deshabilitados o error en la lógica de conmutación por error. | Compruebe que `FAILOVER_ON_4XX` y `FAILOVER_ON_5XX` estén establecidos en `true`. Compruebe los registros de trabajo para ver si hay mensajes de error. |
| Algunas rutas no se optimizan | Ruta que no coincide con las rutas de destino o el patrón de página de HTML. | Compruebe que la ruta de acceso esté en `TARGETED_PATHS` (si se especifica) y que coincida con el patrón regex de la página de HTML. |
| Solicitudes que fallan con un host no válido | `EDGE_OPTIMIZE_TARGET_HOST` incluye el protocolo (por ejemplo, `https://`). | Use solamente el nombre de dominio sin protocolo (por ejemplo, `example.com`, no `https://example.com`). |
| Error 530 durante la conmutación por error | Cloudflare no se puede conectar al origen o la solicitud de conmutación por error tiene encabezados no válidos. | Asegúrese de que la función de conmutación por error elimine los encabezados de Edge Optimize. Compruebe que el origen es accesible y que DNS está configurado correctamente. |

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

**4. Dominio de ensayo (opcional)**

Si usa un nombre de host de ensayo y una clave de API de ensayo de LLM Optimizer, implemente la misma lógica de trabajo en la zona **staging** mediante la clave de API **staging**. A continuación, compruebe el tráfico de bots en el host de ensayo:

```
curl -svo /dev/null https://staging.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Reemplace `https://staging.example.com/page.html` por su dirección URL y ruta de ensayo real. Una respuesta correcta incluye el encabezado `x-edgeoptimize-request-id`.

{{verify-routing-status-in-ui}}

{{return-to-overview}}
