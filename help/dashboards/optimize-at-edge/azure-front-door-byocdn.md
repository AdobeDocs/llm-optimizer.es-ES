---
title: Optimizar en Edge - Puerta delantera de Azure (BYOCDN)
description: Aprenda a configurar Azure Front Door BYOCDN para optimizar en Edge en LLM Optimizer.
feature: Opportunities
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: 1d07ce1820e2688a130e410ee88ab329d628356a
workflow-type: tm+mt
source-wordcount: 768
ht-degree: 24%

---


# Puerta delantera del Azure (BYOCDN)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

La puerta delantera del Azure no ejecuta código personalizado en el borde. El enrutamiento se ha configurado con un **conjunto de reglas** junto con un **grupo de origen** específico para Edge Optimize. La conmutación por error se gestiona mediante los sondeos de mantenimiento del grupo de origen basados en prioridades de Azure Front Door.

**Requisitos previos**

Antes de configurar las reglas de enrutamiento de puerta delantera de Azure, asegúrese de lo siguiente:

* Acceso a su perfil de Azure Front Door.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Paso 1: Crear un grupo de origen para Optimizar de Edge

Su perfil de Azure Front Door ya tiene un grupo de origen predeterminado que apunta a su origen. Crear un grupo de origen **new** para Edge Optimize:

* **Nombre:** `edge-optimize-origin-group`
* **Orígenes (conmutación por error basada en prioridad):**
   * **Prioridad 1** — `live.edgeoptimize.net` (Encabezado de host de origen: `live.edgeoptimize.net`)
   * **Prioridad 2**: su extremo de dominio (por ejemplo, `www.example.com`). Esto es para la conmutación por error: si Edge Optimize no está en buen estado, solicita la ruta a su dominio, que vuelve a entrar en Azure Front Door y se proporciona desde su origen predeterminado.
* **Sondeos de estado:** **Habilitado**
   * Ruta: `/health/<your-domain>` (por ejemplo, `/health/www.example.com`)
   * Protocolo: HTTPS
   * Intervalo: 225 segundos
* **Afinidad de la sesión:** **Deshabilitada**
* **Validación del nombre del sujeto del certificado:** **Habilitado**

![Grupo de origen de Edge Optimize con dos orígenes basados en prioridades y sondeos de mantenimiento](/help/assets/optimize-at-edge/azure-front-door-origin-group.png)

>[!NOTE]
>
>El grupo de origen `edge-optimize-origin-group` muestra una advertencia **&quot;Sin asociar&quot;** en el portal. Esto es lógico: se hace referencia a él a través de una anulación de ruta de conjunto de reglas, no directamente a través de una ruta.

## Paso 2: Configuración de la ruta

Normalmente, se crea una ruta predeterminada con el perfil de la puerta principal de Azure. El conjunto de reglas (paso 3) anula el grupo de origen para el tráfico auténtico, por lo que no se necesita una ruta independiente para Optimizar de Edge.

## Paso 3: Crear el conjunto de reglas

Vaya a **Conjuntos de reglas** > **Agregue un conjunto de reglas** y asígnele el nombre `EORouting`. Añada tres reglas en este orden.

![conjunto de reglas EORouting que muestra las reglas de eliminación de encabezados y de enrutamiento de bots](/help/assets/optimize-at-edge/azure-front-door-ruleset-routing.png)

### Regla 1: StripIncomingEOHeaders01

Elimina los encabezados entrantes de Edge Optimize para evitar la suplantación. Sin condiciones: se aplica a todas las solicitudes. Dejar de evaluar: **Desactivado**.

**Acciones** — Eliminar encabezado de solicitud para cada una de:

* `x-edgeoptimize-url`
* `x-edgeoptimize-config`
* `x-edgeoptimize-api-key`
* `x-edgeoptimize-fetcher-key`

### Regla 2: EOGPTBotRootGET03

Enruta las solicitudes de bots en las rutas de página de HTML a Edge Optimize. Dejar de evaluar: **El**.

**Condiciones** (todas deben coincidir):

* Método de solicitud: **Igual** `GET`
* Ruta de solicitud: **RegEx** `(^$|^.*/$|(^|.*/)[^./]+$|^.*\.html$)` (coincide con la raíz del sitio, las rutas de acceso que terminan en `/`, las rutas de acceso de página sin extensión y las rutas de acceso de `.html`)
* Agente de usuario: **Contiene cualquiera de** `chatgpt-user`, `gptbot`, `oai-searchbot`, `adobeedgeoptimize-ai`, `perplexitybot`, `perplexity-user`, `claudebot`, `claude-user`, `claude-searchbot`. Establezca la transformación de la cadena en **A minúsculas**.
* `x-edgeoptimize-monitor`: **No contiene** `1`
* `x-edgeoptimize-request`: **No contiene ninguno de** `failover`, `1`

**Acciones**:

* Sobrescritura de encabezado de solicitud `x-edgeoptimize-url` = `/{url_path}?{query_string}`
* Sobrescritura de encabezado de solicitud `x-edgeoptimize-config` = `LLMCLIENT=TRUE;`
* Sobrescritura de encabezado de solicitud `x-edgeoptimize-api-key` = `YOUR_API_KEY`
* Sobrescritura de encabezado de solicitud `x-edgeoptimize-monitor` = `1`
* Anulación de configuración de ruta: grupo de origen → `edge-optimize-origin-group`, protocolo de reenvío → Coincidir con la solicitud entrante, almacenamiento en caché → **deshabilitado**

### Regla 3: HealthProbeRewrite03

Reescribe las solicitudes de sondeo de mantenimiento de puerta principal de Azure para que lleguen a su origen como `/` en lugar de como `/health/<domain>`. Esto permite que Azure Front Door supervise la disponibilidad de Edge Optimize sin requerir un punto final de estado específico en su origen. Dejar de evaluar: **El**.

![Regla de reescritura de sondeo de estado](/help/assets/optimize-at-edge/azure-front-door-ruleset-healthprobe.png)

**Condiciones** (todas deben coincidir):

* Ruta de URL de solicitud: **Comienza con** `/health/`
* `x-fd-healthprobe`: **Contiene** `1`

**Acciones**:

* Reescritura de URL — Patrón de Source: `/health/`, destino: `/`
* Sobrescritura del encabezado de respuesta `custom-origin-health` = `routed` (diagnóstico: se puede eliminar después de la verificación)
* Anexar encabezado de solicitud `user-agent` = ` AdobeEdgeOptimize/1.0` (agregar un espacio inicial — Azure Front Door anexa el valor tal cual)
* Anulación de configuración de ruta: grupo de origen → `default-origin-group`, protocolo de reenvío → Coincidir con la solicitud entrante, almacenamiento en caché → **deshabilitado**

## Paso 4: Asociar el conjunto de reglas con la ruta

Abra la ruta, desplácese hasta la sección **Reglas** de la parte inferior y seleccione el conjunto de reglas `EORouting` en la lista desplegable. Si tiene conjuntos de reglas existentes, use **Mover al principio** para colocar `EORouting` en **#1**. Las reglas de Optimización en Edge solo interceptan tráfico auténtico y solicitudes de bucle invertido de Optimización de Edge: el resto del tráfico pasa sin verse afectado por las demás reglas. Guarde y espere a que se propague (aproximadamente 20 minutos).

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

{{verify-routing-status-in-ui}}

{{return-to-overview}}
