---
title: Optimizar en Edge
description: Obtenga información sobre cómo entregar optimizaciones en LLM Optimizer en el perímetro de la CDN sin necesidad de realizar cambios en la creación.
feature: Opportunities
source-git-commit: c1040edc78480f0df9ea3c29cc15009d0596941f
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 1%

---


# Optimizar en Edge

Esta página proporciona información general detallada sobre cómo entregar optimizaciones en el perímetro de CDN sin ningún cambio en la creación. Abarca el proceso de incorporación, las oportunidades de optimización disponibles y cómo optimizar automáticamente en Edge.

>[!NOTE]
>Actualmente, esta funcionalidad se encuentra en Acceso anticipado. Puede obtener más información acerca de los programas de acceso anticipado [aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## ¿Qué es Optimizar en Edge?

Optimizar en Edge es una capacidad de implementación basada en Edge en LLM Optimizer que sirve para realizar cambios prácticos de IA en los agentes de usuario de LLM. En el contexto actual, &quot;Edge&quot; significa que la optimización se aplica en la capa de CDN. Dado que ofrece optimizaciones en la capa de CDN, no se requieren cambios de creación en el sistema de administración de contenido (CMS), por lo que el CMS de origen permanece sin cambios. Esta separación le permite mejorar la visibilidad de LLM sin alterar los flujos de trabajo de publicación existentes. Se dirige únicamente al tráfico auténtico y no afecta ni a los usuarios humanos ni a los bots de SEO. Cuando LLM Optimizer detecta oportunidades para optimizar una página, los usuarios pueden implementar correcciones directamente en el perímetro de la CDN.

Optimizar en Edge es una alternativa más rápida y sencilla que las correcciones tradicionales que requieren esfuerzos de ingeniería complejos. Como se ha mencionado, una vez que complete una configuración única, no se requieren cambios de plataforma ni ciclos de desarrollo largos para aplicar los cambios. Puede publicar mejoras en minutos sin necesidad de participación del desarrollador. Es una forma sin código de optimizar el sitio web para los agentes de IA.

Optimizar en Edge está diseñado para usuarios empresariales en equipos de marketing, SEO, contenido y estrategia digital. Puede permitir a los usuarios empresariales completar el recorrido completo en LLM Optimizer: identificar oportunidades, comprender sugerencias e implementar fácilmente las correcciones. Con Optimizar en Edge, los usuarios pueden obtener una vista previa de los cambios, implementarlos rápidamente en CDN y validar que las optimizaciones estén activas. Se puede realizar un seguimiento del rendimiento en el ecosistema de LLM Optimizer.

### Ventajas principales

* **Envío solo de IA:** Sirve HTML optimizado solo para agentes de IA sin impacto en visitantes humanos ni en bots de SEO.
* **Ciclos más rápidos:** Publicar cambios en minutos, no en semanas. No se requieren cambios de plataforma ni ciclos de ingeniería largos.
* **Reversible:** Compatible con una capacidad de reversión de un clic que puede revertir la página en minutos.
* **Sin impacto en el rendimiento:** Las optimizaciones y el almacenamiento en caché basados en Edge no afectan la latencia del sitio.
* **No depende de CDN ni de CMS:** Funciona con cualquier configuración de CDN y configuración de front-end, independientemente del sistema de administración de contenido.

### ¿Qué oportunidades se admiten con Optimizar en Edge?

Las oportunidades que pueden mejorar la experiencia web auténtica se admiten con Optimizar en Edge. Obtenga más información acerca de cada oportunidad en la página [Tablero de oportunidades](/help/dashboards/opportunities.md) y en la sección de oportunidades de la página actual.

## Incorporación

Póngase en contacto con el equipo de su cuenta de Adobe o con el equipo de FDE para iniciar el proceso de incorporación. Su equipo de TI o CDN también tiene que completar los requisitos previos y el proceso de configuración. Además, también puede ponerse en contacto con `llmo-at-edge@adobe.com` para obtener más ayuda para la incorporación.

Requisitos previos para la incorporación a Optimize en Edge:

* Complete el proceso de incorporación a LLM Optimizer.
* Complete el proceso de reenvío de registros para los registros de CDN.

Requisitos para su equipo de TI/CDN:

* Genere una clave de API.
* Añada las reglas de enrutamiento Optimize at Edge en la CDN.
* Lista de permitidos de rutas definidas por el usuario para todo el dominio.
* Agregar una lista definida por el usuario de agentes de usuario LLM a destino.
* Asegúrese de que `robots.txt` no bloquee ningún agente de usuario destinado a destinatario.
* Confirme Optimización en el enrutamiento de Edge en la interfaz de LLM Optimizer.

Para guiar el proceso de configuración, que se presenta a continuación, hay configuraciones de muestra para una serie de configuraciones de CDN. Tenga en cuenta que estos ejemplos deben adaptarse a la configuración real en directo. Se recomienda aplicar primero los cambios en los entornos más bajos.

>[!BEGINTABS]

>[!TAB CDN administrado por Adobe]

**CDN administrado por Adobe**

El propósito de esta configuración es configurar las solicitudes con agentes de usuario agénticos que se enrutarán al servicio Optimizer (`live.edgeoptimize.net` backend). Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edge-optimize-request-id` en la respuesta.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edge-optimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

La configuración de enrutamiento se realiza mediante una regla de CDN [originSelector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). Los requisitos previos son los siguientes:

* decidir el dominio que se va a distribuir
* decida las rutas que desea enrutar
* decida los agentes de usuario que se van a enrutar (regex recomendado)

Para implementar la regla, debe hacer lo siguiente:

* crear una [canalización de configuración](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* confirmar el archivo de configuración `cdn.yaml` en su repositorio
* ejecutar la canalización de configuración


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
            - reqHeader: x-edge-optimize-request
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

Para probar la configuración, ejecute un curl y espere lo siguiente:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edge-optimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

<!-- >>[!TAB Akamai (BYOCDN)]

**Tokowaka BYOCDN - Akamai**

```
{
    "name": "Project Tokowaka CDN Rule",
    "children": [
        {
            "name": "Connection settings",
            "children": [],
            "behaviors": [
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.health-detect.status>off</forward:availability.health-detect.status>\n<forward:availability>\n<max-reforwards>1</max-reforwards>\n<max-reconnects>1</max-reconnects>\n</forward:availability>\n<match:forward.server-type value=\"CUSTOMER_ORIGIN\">\n<network:http.read>%(PMUSER_HTTP_READ)</network:http.read>\n<network:http.first-byte-timeout>%(PMUSER_FIRST_BYTE_TIMEOUT)</network:http.first-byte-timeout>\n<network:http.connect-timeout>%(PMUSER_HTTP_CONNECT_TIMEOUT)</network:http.connect-timeout> \n</match:forward.server-type>"
                    },
                    "uuid": "4a8c027b-1b23-44a7-8e12-f8d07e453679",
                    "templateUuid": "41c77091-419f-43f2-9a84-0b406b050cc8"
                }
            ],
            "uuid": "4759571b-8036-4c16-9b60-d3aeb84958f1",
            "criteria": [],
            "criteriaMustSatisfy": "all"
        },
        {
            "name": "Site Failover Behavior",
            "children": [],
            "behaviors": [
                {
                    "name": "failAction",
                    "options": {
                        "actionType": "RECREATED_CO",
                        "contentCustomPath": false,
                        "contentHostname": "www.adobe.com",
                        "enabled": true
                    }
                },
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.fail-action2>\n<add-header>\n<status>on</status>\n<name>x-tokowaka-request</name>\n<value>fo</value>\n</add-header>\n</forward:availability.fail-action2>"
                    }
                }
            ],
            "uuid": "b3000c12-1ab8-49b1-a5d0-75e58bb18c9c",
            "criteria": [
                {
                    "name": "matchResponseCode",
                    "options": {
                        "lowerBound": 400,
                        "matchOperator": "IS_BETWEEN",
                        "upperBound": 599
                    }
                },
                {
                    "name": "originTimeout",
                    "options": {
                        "matchOperator": "ORIGIN_TIMED_OUT"
                    }
                }
            ],
            "criteriaMustSatisfy": "any",
            "comments": "If Tokowaka origin returns a 4xx or 5xx error (or times out), failover condition is to send the request back to Akamai and set the x-tokowaka-request header so we don't re-send the request to Tokowaka"
        }
    ],
    "behaviors": [
        {
            "name": "origin",
            "options": {
                "cacheKeyHostname": "ORIGIN_HOSTNAME",
                "compress": true,
                "customValidCnValues": [
                    "{{Origin Hostname}}",
                    "{{Forward Host Header}}",
                    "*.tokowaka.now"
                ],
                "enableTrueClientIp": true,
                "forwardHostHeader": "ORIGIN_HOSTNAME",
                "hostname": "edge.tokowaka.now",
                "httpPort": 80,
                "httpsPort": 443,
                "ipVersion": "IPV4",
                "minTlsVersion": "DYNAMIC",
                "originCertificate": "",
                "originCertsToHonor": "STANDARD_CERTIFICATE_AUTHORITIES",
                "originSni": true,
                "originType": "CUSTOMER",
                "ports": "",
                "standardCertificateAuthorities": [
                    "akamai-permissive",
                    "THIRD_PARTY_AMAZON"
                ],
                "tlsVersionTitle": "",
                "trueClientIpClientSetting": true,
                "trueClientIpHeader": "True-Client-IP",
                "verificationMode": "CUSTOM"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_LLMCLIENT",
                "variableValue": "TRUE"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "caseSensitive": false,
                "extractLocation": "CLIENT_REQUEST_HEADER",
                "globalSubstitution": false,
                "headerName": "Accept-Language ",
                "regex": "^([a-zA-Z]{2}).*",
                "replacement": "$1",
                "transform": "SUBSTITUTE",
                "valueSource": "EXTRACT",
                "variableName": "PMUSER_LANG"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_X_FORWARDED_HOST",
                "variableValue": "{{builtin.AK_HOST}}"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY",
                "variableValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}};X_FORWARDED_HOST={{user.PMUSER_X_FORWARDED_HOST}}"
            }
        },
        {
            "name": "caching",
            "options": {
                "behavior": "CACHE_CONTROL_AND_EXPIRES",
                "cacheControlDirectives": "",
                "defaultTtl": "1d",
                "enhancedRfcSupport": false,
                "honorMustRevalidate": false,
                "honorPrivate": false,
                "mustRevalidate": false
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-tokowaka-api-key",
                "newHeaderValue": "<your api-key here>",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-config",
                "newHeaderValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-url",
                "newHeaderValue": "{{builtin.AK_URL}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "cacheId",
            "options": {
                "rule": "INCLUDE_VARIABLE",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY"
            }
        },
        {
            "name": "modifyIncomingResponseHeader",
            "options": {
                "action": "DELETE",
                "customHeaderName": "Age",
                "standardDeleteHeaderName": "OTHER"
            }
        },
        {
            "name": "prefreshCache",
            "options": {
                "enabled": true,
                "prefreshval": 90
            }
        },
        {
            "name": "modifyOutgoingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-Forwarded-Host",
                "newHeaderValue": "{{builtin.AK_HOST}}",
                "standardModifyHeaderName": "OTHER"
            }
        }
    ],
    "criteria": [
        {
            "name": "userAgent",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "IS_ONE_OF",
                "matchWildcard": true,
                "values": [
                    "*Tokowaka-AI*",
                    "*ChatGPT-User*",
                    "*GPTBot*",
                    "*OAI-SearchBot*"
                ]
            }
        },
        {
            "name": "path",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "MATCHES_ONE_OF",
                "normalize": false,
                "values": [
                ]
            }
        },
        {
            "name": "requestHeader",
            "options": {
                "headerName": "x-tokowaka-request",
                "matchOperator": "DOES_NOT_EXIST",
                "matchWildcardName": false
            }
        },
        {
            "name": "matchVariable",
            "options": {
                "matchCaseSensitive": true,
                "matchOperator": "IS",
                "matchWildcard": false,
                "variableExpression": "FALSE",
                "variableName": "PMUSER_TOKOWAKA_DISABLE"
            }
        }
    ],
    "criteriaMustSatisfy": "all"
}
```

Important considerations:

* Tokowaka Rule will be ON based on User-Agent + Path + x-tokowaka-request (if not present) + TOKOWAKA_DISABLE variable (to allow switch off using a single variable toggle)
* Set up rules to **Modify Incoming Request Headers** rule to set custom headers
* Set cache-key in Akamai using user defined variable through Cache-ID modification mechanism. Only a single user defined variable is allowed, so create a separate variable for cache_key and set it accordingly.
* Lang: extracted from Accept-Language header using "regex": "^([a-zA-Z]{2}).*"
* With Cache ID Modification within a match on User Agent, the content can't be purged by URL (just FYI)
* Site failover mechanism: With the match on User-Agent rule, Akamai does not allows to failover based on health check, but only only basis of origin response/connectivity per request. Set **x-tokowaka-fo:true**  resp header in case of failover response.
* SWR is not supported by Akamai. So, only TTL based caching is there. So, configure a rule in Akamai to strip Age header from origin response else TTL based caching would not work.
* Ensure that the Tokowaka rule is the bottom most rule in the rule hierarchy (so that it overrides all other rules).-->

>[!TAB Fastly (BYOCDN)]

**Edge Optimize BYOCDN - Fastly - VCL**

![VCL de Fastly](/help/assets/optimize-at-edge/fastly-vcl.png)

![Agregar fragmentos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**fragmento vcl_recv**

```
unset req.http.x-edge-optimize-url;
unset req.http.x-edge-optimize-config;
unset req.http.x-edge-optimize-api-key;

