---
title: 'Optimizar en Edge: servidor HTTP de Apache'
description: Obtenga información sobre cómo configurar Apache HTTP Server (proxy inverso autoalojado) BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: d7e723161836027dcdde931378f5d0f776a1ecfc
workflow-type: tm+mt
source-wordcount: 585
ht-degree: 32%

---


# Apache HTTP Server

Esta configuración se aplica cuando Apache HTTP Server actúa como proxy inverso delante de su origen (una configuración autoalojada, **sin** AEM Dispatcher). Enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

La integración es un conjunto de archivos Apache `Include` nativos; no hay código ni trabajador para implementar. Descarga tres archivos, establece tu clave de API y agrega dos líneas de `Include` a tu host virtual.

**Requisitos previos**

Antes de configurar las reglas de enrutamiento de Apache, asegúrese de lo siguiente:

* Apache HTTP Server 2.4 o posterior con estos módulos habilitados: `proxy`, `proxy_http`, `ssl`, `rewrite`, `headers`, `env` y `setenvif`.
* Acceso a la configuración de Apache (el `<VirtualHost>` para su sitio) y la capacidad de volver a cargar Apache.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Configuración

**1. Descargar los archivos de configuración**

Descargue los tres archivos de inclusión de Edge Optimize del repositorio de muestras de código de [Optimize at Edge](https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/apache) y colóquelos en un directorio de su servidor Apache (por ejemplo, `conf/oae/`):

| Archivo | Función |
|------|---------|
| `oae-routing.conf` | Detecta bots de IA, inserta encabezados de Edge Optimize, enruta las solicitudes de página de HTML al servidor y configura el aislamiento de caché y la conmutación por error. |
| `oae-failover.conf` | Reproduce la solicitud original con el origen si Edge Optimize devuelve un error. |
| `domains.conf` | Habilita Optimizar en Edge por dominio y contiene su clave de API. |

No necesita modificar `oae-routing.conf` o `oae-failover.conf`, utilícelos tal cual.

**2. Habilite su dominio y establezca la clave de API (`domains.conf`)**

Edite `domains.conf` y agregue una línea por cada dominio que esté habilitando. Reemplace el host por su dominio y `YOUR_API_KEY` por la clave de la interfaz de usuario de LLM Optimizer. Los dominios no enumerados se dirigen al origen sin cambios, por lo que puede habilitar un dominio a la vez.

```
SetEnvIfExpr "%{HTTP_HOST} =~ m#(?i)^(www\.)?example\.com(:\d+)?$#" OAE_DOMAIN_ENABLED=1 OAE_API_KEY=YOUR_API_KEY
```

**3. Incluir los archivos en el host virtual**

Agregue las dos `Include` líneas a su `<VirtualHost *:443>` existente. El archivo de enrutamiento se va **antes** de la reescritura y las reglas de `ProxyPass`; el archivo de conmutación por error se va **después** de ellas. En el ejemplo siguiente, las líneas marcadas `#NEWLINE` son las únicas que agrega para Optimizar en Edge; todo lo demás (`ServerName`, `ProxyPass` y el resto) es la configuración existente sin modificar.

```
Define OAE_CONF_DIR conf/oae                       #NEWLINE  directory holding the OAE include files

<VirtualHost *:443>
    ServerName www.example.com

    Include "${OAE_CONF_DIR}/oae-routing.conf"     #NEWLINE  OAE routing — BEFORE your Rewrite & ProxyPass rules

    # --- your existing rewrite rules and ProxyPass to origin ---
    ProxyPass        "/" "https://www.example.com/"
    ProxyPassReverse "/" "https://www.example.com/"

    Include "${OAE_CONF_DIR}/oae-failover.conf"    #NEWLINE  OAE failover — AFTER your ProxyPass rules
</VirtualHost>
```

**4. Volver a cargar Apache**

Valide la configuración y vuelva a cargar Apache para aplicar los cambios.

>[!NOTE]
>
>Las respuestas humanas y optimizadas para bots se guardan automáticamente en entradas de caché independientes (el archivo de enrutamiento establece `Vary: x-edgeoptimize-config`). Si su Apache ya utiliza `mod_cache`, asegúrese de que tenga `CacheQuickHandler Off` para que la búsqueda en la caché se ejecute después de establecer los encabezados de Edge Optimize.

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
