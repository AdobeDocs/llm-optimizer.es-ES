---
title: 'Optimizar en Edge: Cloudflare (BYOCDN)'
description: Obtenga información sobre cómo configurar Cloudflare BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:46:02.378Z'
TQID: 'https://experienceleague.adobe.com/ZgOX0yC8qyb13Y7YNCg3Y1A6Q3TSk9-mUQ8gthzQvLM'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e0828736-236a-487b-a478-5a635455eadc
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: e36ee407933e2d3d56cadf1c9517f23f24d41d91
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 93%

---


# Cloudflare (BYOCDN)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de enrutamiento de Cloud Flare Worker, asegúrese de lo siguiente:

* Tener una cuenta de Cloudflare con trabajadores habilitados en su dominio.
* Tener acceso a la configuración DNS de su dominio en Cloudflare.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Funcionamiento del enrutamiento

Cuando se configura correctamente, Cloudflare Worker intercepta una solicitud a su dominio (por ejemplo, `www.example.com/page.html`) desde un agente de usuario agéntico y la enruta al back-end de Edge Optimize. La solicitud de back-end incluye los encabezados necesarios.

### Prueba de la solicitud de servidor

Puede verificar el enrutamiento realizando una solicitud directa al back-end de Edge Optimize.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

### Encabezados obligatorios

Se deben configurar los siguientes encabezados en las solicitudes dirigidas al back-end de Edge Optimize:

| Encabezado | Descripción | Ejemplos |
|--------|-------------|---------|
| `x-forwarded-host` | El host original de la solicitud. Es necesario para identificar el dominio del sitio. | `www.example.com` |
| `x-edgeoptimize-url` | La ruta de URL y la cadena de consulta originales de la solicitud. | `/page.html` o `/products?id=123` |
| `x-edgeoptimize-api-key` | La clave de API proporcionada por Adobe para su dominio. | `your-api-key-here` |
| `x-edgeoptimize-config` | Cadena de configuración para la diferenciación de la clave de caché. | `LLMCLIENT=TRUE;` |

## Opciones de configuración

Existen dos maneras de configurar Cloudflare Worker para Edge Optimize:

