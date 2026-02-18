---
source-git-commit: beae935e7a34f5bccbe21578fa9a928912958710
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---
# Fragmentos

## Verifique la configuración: CDN administrada por Adobe {#verify-setup-adobe-aem-cs-cdn}

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

## Verificar la configuración: BYOCDN {#verify-setup-byocdn}

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

![Estado de enrutamiento de tráfico AI con enrutamiento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Pasos de recuperación de claves API {#retrieve-byocdn-api-key}

**Pasos para recuperar la clave de API:**

1. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. En **Enrutamiento del tráfico de IA para implementar optimizaciones**, marque la casilla de verificación **Implementar optimizaciones en agentes de IA**.

   ![Marque Implementar optimizaciones en agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie la clave de API y continúe con los pasos de configuración de enrutamiento a continuación.

   ![Copiar la clave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >En esta fase, el estado puede mostrar una cruz roja que indique que la configuración aún no ha finalizado. Esto es de esperar: una vez que complete la configuración de enrutamiento a continuación y el tráfico de bots de IA comience a fluir, el estado se actualizará a una marca de verificación verde que confirme que el enrutamiento se ha habilitado correctamente.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

## Volver a la descripción general {#return-to-overview}

Para obtener más información sobre Optimizar en Edge, incluidas las oportunidades disponibles, los flujos de trabajo de optimización automática y las preguntas frecuentes, vuelve a [Optimizar en la descripción general de Edge](/help/dashboards/optimize-at-edge.md).
