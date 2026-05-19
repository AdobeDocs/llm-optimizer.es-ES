---
title: 'Optimizar en Edge: CDN administrada por AEM Cloud Service (Fastly)'
description: Obtenga información sobre cómo configurar la CDN administrada de AEM Cloud Service (Fastly) para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:31:38.650Z'
TQID: 'https://experienceleague.adobe.com/qrCODY3Qg6dDd9QRcaYGdN4YVCgKAsl56UTAVZpsIwE'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 836
ht-degree: 100%

---


# CDN administrada por AEM Cloud Service (Fastly)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

## Requisitos previos

Para acceder a esta función, haga lo siguiente:

- Los clientes de pago deben tener acceso al perfil de producto de IMS **Usuarios de Adobe LLM Optimizer**. Póngase en contacto con el administrador de su organización para solicitar acceso.
  ![Añadir usuario a un perfil del producto](/help/assets/optimize-at-edge/cs-fastly-user-product-profiles.png)
- Los clientes de la versión de prueba deben formar parte del grupo de IMS **Administradores de LLMO**. Si el grupo no existe, el administrador de su organización puede crearlo y añadirle
  ![Crear grupo de IMS de administradores de LLMO](/help/assets/optimize-at-edge/cs-fastly-create-ims-group.png)

>[!NOTE]
> Esta función no es compatible con Safari o con los modos de exploración incógnito/privado.

## Pasos para habilitar el enrutamiento

Para empezar a enrutar el tráfico agéntico a Edge Optimize, haga lo siguiente:

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de la CDN**.

   ![Vaya a Configuración del cliente](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. Localice la sección **Implementar optimizaciones en agentes de IA**. Haga clic en el botón **Habilitar**.

   ![Implementar optimizaciones en agentes de IA: pendiente](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. En el cuadro de diálogo de confirmación, seleccione **Habilitar** para confirmar que desea habilitar el enrutamiento. Si aparece un error, consulte la sección [Solución de problemas](#troubleshooting) para resolverlo.

   ![Habilitar cuadro de diálogo de confirmación del motor de optimización](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. Una vez confirmado, el enrutamiento tarda unos minutos en completarse.

   ![Enrutamiento en curso](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   Vuelva a cargar la página al cabo de 5 minutos para comprobar que el enrutamiento se ha completado. Una vez que el enrutamiento esté configurado y activo, el estado se actualizará a **Completado** para mostrar una marca de verificación verde que indica que el enrutamiento se ha habilitado. No se requiere ninguna otra acción por su parte.

   ![Implementar optimizaciones en agentes de IA: completado](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   Para deshabilitar el enrutamiento en cualquier momento, vuelva a la sección **Implementar optimizaciones en agentes de IA** en la pestaña **Configuración de la CDN** y haga clic en **Deshabilitar**.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de cuentas de Adobe o con `llmo-at-edge@adobe.com`.

## Resolución de problemas

Si aparece un error al habilitar o deshabilitar el enrutamiento, tendrá un aspecto similar al siguiente:

![Error del cuadro de diálogo de confirmación](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

Utilice la lista siguiente para identificar el error y seguir las instrucciones.

1. **El usuario no tiene acceso al producto LLMO**

   **Causa:** la cuenta de usuario no tiene el contexto del producto LLM Optimizer en su perfil de Adobe IMS. Esto es necesario para que los clientes de pago configuren el enrutamiento de CDN.

   **Recomendación:** compruebe que el administrador de su organización le ha asignado el perfil de producto **Usuarios de Adobe LLM Optimizer** en Adobe Admin Console.

2. **Solo los miembros del grupo de administradores de LLMO pueden configurar el enrutamiento de CDN**

   **Causa:** su cuenta no es miembro del grupo de IMS de **Administradores de LLMO**. Esto es necesario para que los clientes de la versión de prueba configuren el enrutamiento de CDN.

   **Recomendación:** compruebe que su administrador de organización lo ha añadido al grupo de IMS de **Administradores de LLMO** en Adobe Admin Console.

3. **El tipo de CDN solicitado aem-cs-fastly no coincide con la CDN detectada para este dominio**

   **Causa:** esto indica que el tipo de CDN detectado para su sitio no es *CDN administrada por AEM Cloud Service (Fastly)*.

   **Recomendación:** compruebe que el sitio se atiende a través de una CDN administrada por AEM Cloud Service (Fastly).

4. **Error al sondear el sitio**

   **Causa:** LLM Optimizer no pudo acceder a su sitio durante la configuración del enrutamiento. Esto puede suceder si el sitio no está activo, es inaccesible o si se ha agotado el tiempo de espera de la solicitud.

   **Recomendación:** compruebe que el sitio es de acceso público, que devuelve una respuesta válida e inténtelo de nuevo.

5. **El sitio no devolvió una respuesta válida para el sondeo del enrutamiento**

   **Causa:** el sitio devolvió un estado HTTP inesperado (no 2xx ni 301) cuando se sondeó durante la instalación.

   **Recomendación:** compruebe que el sitio devuelve una respuesta correcta (2xx) para la dirección URL base registrada en LLM Optimizer e inténtelo de nuevo.

6. **Error de autenticación con el servicio IMS ascendente**

   **Causa:** es posible que la sesión haya caducado o que se haya producido un problema al autenticarse con Adobe IMS durante la solicitud de enrutamiento.

   **Recomendación:** cierre la sesión de LLM Optimizer, vuelva a iniciarla e intente habilitar de nuevo el enrutamiento.

Si el problema persiste, póngase en contacto con el equipo de cuentas de Adobe o con `llmo-at-edge@adobe.com`.

## (Opcional) Verificar la configuración

Una vez completada la configuración, puede comprobar opcionalmente que el tráfico de bots de IA se dirige hacia Edge Optimize y que el tráfico humano no se ve afectado.

1. **Probar el tráfico de bots (debe optimizarse)**

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

2. **Probar el tráfico humano (NO debería verse afectado)**

   Simule una solicitud normal de un explorador:

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
   ```

   La respuesta no debe contener el encabezado `x-edgeoptimize-request-id`. El contenido de la página y el tiempo de respuesta deben seguir siendo los mismos que antes de habilitar Optimizar en Edge.

3. **Cómo diferenciar entre los dos escenarios**

   | Encabezado | Tráfico de bots (optimizado) | Tráfico humano (no afectado) |
   |---|---|---|
   | `x-edgeoptimize-request-id` | Presente: contiene un ID de solicitud único | Ausente |
   | `x-edgeoptimize-fo` | Solo está presente si se produjo la conmutación por error (valor: `1`) | Ausente |

4. **Comprobar el estado de enrutamiento en LLM Optimizer**

   También puede confirmar el enrutamiento en la interfaz de usuario de LLM Optimizer. Abra **Configuración del cliente** y seleccione la pestaña **Configuración de la CDN**. Cuando el enrutamiento está activo, la sección **Implementar optimizaciones en agentes de IA** muestra el estado **Completado**.

   ![Implementar optimizaciones en agentes de IA: completado](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
