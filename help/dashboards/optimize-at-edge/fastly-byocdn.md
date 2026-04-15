---
title: 'Optimizar en Edge: Fastly (BYOCDN)'
description: Aprenda a configurar Fastly BYOCDN para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 412500d2a95d66a5c9bf6fa88efc62c6244834c8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 5%

---


# Rápido (BYOCDN)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de configurar las reglas de VCL de Fastly, asegúrese de lo siguiente:

* Acceso a Fastly para su dominio.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.
* (Opcional) Para probar el enrutamiento de ensayo, consulte **Opcional: Prueba del enrutamiento en un nombre de host de ensayo** al final de esta página.

{{retrieve-byocdn-api-key}}

**Configuración**

Agregue los tres fragmentos de VCL siguientes al servicio Fastly. Estos fragmentos administran el enrutamiento de solicitudes auténticas a Edge Optimize, la separación de claves de caché y la conmutación por error al origen predeterminado.

![VCL de Fastly](/help/assets/optimize-at-edge/fastly-vcl.png)

![Añadir fragmentos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**fragmento vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;
unset req.http.x-edgeoptimize-fetcher-key; # Optional (required only in case of WAF)

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.http.x-edgeoptimize-fetcher-key = "<YOUR FETCHER KEY>"; # Optional (required only in case of WAF)
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

**Permitir la optimización en Edge mediante reglas de firewall (opcional)**

{{waf-allowlist-setup}}

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

{{verify-routing-status-in-ui}}

{{retrieve-staging-edge-optimize-api-key}}

```
curl -svo /dev/null https://staging.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

{{return-to-overview}}
