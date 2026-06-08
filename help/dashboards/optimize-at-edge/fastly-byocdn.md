---
title: 'Optimizar en Edge: Fastly (BYOCDN)'
description: Obtenga información sobre cómo configurar Fastly BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:51:24.924Z'
TQID: 'https://experienceleague.adobe.com/qXp1pbmZrxahHFOUzIuo-WEawdgNWIIQKDyy0yL2MLA'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: c5a8f033aac85913b56a40bb1560537da04847f2
workflow-type: tm+mt
source-wordcount: 350
ht-degree: 96%

---


# Fastly (BYOCDN)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de VCL de Fastly, asegúrese de lo siguiente:

* Tener acceso a Fastly para su dominio.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Configuración**

Añada los tres fragmentos de VCL siguientes a su servicio de Fastly. Estos fragmentos administran las solicitudes del enrutamiento de las solicitudes agénticas a Edge Optimize, la separación de claves de caché y la conmutación por error a su origen predeterminado.

![Configuración de servidor rápida](/help/assets/optimize-at-edge/fastly-backend-config.png)

![Añadir fragmentos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**fragmento vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;
unset req.http.x-edgeoptimize-fetcher-key; # Optional (required only in case of WAF)

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User|ClaudeBot|Claude-User|Claude-SearchBot)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.http.x-edgeoptimize-fetcher-key = "<YOUR FETCHER KEY>"; # Optional (required only in case of WAF)
  set req.backend = F_EDGE_OPTIMIZE;
  return(lookup);
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
  restart;
}

if (req.http.x-edgeoptimize-config) {
  return(deliver);
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**Conmutación por error**

El fragmento `vcl_deliver` administra la conmutación por error automáticamente. Si Edge Optimize devuelve un error `4XX` o `5XX`, la solicitud se reinicia y se redirige de nuevo al origen predeterminado para que el usuario final siga recibiendo una respuesta. Las respuestas de conmutación por error incluyen el encabezado `x-edgeoptimize-fo: 1`.

| Escenario | Comportamiento |
| --- | --- |
| Edge Optimize devuelve `2XX` | Se sirve una respuesta optimizada al cliente. |
| Edge Optimize devuelve `4XX` o `5XX` | La solicitud se reinicia y se sirve desde el origen predeterminado. |
| Respuesta de conmutación por error | Incluye el encabezado `x-edgeoptimize-fo: 1`. |

**Permitir Optimizar en Edge mediante reglas de cortafuegos (opcional)**

{{waf-allowlist-setup}}

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
