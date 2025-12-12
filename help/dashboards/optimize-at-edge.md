---
title: Optimizar en Edge
description: Obtenga información sobre cómo entregar optimizaciones en LLM Optimizer en el perímetro de la CDN sin necesidad de realizar cambios en la creación.
feature: Opportunities
source-git-commit: 3c6f287b3c3787cee95f99b7031412f26692a88b
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---


# Optimizar en Edge

Esta sección...

## ¿Qué es Optimizar en Edge?

Optimizar en Edge es una capacidad de implementación basada en Edge en LLM Optimizer que puede proporcionar cambios compatibles con IA a los agentes de usuario de LLM. Dado que ofrece optimizaciones en el perímetro de la CDN, no se requieren cambios de creación en el sistema de administración de contenido (CMS). También se dirige únicamente al tráfico real y no afecta a los usuarios humanos ni a los bots de SEO.

Cuando LLM Optimizer detecta oportunidades para optimizar una página, los usuarios pueden implementar correcciones directamente en el perímetro de sin necesidad de realizar cambios en la plataforma.

Esta capacidad se encuentra actualmente en Acceso anticipado.

## ¿Por qué debería interesar a un cliente?

Optimizar en Edge es una alternativa más rápida y sencilla que las correcciones tradicionales que requieren esfuerzos de ingeniería complejos. Una vez que los clientes completan una configuración única, no se requieren cambios de plataforma ni ciclos de desarrollo largos para aplicar los cambios a las páginas web. El usuario puede publicar mejoras en minutos, no en semanas, sin requerir la participación del desarrollador. Esta es una forma de bajo riesgo y sin código de optimizar su sitio web para los agentes de IA.

### Ventajas clave y propuesta de valor

* **Envío solo de IA:** Sirve HTML optimizado para agentes de IA solamente sin impacto en visitantes humanos o bots de SEO.
* **Ciclos más rápidos:** Publicar cambios en minutos, no en semanas. No se requieren cambios de plataforma ni ciclos de ingeniería largos.
* **De bajo riesgo y reversible:** Compatible con la función de reversión con un solo clic que puede revertir la página en minutos.
* **Sin impacto en el rendimiento:** Las optimizaciones y el almacenamiento en caché basados en Edge no afectan la latencia del sitio.
* **No depende de CDN ni de CMS:** Funciona con cualquier configuración de CDN y configuración de front-end, independientemente de CMS.

## ¿Quién debería usarlo?

Optimizar en Edge está diseñado para usuarios empresariales en equipos de marketing, SEO, contenido y estrategia digital. Puede permitir a los usuarios empresariales completar el recorrido completo en LLM Optimizer: identificar oportunidades, comprender sugerencias e implementar fácilmente las correcciones. Con Optimizar en Edge, los usuarios pueden obtener una vista previa de los cambios, implementarlos rápidamente en el perímetro y validar que las optimizaciones estén activas. Se puede realizar un seguimiento del rendimiento en el ecosistema de LLM Optimizer.

## ¿Qué oportunidades se han optimizado en Edge?

Las oportunidades que pueden mejorar la experiencia web auténtica se admiten con Optimizar en Edge. Obtenga más información sobre cada oportunidad en la sección [Oportunidades](/help/dashboards/opportunities.md).

## Incorporación

Puede activar Optimizar en Edge después de haber incorporado LLM Optimizer y de haber reenviado los registros de CDN.

Se necesita un ingeniero de CDN para completar la configuración inicial y habilitar Optimizar en Edge.

Requisitos para la instalación:

* Genere una clave de API.
* Añada las reglas de enrutamiento Optimize at Edge en la CDN.
* Lista de permitidos de rutas definidas por el usuario para todo el dominio.
* Agregar una lista definida por el usuario de agentes de usuario LLM a destino.
* Asegúrese de que robots.txt no bloquee ningún agente de usuario destinado a segmentar.
* Confirme que el enrutamiento Optimizar en Edge se encuentra en la interfaz de usuario de LLM Optimizer.

