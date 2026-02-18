---
title: 'Optimizar en Edge: CDN administrada por AEM Cloud Service (rápidamente)'
description: Aprenda a configurar la CDN administrada de AEM Cloud Service (Fastly) para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 16%

---


# CDN administrada por AEM Cloud Service (rápidamente)

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

{{verify-setup-adobe-aem-cs-cdn}}

{{return-to-overview}}
