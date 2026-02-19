---
title: 'Optimizar en Edge: CDN administrada por AEM Cloud Service (rápidamente)'
description: Aprenda a configurar la CDN administrada de AEM Cloud Service (Fastly) para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 12%

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

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

{{return-to-overview}}
