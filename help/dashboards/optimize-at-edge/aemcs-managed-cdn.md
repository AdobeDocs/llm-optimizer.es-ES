---
title: 'Optimizar en Edge: CDN administrada por AEM Cloud Service (rápidamente)'
description: Aprenda a configurar la CDN administrada de AEM Cloud Service (Fastly) para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 0c7ccadbb40c8c119cb2a57cf8118708c33c4236
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 12%

---


# CDN administrada por AEM Cloud Service (rápidamente)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Para empezar a enrutar el tráfico auténtico a Edge Optimize:

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Busque la sección **Implementar optimizaciones en agentes de IA**. Marque la casilla de verificación **Activar motor de optimización**.

   ![Implementar optimizaciones en agentes de IA — pendientes](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. En el cuadro de diálogo de confirmación, seleccione **Habilitar**. El equipo de Adobe se encargará de la configuración de enrutamiento en su nombre.

   ![Activar diálogo de confirmación del motor de optimización](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

   Una vez que el enrutamiento esté configurado y activo, el estado se actualiza a **Completado** con una marca de verificación verde que confirma que el enrutamiento está habilitado. No se requiere ninguna otra acción por su parte.

   ![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

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

**4. Comprobar el estado de enrutamiento en LLM Optimizer**

También puede confirmar el enrutamiento en la interfaz de usuario de LLM Optimizer. Abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**. Cuando el enrutamiento está activo, la sección **Implementar optimizaciones en agentes de IA** muestra **Completado**.

![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