if (!req.http.x-edge-optimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edge-optimize-url = req.url; # required for identifying the original url
  set req.http.x-edge-optimize-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-edge-optimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**fragmento vcl_hash**

```
if (req.http.x-edge-optimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edge-optimize-config;
}
```

**vcl_deliver_snippet**

```
if (req.http.x-edge-optimize-config && resp.status >= 400) {
  set req.http.x-edge-optimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edge-optimize-config && req.http.x-edge-optimize-request == "failover") {
  set resp.http.x-edge-optimize-fo = "1";
}
```

>[!ENDTABS]

>[!NOTE]
>Para otros proveedores de CDN, póngase en contacto con `llmo-at-edge@adobe.com` para ayudar a sus equipos de TI/CDN en la incorporación. Una vez completadas las configuraciones, puede implementar sugerencias para Optimizar en las oportunidades de Edge en LLM Optimizer.

## Oportunidades

En la tabla siguiente se presentan las oportunidades que pueden mejorar la experiencia web auténtica y que son compatibles con Optimizar en Edge.

| Oportunidad | Tipo | Identificar automáticamente | Sugerencia automática | Optimización automática |
|---------|----------|----------|----------|----------|
| Recuperar visibilidad del contenido | GEO técnico | Detecta páginas donde se oculta contenido crítico a los agentes de IA. Muestra las direcciones URL afectadas y el contenido esperado que se puede recuperar. | Resalta el contenido que puede estar disponible para los agentes de IA y recomienda habilitar el procesamiento previo para esas páginas. | Proporciona una instantánea de HTML totalmente procesada y compatible con IA al tráfico auténtico que recupera el contenido oculto anteriormente. |
| Optimizar encabezados para LLM | Optimización de contenido | Analiza encabezados para detectar encabezados vacíos, duplicados, ausentes o ambiguos que pueden reducir la legibilidad del equipo. | Propone una jerarquía de encabezados más limpia y etiquetas mejoradas, y muestra una previsualización de la estructura actualizada para cada página. | Inserta la estructura de encabezado mejorada para los agentes de IA, preservando el diseño visual al mismo tiempo que hace que la página sea más legible para los LLM. |
| Agregar resúmenes compatibles con LLM | Optimización de contenido | Identifica páginas largas o complejas que carecen de resúmenes concisos en el nivel de página o sección, lo que dificulta que la inteligencia artificial las analice y comprenda rápidamente. | Recomienda resúmenes cortos generados por IA en el nivel de página y sección que capturan contenido clave. | Inserta los resúmenes en las secciones relevantes de HTML, lo que mejora la forma en que los modelos interpretan y describen el contenido de la página. |
| Añadir preguntas frecuentes relevantes | Optimización de contenido | Detecta lagunas de intención en el contenido de la página existente que podrían beneficiarse de las preguntas frecuentes. | Sugiere contenido de preguntas más frecuentes generado por IA alineado con la intención del usuario y los temas existentes. | Inserta contenido de preguntas frecuentes en HTML, lo que hace que las páginas sean más reconocibles y relevantes en respuestas impulsadas por IA. |
| Simplificar contenido complejo | Optimización de contenido | Indica páginas con texto complejo que puede dificultar la comprensión de la IA. | Proporciona versiones simplificadas de texto complejo generadas por IA preservando al mismo tiempo el significado original. | Reescribe secciones complejas en la página, lo que mejora la legibilidad de la IA. |

### Herramientas adicionales

La [Adobe LLM Optimizer: ¿Es citable su página web?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) La extensión de Chrome muestra la cantidad de contenido web al que pueden acceder los LLM y lo que permanece oculto. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración.

Con un solo clic, puede evaluar la legibilidad automática de cualquier sitio. Puede ver una comparación en paralelo de lo que ven los agentes de IA frente a lo que ven los usuarios humanos y estimar cuánto contenido se puede recuperar mediante LLM Optimizer. Ver [¿Puede AI leer su sitio web?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) página para obtener más información.

## Oportunidades detalladas

En las secciones siguientes, puede ver detalles adicionales de cada oportunidad admitida con Optimizar en Edge.

### Recuperar visibilidad del contenido

Esta oportunidad marca páginas donde el contenido clave está oculto para los agentes de IA debido al procesamiento en el lado del cliente. Para cada página identificada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta los huecos de visibilidad y le permite aplicar cambios directamente para recuperar el contenido oculto. Al implementar esta oportunidad con Optimizar en Edge, se proporciona una versión de la página procesada previamente y optimizada para IA a los agentes de usuario de LM para que puedan acceder al contexto completo sin ejecutar JavaScript.
Esto garantiza que la página sea primero totalmente visible para los agentes de IA. Además de ese HTML preprocesado, se aplican mejoras adicionales.

>[!IMPORTANT]
>Esta capacidad de procesamiento previo se aplica automáticamente a todas las oportunidades que se presentan a continuación cuando se implementa con Optimizar en Edge para garantizar que la página sea totalmente visible para los agentes de IA.

### Optimizar encabezados para LLM

Esta oportunidad detecta páginas en las que la estructura de encabezados dificulta que los agentes de IA comprendan la página debido a encabezados vacíos, duplicados, inexistentes o ambiguos. Para cada página afectada, la oportunidad muestra los encabezados subóptimos y recomienda una jerarquía más clara. Cuando se implementa con Optimizar en Edge, los encabezados mejorados se aplican en HTML servido al tráfico auténtico. Esto ayuda a la legibilidad de la máquina mientras que el diseño de la cara humana permanece igual.

### Agregar resúmenes compatibles con LLM

Esta oportunidad identifica las páginas que pueden beneficiarse de resúmenes concisos para ayudar a los LLM a comprender rápidamente de qué trata el contenido de la página. Para cada página, la oportunidad detecta dónde más se necesita un resumen y crea resúmenes generados por IA en el nivel de página o de sección. Al implementar con Optimizar en Edge, estos resúmenes se insertan en HTML que los agentes de IA recuperan, lo que mejora las posibilidades de que el contenido se describa con más precisión.

### Añadir preguntas frecuentes relevantes

Esta oportunidad marca páginas en las que el contenido adicional de preguntas y respuestas podría coincidir mejor con la intención del usuario y las indicaciones de la detección controlada por IA. Para cada página, propone bloques de preguntas más frecuentes generados por IA vinculados a la intención y el contenido del usuario en la página. Con Optimizar en Edge, estas preguntas frecuentes se insertan en HTML, lo que hace que su página sea más compatible con IA y aumenta la probabilidad de que las respuestas de IA reflejen directamente sus directrices.

### Simplificar contenido complejo

Esta oportunidad encuentra páginas con párrafos largos y complejos que pueden reducir la comprensión de IA. Para cada página que supera los umbrales de legibilidad, crea contenido generado por IA que es más sencillo y fácil de analizar, conservando al mismo tiempo el significado original. Cuando se implementa en el perímetro de, el contenido simplificado entregado al tráfico auténtico ayuda a los LLM a interpretar y resumir el contenido de forma más fiel.

## Optimización automática en Edge

Para cada oportunidad, puede obtener una vista previa, editar, implementar, ver en directo y revertir las optimizaciones en el perímetro de.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Vista previa

**Vista previa** le permite ver el impacto de una sugerencia antes de que se ponga en marcha. Aparece una diferencia en paralelo entre la página actual y la versión optimizada para IA que se espera después de aplicar la sugerencia. Esta vista utiliza la misma lógica de Optimizar en Edge que activará el tráfico en directo, pero en un modo de vista previa aislado. Esto no afecta al tráfico en directo, ya que es una simulación de solo lectura para revisión.

![Vista previa](/help/assets/optimize-at-edge/preview.png)

### Editar

**Editar** le permite refinar o reescribir por completo la sugerencia generada automáticamente antes de implementarla. En lugar de aceptar la sugerencia, mantiene un control total a través del flujo de trabajo de edición. La vista muestra los cambios propuestos en un editor estructurado, donde puede modificar el texto para que coincida mejor con la intención original. La versión editada se proporcionará a los agentes de IA una vez implementada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implementación

**Implementar** publica las sugerencias seleccionadas para que las experiencias optimizadas se puedan ofrecer desde el perímetro a los agentes de IA. Si la CDN está completamente enrutada, todas las páginas del dominio suelen mostrarse con los nuevos cambios en cuestión de minutos. Si el enrutamiento solo se ha configurado para rutas seleccionadas, solo las páginas incluidas en la lista de permitidos se activan con las optimizaciones.

![Implementar](/help/assets/optimize-at-edge/deploy.png)

### Ver activo

**Ver en vivo** le permite verificar que la optimización está activa y que se comporta según lo esperado para el tráfico auténtico, una vista a la que de otra manera sería difícil acceder. Puede ver la página activa en Sugerencias fijas, que procesa la página como se muestra a los agentes de IA.

![Ver activo](/help/assets/optimize-at-edge/view-live.png)

### Reversión

La reversión de forma segura revierte una optimización implementada anteriormente. La versión de solo IA de la página suele volver a su estado anterior en cuestión de minutos, lo que permite experimentar con optimizaciones cuando es necesario.

![Reversión](/help/assets/optimize-at-edge/rollback.png)

## Preguntas frecuentes

P. ¿Qué tipo de LLM dirige con Optimizar en Edge?

Usted define la lista de agentes de usuario a los que dirigirse durante el proceso de incorporación.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

P. ¿Qué sucede si todavía no estoy incorporado a Optimize en Edge?

Si hace clic en **Implementar optimizaciones** antes de completar la configuración necesaria, no se aplicará nada al sitio. En su lugar, un cuadro de diálogo emergente le pedirá que se ponga en contacto con nuestro equipo en `llmo-at-edge@adobe.com` para obtener ayuda sobre la incorporación. Hasta que se complete la incorporación, aún puede explorar las oportunidades y sugerencias detectadas, pero el flujo de trabajo de implementación con un solo clic permanecerá inactivo.

P: ¿Qué sucede cuando el contenido se actualiza en el origen?

Servimos la versión optimizada de la página desde la caché siempre y cuando la página de origen subyacente no haya cambiado. Sin embargo, cuando la fuente cambia, nuestro sistema se actualiza automáticamente para que los agentes de IA siempre reciban el contenido más actualizado. Esto se debe a que utilizamos la configuración de tiempo de duración de caché (TTL) bajo (por orden de minutos) para que cualquier actualización de contenido en su sitio déclencheur una nueva optimización dentro de esa ventana. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. ¿Optimizar en Edge solo es para sitios que utilizan el servicio de entrega perimetral de Adobe (EDS)?

No. Optimizar en Edge no depende de la red de distribución de contenido (CDN) y funciona con cualquier arquitectura de front-end, no solo con las implementadas en la pila EDS de Adobe.

P. ¿En qué se diferencia Optimizar en el procesamiento previo de Edge del procesamiento tradicional del lado del servidor (SSR)?

Ambos resuelven diferentes problemas y pueden trabajar juntos. La SSR tradicional procesa contenido del lado del servidor, pero no incluye contenido cargado posteriormente en el explorador. Optimizar en Edge: la renderización previa captura la página después de que JavaScript y los datos del lado del cliente se hayan cargado, lo que produce la versión completamente ensamblada en el perímetro de CDN. SSR se centra en mejorar la experiencia humana y Optimizar en Edge mejora la experiencia web para los LLM.