* [**Opción 1: Implementar en Cloudflare (recomendado)**](#option-1-deploy-to-cloudflare): crea automáticamente un nuevo trabajador y solicita las variables de entorno y los secretos necesarios. Utilice esta opción si no dispone de un Cloudflare Worker existente para este dominio.
* [**Opción 2: Configuración manual**](#option-2-manual-setup): instrucciones paso a paso para crear y configurar el trabajador usted mismo. Utilice esta opción si ya cuenta con un Cloudflare Worker configurado en su dominio: deberá combinar el código de Edge Optimize con su trabajador existente (consulte el [Paso 2: Añadir el código de Worker](#option-2-manual-setup)), o si lo prefiere, tener control total sobre la implementación.

Independientemente de la opción que elija, debe vincular manualmente el trabajador a su dominio; consulte el [paso: Añadir una ruta a su dominio](#add-a-route-to-your-domain).

## Opción 1: Implementar en Cloudflare

Esta opción utiliza el botón **Implementar en Cloudflare** para crear automáticamente el trabajador y configurar las variables de entorno y los secretos necesarios en su cuenta de Cloudflare. Esta es la forma más rápida de empezar si está configurando un nuevo trabajador.

>[!IMPORTANT]
>
>Utilice esta opción únicamente si **no** cuenta con un Cloudflare Worker existente en su dominio. Si ya tiene un trabajador, utilice la [Opción 2: configuración manual](#option-2-manual-setup) para añadir la lógica de enrutamiento de Edge Optimize a su trabajador existente.

### Paso 1: Implementar el trabajador

Haga clic en el botón de abajo para implementar el trabjador de Edge Optimize en su cuenta de Cloudflare:

[![Implementar en Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/cloudflare/automation)

### Paso 2: Rellene el formulario de implementación

Al hacer clic en el botón, se abrirá la página de configuración de Workers. Rellene el formulario de la siguiente manera:

![Página de configuración de Cloudflare Workers](/help/assets/optimize-at-edge/cloudflare-deploy-form.png)

1. **Cuenta Git**: seleccione su cuenta de GitHub o GitLab en el menú desplegable. Cloudflare bifurca el código de trabajador a un repositorio de su cuenta. Si no aparece ninguna cuenta, puede añadir una nueva conexión directamente desde el menú desplegable seleccionando **+ Nueva conexión de GitHub** o **+ Nueva conexión de GitLab**. Para obtener más información, consulte la [guía de integración de Cloudflare Git](https://developers.cloudflare.com/workers/ci-cd/builds/git-integration/github-integration/).

   ![Menú desplegable de la cuenta Git que muestra las opciones Nueva conexión de GitHub y Nueva conexión de GitLab](/help/assets/optimize-at-edge/cloudflare-git-connection.png)
2. **Crear repositorio Git privado**: déjelo marcado (predeterminado).
3. **Nombre del proyecto**: déjelo como `edge-optimize-router` o escriba el nombre que desee.
4. **EDGE_OPTIMIZE_API_KEY**: pegue su clave de API de Edge Optimize proporcionada por Adobe. Este valor se almacena como un secreto cifrado.
5. **EDGE_OPTIMIZE_TARGET_HOST**: escriba el dominio del sitio sin el protocolo (por ejemplo, `www.example.com`).
6. **Comando de compilación**: déjelo vacío.
7. **Implementar comando**: déjelo como `npm run deploy` (precargado).
8. **Compilaciones para ramas que no son de producción**: déjelo sin marcar. Se trata de una función del flujo de trabajo del desarrollador y no es necesaria para esta implementación.
9. Haga clic en **Crear e implementar**.

Una vez implementado el trabajador, prosiga con [Añadir una ruta a su dominio](#add-a-route-to-your-domain) para vincular el trabajador con su dominio. El enrutamiento no se configura automáticamente y debe completarse manualmente.

## Opción 2: configuración manual

Siga estos pasos para crear y configurar el trabajador manualmente.

### Paso 1: Creación del trabajador de Cloudflare

1. Inicie sesión en su panel de control de Cloudflare.
2. Vaya a **Trabajadores y páginas** en la barra lateral.
3. Haga clic en **Crear aplicación** y luego en **Crear trabajador**.
4. Asigne un nombre al trabajador (por ejemplo, `edge-optimize-router`).
5. Haga clic en **Implementar** para crear el trabajador con el código predeterminado.

![Panel control de Cloudflare Workers](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

### Paso 2: Añadir el código de Worker

Después de crear el trabajador, haga clic en **Editar código** y reemplace el código predeterminado por el código de [worker.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudflare/automation/src/worker.js). Si ya tiene un Cloudflare Worker, combine el código con el código de trabajador existente en lugar de reemplazarlo por completo.

Haga clic en **Guardar e implementar** para publicar el trabajador.

### Paso 3: Configurar las variables y los secretos de entorno

Las variables del entorno almacenan la configuración confidencial como su clave de API de forma segura.

1. En la configuración del trabajador, vaya a **Configuración** > **Variables**.
2. En **Variables del entorno**, haga clic en **Añadir variable**.
3. Añada las siguientes variables:

   | Nombre de la variable | Descripción | Necesario |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Su clave de API de Edge Optimize proporcionada por Adobe. | Sí |
   | `EDGE_OPTIMIZE_TARGET_HOST` | El host de destino para solicitudes de Edge Optimize (enviadas como encabezado `x-forwarded-host`) y el dominio de origen para conmutación por error. Debe ser solamente el dominio sin protocolo (por ejemplo, `www.example.com`, no `https://www.example.com`). | Sí |

4. Para la clave de API, haga clic en **Cifrar** para almacenarla de forma segura.
5. Haga clic en **Guardar e implementar**.

![Variables del entorno de Cloudflare](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

## Añadir una ruta a su dominio {#add-a-route-to-your-domain}

Independientemente de la opción de configuración utilizada, debe vincular manualmente el trabajador al dominio. Este paso activa el trabajador en su tráfico.

1. Vaya a la **Configuración** del trabajador > **Activadores**.
2. En **Rutas**, haga clic en **Añadir ruta**.
3. Escriba el patrón de su dominio (por ejemplo, `www.example.com/*` o `example.com/*`).
4. Seleccione una zona de la lista desplegable.
5. Haga clic en **Guardar**.

También puede configurar rutas en el nivel de zona:

1. Vaya a su dominio en Cloudflare.
2. Vaya a **Rutas de los trabajadores**.
3. Haga clic en **Añadir ruta** y especifique el patrón y el trabajador.

![Rutas de Cloudflare Worker](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

### Verificación del comportamiento de failover

Si Edge Optimize no está disponible o devuelve un error, el trabajador conmuta automáticamente por error a su origen. Las respuestas de la conmutación por error incluyen el encabezado `x-edgeoptimize-fo`:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Puede supervisar los eventos de conmutación por error en los registros de Cloudflare Workers para solucionar problemas.

### Explicación de la lógica de trabajo

Cloudflare Worker implementa la siguiente lógica:

1. **Detección de agente de usuario:** comprueba si el agente de usuario de la solicitud entrante coincide con alguno de los bots agénticos definidos (no distingue entre mayúsculas y minúsculas).

2. **Destino de ruta:** filtra de forma opcional las solicitudes basadas en rutas de destino. De manera predeterminada, todas las páginas HTML (URL que terminan con `/`, sin extensión o `.html`) se enrutan. Puede especificar rutas de acceso específicas utilizando la matriz `TARGETED_PATHS`.

3. **Protección de bucle:** el encabezado `x-edgeoptimize-request` evita bucles infinitos. Cuando Edge Optimize devuelve las solicitudes a su origen, este encabezado se establece en `"1"` y el trabajador deja pasar la solicitud sin redirigirla a Edge Optimize.

4. **Seguridad del encabezado:** antes de establecer encabezados de Edge Optimize, el trabajador quita todos los encabezados `x-edgeoptimize-*` de la solicitud entrante para evitar ataques de inyección de encabezado.

5. **Asignación de encabezados:** el trabajador establece los encabezados necesarios de Edge Optimize:
   * `x-forwarded-host`: identifica el dominio del sitio original.
   * `x-edgeoptimize-url`: conserva la ruta de acceso de la solicitud y la cadena de consulta originales.
   * `x-edgeoptimize-api-key`: autentica la solicitud con Edge Optimize.
   * `x-edgeoptimize-config`: proporciona la configuración de clave de caché.

6. **Lógica de conmutación por error:** si Edge Optimize devuelve código de estado de error (errores de cliente 4XX o errores de servidor 5XX) o se produce un error en la solicitud debido a un fallo de red, el trabajador conmuta automáticamente por error a su origen mediante `EDGE_OPTIMIZE_TARGET_HOST`. La respuesta de conmutación por error incluye el encabezado `x-edgeoptimize-fo: 1` para indicar que se ha producido la conmutación por error.

7. **Administración de redireccionamiento:** la opción `redirect: "manual"` garantiza que las respuestas de redireccionamiento de Edge Optimize se pasen al cliente sin que el trabajador las siga.

## Personalizar la configuración

Puede personalizar el comportamiento del trabajador modificando las constantes de configuración en la parte superior del código:

### Lista de bots agénticos

Modifique la matriz `AGENTIC_BOTS` para añadir o quitar agentes de usuario:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  'ClaudeBot',
  'Claude-User',
  'Claude-SearchBot',
  // Add additional user agents as needed
];
```

### Rutas de destino

De forma predeterminada, todas las páginas HTML se enrutan a Edge Optimize. Para limitar el enrutamiento a rutas de acceso específicas, modifique la matriz `TARGETED_PATHS`:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

### Configuración de conmutación por error

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

### Consideraciones importantes

* **Comportamiento de conmutación por error:** el trabajador conmuta automáticamente por error a su origen si Edge Optimize devuelve algún error (códigos de estado 4XX o 5XX) o si la solicitud falla debido a un error de red. La conmutación por error usa `EDGE_OPTIMIZE_TARGET_HOST` como dominio de origen (similar a `F_Default_Origin` de Fastly o `Default_Origin` de CloudFront). Las respuestas de conmutación por error incluyen el encabezado `x-edgeoptimize-fo: 1`, que puede utilizar para la supervisión y la depuración.

* **Almacenamiento en caché:** Cloudflare almacena en caché las respuestas según la URL de forma predeterminada. Dado que el tráfico agéntico recibe un contenido diferente al tráfico humano, asegúrese de que la configuración de la caché se corresponde con esto. Considere utilizar la API de caché o los encabezados de caché para diferenciar el contenido almacenado en caché. El encabezado `x-edgeoptimize-config` debe incluirse en la clave de caché.

* **Limitación de volumen:** monitorice su uso de Edge Optimize y considere implementar una limitación de volumen para el tráfico agéntico si fuese necesario.

* **Pruebas:** pruebe siempre la configuración en un entorno de ensayo antes de implementarla en producción. Compruebe que el tráfico humano y el agéntico se comportan según lo esperado. Pruebe el comportamiento de la conmutación por error simulando los errores de Edge Optimize.

* **Registro:** habilite el registro de Cloudflare Workers para supervisar solicitudes y solucionar problemas. Vaya a **Trabajadores** > **su trabajador** > **Registros** para ver los registros en tiempo real. El trabajador registra eventos de conmutación por error para la depuración.

## Resolución de problemas

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| No hay ningún encabezado `x-edgeoptimize-request-id` en la respuesta | La ruta del trabajador no coincide o el agente de usuario no está en la lista de bots agénticos. | Compruebe que el patrón de la ruta coincida con la URL de la solicitud. Compruebe que el agente de usuario se encuentra en la matriz `AGENTIC_BOTS`. |
| Errores 401 o 403 de Edge Optimize | Falta la clave API o no es válida. | Compruebe que `EDGE_OPTIMIZE_API_KEY` se haya establecido correctamente en las variables del entorno y los secretos. Póngase en contacto con Adobe para confirmar que su clave de API está activa. |
| Redirecciones o bucles infinitos | El encabezado de protección de bucle no está configurado o no se ha comprobado correctamente. | Asegúrese de que la comprobación del encabezado `x-edgeoptimize-request` esté activa. |
| Tráfico humano afectado | La lógica de enrutamiento del trabajador es demasiado amplia. | Compruebe que la lógica de coincidencia del agente de usuario sea correcta y que no distingue entre mayúsculas y minúsculas. Compruebe que la configuración de `TARGETED_PATHS` sea correcta. |
| Tiempos de respuesta largos | Latencia de la red del back-end de Edge Optimize. | Esto es lo que se espera para la primera solicitud; las solicitudes posteriores se almacenan en la caché en Edge Optimize. |
| Encabezado `x-edgeoptimize-fo: 1` en respuesta | Edge Optimize devolvió un error y se produjo una conmutación por error al origen. | Consulte los registros de Cloudflare Workers para ver el código de error específico. Verifique el estado del servicio de Edge Optimize con Adobe. |
| La conmutación por error no funciona | Se han deshabilitado los indicadores de conmutación por error o se ha producido un error en su lógica. | Compruebe que `FAILOVER_ON_4XX` y `FAILOVER_ON_5XX` estén establecidos en `true`. Compruebe los registros de los trabajadores para ver si hay mensajes de error. |
| Algunas rutas no se optimizan | La ruta no coincide con las rutas de destino o el patrón de la página HTML. | Compruebe que la ruta de acceso esté en `TARGETED_PATHS` (si se especifica) y que coincida con el patrón regex de la página HTML. |
| Las solicitudes fallan con un host no válido | `EDGE_OPTIMIZE_TARGET_HOST` incluye un protocolo (por ejemplo, `https://`). | Use solamente el nombre del dominio sin protocolo (por ejemplo, `example.com`, no `https://example.com`). |
| Error 530 durante la conmutación por error | Cloudflare no se puede conectar al origen o la solicitud de conmutación por error tiene encabezados no válidos. | Asegúrese de que la función de conmutación por error elimine los encabezados de Edge Optimize. Compruebe que su origen sea accesible y que el DNS esté configurado correctamente. |

## Permitir la optimización en Edge mediante reglas de cortafuegos (opcional)

{{waf-allowlist-setup}}

## Verificación de la configuración

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