Adobe proporciona fragmentos de configuración de muestra para la mayoría de las CDN principales para guiar el proceso de instalación. Los ejemplos de fragmento incluidos en nuestras directrices deben adaptarse a la configuración en directo real. Adobe recomienda implementar primero los cambios en los entornos más bajos.

>[!BEGINTABS]

>[!TAB CDN administrada por AEM Cloud Service (rápidamente)]

**Tokowaka BYOCDN - CDN administrada por Adobe**

Utiliza solo originSelectors para seleccionar el origen Tokowaka.

El siguiente ejemplo enruta las solicitudes de los agentes LLM en un dominio específico que coincide con el patrón &quot;/es/*&quot; o las rutas exactas (solo se enruta a las páginas HTML). Se supone que el ejemplo proporciona un punto de partida y, en caso de que tenga varios originSelectors en la configuración, se recomienda colocarlo primero.

Notas importantes:

* La solicitud x-tokowaka debe comprobarse antes de enrutar al backend de Tokowaka. Solo las solicitudes que no tengan este encabezado deben enrutarse al backend de Tokowaka.
* la regla originSelector que dirige al backend de Tokowaka debería estar primero en la lista si hay varias reglas.
* El secreto TOKOWAKA_API_KEY debe implementarse antes de implementar el cdn.yaml

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Tokowaka backend
  originSelectors:
    rules:
      - name: route-to-tokowaka-backend
        when:
          allOf:
            - reqHeader: x-tokowaka-request
              exists: false # avoid loops when requests comes from Tokowaka
            - reqHeader: user-agent
              matches: "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: tokowaka-backend
          headers:
            x-tokowaka-api-key: "${{TOKOWAKA_API_KEY}}"
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"
```

>[!TAB Akamai (BYOCDN)]

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

Consideraciones importantes:

* La regla Tokowaka estará ON basada en la variable User-Agent + Path + x-tokowaka-request (si no está presente) + TOKOWAKA_DISABLE (para permitir el apagado con una sola opción de variable)
* Configure reglas para **Modificar encabezados de solicitud entrantes** para establecer encabezados personalizados
* Establezca la clave de caché en Akamai utilizando la variable definida por el usuario a través del mecanismo de modificación Cache-ID. Solo se permite una variable definida por el usuario, por lo que debe crear una variable independiente para cache_key y establecerla en consecuencia.
* Idioma: extraído del encabezado Accept-Language mediante &quot;regex&quot;: &quot;^([a-zA-Z]{2}).*&quot;
* Con la modificación del ID de caché dentro de una coincidencia en el agente de usuario, el contenido no se puede purgar por dirección URL (solo para su información)
* Mecanismo de conmutación por error del sitio: con la coincidencia en la regla de agente de usuario, Akamai no permite la conmutación por error en función de la comprobación de estado, sino solo en función de la respuesta de origen/conectividad por solicitud. Establecer el encabezado de resp **x-tokowaka-fo:true** en caso de respuesta de conmutación por error.
* Akamai no admite SWR. Por lo tanto, solo el almacenamiento en caché basado en TTL está allí. Por lo tanto, configure una regla en Akamai para eliminar el encabezado Age de la respuesta de origen; de lo contrario, el almacenamiento en caché basado en TTL no funcionaría.
* Asegúrese de que la regla Tokowaka sea la regla que se encuentre más abajo en la jerarquía de reglas (de modo que anule todas las demás reglas).

>[!TAB Fastly (BYOCDN)]

**Tokowaka BYOCDN - Fastly - VCL**

![VCL de Fastly](/help/assets/optimize-at-edge/fastly-vcl.png)

![Agregar fragmentos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**fragmento vcl_recv**

```
unset req.http.x-tokowaka-url;
unset req.http.x-tokowaka-config;
unset req.http.x-tokowaka-api-key;

if (!req.http.x-tokowaka-request
    && req.http.user-agent ~ "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-tokowaka-url = req.url; # required for identifying the original url
  set req.http.x-tokowaka-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-tokowaka-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_Tokowaka;
}
```

**fragmento vcl_hash**

```
if (req.http.x-tokowaka-config) {
  set req.hash += "tokowaka";
  set req.hash += req.http.x-tokowaka-config;
}
```

**vcl_deliver_snippet**

```
if (req.http.x-tokowaka-config && resp.status >= 400) {
  set req.http.x-tokowaka-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-tokowaka-config && req.http.x-tokowaka-request == "failover") {
  set resp.http.x-tokowaka-fo = "1";
}
```

>[!ENDTABS]


Para otros proveedores de CDN, póngase en contacto con llmo-at-edge@adobe.com para ayudar a sus equipos de TI/CDN en la incorporación.

<!--This should probably be included Opportunities dashboard content. Content also needs serious editing - lots of "customer needs"and business user" etc.-->

Una vez completadas las configuraciones, los usuarios empresariales pueden implementar sugerencias para Optimizar en las oportunidades de Edge en LLM Optimizer.

## Oportunidades

| Oportunidad | Tipo | Identificar automáticamente | Sugerencia automática | Optimización automática |
|---------|----------|----------|----------|----------|
| Recuperar visibilidad del contenido | GEO técnico | Detecta páginas donde se oculta contenido crítico a los agentes de IA. Muestra las direcciones URL afectadas y el contenido esperado que se puede recuperar. | Resalta el contenido que puede estar disponible para los agentes de IA y recomienda habilitar el procesamiento previo para esas páginas. | Proporciona una instantánea de HTML totalmente procesada y compatible con IA al tráfico auténtico que recupera el contenido oculto anteriormente. |
| Optimización de encabezados para IA | Optimización de contenido | Analiza los encabezados para detectar encabezados vacíos, duplicados, que faltan o ambiguos que pueden reducir la legibilidad del equipo. | Propone una jerarquía de encabezados más limpia y etiquetas mejoradas, y muestra una previsualización de la estructura actualizada para cada página. | Inserta la estructura de encabezado mejorada para los agentes de IA, preservando su diseño visual al mismo tiempo que hace que la página sea más comprensible para los LLM. |
| Agregar resúmenes compatibles con IA | Optimización de contenido | Identifica páginas largas o complejas que carecen de resúmenes concisos en el nivel de página o sección, lo que dificulta que la inteligencia artificial las analice y comprenda rápidamente. | Recomienda resúmenes cortos generados por IA en el nivel de página y de sección que capturan contenido clave. | Inserta los resúmenes en las secciones relevantes de HTML, lo que mejora la forma en que los modelos interpretan y describen el contenido de la página. |
| Añadir preguntas frecuentes relevantes | Optimización de contenido | Detecta lagunas de intención en el contenido de la página existente que podrían beneficiarse de las preguntas frecuentes. | Sugiere contenido de preguntas más frecuentes generado por IA y alineado con las intenciones del usuario y los temas existentes. | Inserta contenido de preguntas frecuentes en HTML, lo que hace que las páginas sean más reconocibles y relevantes en respuestas impulsadas por IA. |
| Simplificar contenido complejo | Optimización de contenido | Indica páginas con texto complejo que puede dificultar la comprensión de la IA. | Proporciona versiones simplificadas de pruebas complejas generadas por IA, a la vez que conserva el significado original. | Reescribe secciones complejas en la página, lo que mejora la legibilidad de la IA. |

### Recuperar visibilidad del contenido

Esta oportunidad marca páginas donde el contenido clave está oculto para los agentes de IA debido al procesamiento en el lado del cliente. Para cada página identificada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta los huecos de visibilidad y le permite aplicar cambios directamente para recuperar el contenido oculto. Al implementar esta oportunidad con Optimizar en Edge, se proporciona una versión de la página procesada previamente y optimizada para IA a los agentes de usuario de LM para que puedan acceder al contexto completo sin ejecutar JavaScript.

**Esta capacidad de procesamiento previo se aplica automáticamente a todas las oportunidades que siguen cuando se implementan con Optimizar en Edge.**: esto garantiza que la página sea totalmente visible para los agentes de IA en primer lugar. Además de ese HTML preprocesado, se aplican mejoras adicionales.

#### Herramientas adicionales

¿Es citable su página web? La [Adobe LLM Optimizer: ¿Es citable su página web?La extensión de Chrome ](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) le permite ver exactamente a qué parte del contenido de su página web pueden acceder los LLM y qué elementos permanecen ocultos. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración.

Con un solo clic, puede evaluar la legibilidad automática de cualquier sitio, ver una comparación paralela de lo que ven los agentes de IA frente a lo que ven los usuarios humanos y estimar cuánto contenido se puede recuperar con LLM Optimizer. Ver [¿Puede AI leer su sitio web?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obtener más información.

### Optimizar encabezados para LLM

Esta oportunidad detecta páginas en las que la estructura de encabezados dificulta que los agentes de IA comprendan la página debido a encabezados vacíos, duplicados, inexistentes o ambiguos. Para cada página afectada, la oportunidad muestra los encabezados subóptimos y recomienda una jerarquía más clara. Cuando se implementa con Optimizar en Edge, los encabezados mejorados se aplican en HTML servido al tráfico auténtico, lo que puede ayudar a mejorar la legibilidad de la máquina, sin modificar el diseño orientado a las personas.

### Agregar resúmenes compatibles con LLM

Esta oportunidad identifica las páginas que pueden beneficiarse de resúmenes concisos para ayudar a los LLM a entender rápidamente de qué trata la página. Para cada página, la oportunidad detecta dónde se necesita más un resumen y crea resúmenes generados por IA en el nivel de página o de sección. Al implementar con Optimizar en Edge, estos resúmenes se insertan en HTML que los agentes de IA recuperan, lo que mejora las posibilidades de que el contenido se describa con más precisión.

### Añadir preguntas frecuentes relevantes

Esta oportunidad marca páginas en las que el contenido adicional de preguntas y respuestas podría coincidir mejor con la intención del usuario y las indicaciones en el descubrimiento controlado por IA. Para cada página, propone bloques de preguntas más frecuentes generados por IA vinculados a la intención y el contenido del usuario en la página. Con Optimizar en Edge, estas preguntas frecuentes se insertan en HTML, lo que hace que su página sea más compatible con IA y aumenta la probabilidad de que las respuestas de IA reflejen directamente sus directrices.

### Simplificar contenido complejo

Esta oportunidad encuentra páginas con párrafos largos y complejos que pueden reducir la comprensión de IA. Para cada página que supera los umbrales de legibilidad, crea contenido generado por IA que es más sencillo y fácil de analizar, a la vez que preserva el significado original. Cuando se implementa en el perímetro de, el contenido simplificado entregado al tráfico auténtico ayuda a los LLM a interpretar y resumir el contenido de forma más fiel.

## Sugerencias

Para cada oportunidad, puede obtener una vista previa, editar, implementar, previsualizar en directo y revertir las optimizaciones en el perímetro de.

### Vista previa

La vista previa permite a los usuarios ver el impacto de una sugerencia en la página antes de que todo se active. Aparece una diferencia en paralelo entre la página actual y la versión optimizada para IA que se espera después de aplicar la sugerencia. Esta vista utiliza la misma lógica Optimizar en Edge que activará el tráfico en directo, pero en un modo de vista previa seguro y aislado. Esto no afecta al tráfico en directo, ya que es una simulación de solo lectura para revisión.

![Vista previa](/help/assets/optimize-at-edge/preview.png)

### Editar

Editar permite a los usuarios refinar o reescribir por completo la sugerencia generada automáticamente antes de implementarla. En lugar de aceptar pasivamente la sugerencia, los usuarios mantienen un control total a través de este flujo de trabajo &quot;humano en el bucle&quot;. La vista muestra los cambios propuestos en un editor estructurado, donde los usuarios pueden modificar el texto para que coincida mejor con su intención. La versión editada se proporcionará a los agentes de IA una vez implementada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implementación

Implementar publica las sugerencias seleccionadas para que las experiencias optimizadas se puedan ofrecer desde el perímetro a los agentes de IA. Si la CDN está completamente enrutada, todas las páginas del dominio se activan con los nuevos cambios, generalmente en cuestión de minutos. Si el enrutamiento solo se ha configurado para rutas seleccionadas, solo las páginas incluidas en la lista de permitidos se activan con las optimizaciones.

![Implementar](/help/assets/optimize-at-edge/deploy.png)

### Ver activo

Ver en directo permite a los usuarios verificar que la optimización está activa y se comporta según lo esperado para el tráfico auténtico, una vista a la que, de lo contrario, sería difícil acceder. Los usuarios pueden ver la página activa en Sugerencias fijas, lo que procesa la página como se muestra a los agentes de IA.

![Ver activo](/help/assets/optimize-at-edge/view-live.png)

### Reversión

La reversión de forma segura revierte una optimización implementada anteriormente. La versión solo de IA de la página suele volver a su estado anterior en cuestión de minutos, lo que permite a los usuarios experimentar con optimizaciones si es necesario.

![Reversión](/help/assets/optimize-at-edge/rollback.png)

## Preguntas frecuentes

P. ¿Qué tipo de LLM dirige con Optimizar en Edge?

El cliente define completamente la lista de agentes de usuario a los que dirigirse durante la incorporación.

P. ¿Qué significa &quot;Edge&quot; en Optimizar en Edge?

En nuestro contexto, &quot;Edge&quot; significa que la optimización se aplica en la capa de CDN y no dentro de su CMS.

P. ¿Por qué esta optimización requiere una CDN?

La CDN es donde se ensambla la versión optimizada de la página y se envía a los agentes de IA. Aprovechamos la CDN para garantizar que CMS original se mantenga sin cambios. Esta separación le permite mejorar la visibilidad de LLM sin alterar los flujos de trabajo de publicación existentes.

P. ¿Qué sucede si todavía no estoy incorporado a Optimize en Edge?

Si hace clic en **Implementar optimizaciones** antes de completar la configuración necesaria, no se aplicará nada al sitio. En su lugar, un cuadro de diálogo emergente le pedirá que se ponga en contacto con nuestro equipo en llmo-at-edge@adobe.com para obtener ayuda sobre la incorporación. Hasta que se complete la incorporación, aún puede explorar las oportunidades y sugerencias detectadas, pero el flujo de trabajo de implementación con un solo clic permanecerá inactivo.

P: ¿Qué sucede cuando el contenido se actualiza en el origen?

Servimos la versión optimizada de la página desde la caché siempre y cuando la página de origen subyacente no haya cambiado. Sin embargo, cuando la fuente cambia, nuestro sistema se actualiza automáticamente para que los agentes de IA siempre reciban el contenido más actualizado. Esto se debe a que utilizamos TTL de caché baja en orden de minutos, de modo que cualquier actualización de contenido en el sitio déclencheur una nueva optimización dentro de esa ventana. Como no hay un TTL universal que se ajuste a cada sitio, podemos configurarlo en función de las reglas de invalidación de la caché para garantizar que ambos sistemas permanezcan sincronizados.

P. ¿Optimizar en Edge solo es para sitios que utilizan el servicio de entrega perimetral de Adobe (EDS)?

No. Optimizar en Edge no depende de la red de distribución de contenido (CDN) y funciona con cualquier arquitectura de front-end, no solo con las implementadas en la pila EDS de Adobe.

P. ¿En qué se diferencia Optimizar en el procesamiento previo de Edge del procesamiento tradicional del lado del servidor (SSR)?

Los dos resuelven problemas diferentes y pueden trabajar juntos. La SSR tradicional procesa contenido del lado del servidor, pero no incluye contenido cargado posteriormente en el explorador. Optimizar en Edge: la renderización previa captura la página después de que JavaScript y los datos del lado del cliente se hayan cargado, lo que produce la versión completamente ensamblada en el perímetro de CDN. SSR se centra en mejorar la experiencia humana y Optimizar en Edge mejora la experiencia web para los LLM.


















