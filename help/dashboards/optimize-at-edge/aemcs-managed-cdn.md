---
title: 'Optimizar en Edge: CDN administrada por AEM Cloud Service (rápidamente)'
description: Aprenda a configurar la CDN administrada de AEM Cloud Service (Fastly) para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 184d6008c2579014c6ff453e8bfff4bb898f4b82
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# CDN administrada por AEM Cloud Service (rápidamente)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, compruebe el encabezado `x-edgeoptimize-request-id` en la respuesta.

## Requisitos previos

Para acceder a esta función:

- Los clientes de pago deben tener acceso al perfil de producto de IMS **Usuarios de Adobe LLM Optimizer**. Póngase en contacto con el administrador de su organización para solicitar acceso.
  ![Agregar usuario a un perfil de producto](/help/assets/optimize-at-edge/cs-fastly-user-product-profiles.png)
- Los clientes de prueba deben formar parte del grupo de IMS **Administración de LMO**. Si el grupo no existe, el administrador de su organización puede crearlo y agregarle.
  ![Crear grupo IMS de administrador de LLMO](/help/assets/optimize-at-edge/cs-fastly-create-ims-group.png)

>[!NOTE]
> Safari o los modos de navegación incógnito/privada no admiten esta función.

## Pasos para activar el enrutamiento

Para empezar a enrutar el tráfico auténtico a Edge Optimize:

1. En LLM Optimizer, abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

   ![Ir a la configuración del cliente](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. Busque la sección **Implementar optimizaciones en agentes de IA**. Haga clic en el botón **Habilitar**.

   ![Implementar optimizaciones en agentes de IA — pendientes](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. En el cuadro de diálogo de confirmación, seleccione **Habilitar** para confirmar que desea habilitar el enrutamiento. Si aparece un error, consulte la sección [Solución de problemas](#troubleshooting) para resolverlo.

   ![Activar diálogo de confirmación del motor de optimización](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. Una vez confirmado, el enrutamiento tarda unos minutos en completarse.

   ![Enrutamiento en curso](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   Vuelva a cargar la página después de 5 minutos para comprobar que el enrutamiento ha finalizado. Una vez que el enrutamiento esté configurado y activo, el estado se actualiza a **Completado** con una marca de verificación verde que confirma que el enrutamiento está habilitado. No se requiere ninguna otra acción por su parte.

   ![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   Para deshabilitar el enrutamiento en cualquier momento, vuelva a la sección **Implementar optimizaciones en los agentes de IA** en la pestaña **Configuración de CDN** y haga clic en **Deshabilitar**.

Además, si necesita ayuda con los pasos anteriores, póngase en contacto con el equipo de la cuenta de Adobe o con `llmo-at-edge@adobe.com`.

## Resolución de problemas

Si aparece un error al habilitar o deshabilitar el enrutamiento, tendrá un aspecto similar al siguiente:

![Error de diálogo de confirmación](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

Utilice la lista siguiente para identificar el error y seguir las instrucciones.

1. **El usuario no tiene acceso al producto LLMO**

   **Causa:** La cuenta de usuario no tiene el contexto de producto de LLM Optimizer en su perfil de IMS de Adobe. Esto es necesario para que los clientes de pago configuren el enrutamiento de CDN.

   **Recomendación:** Compruebe que el administrador de su organización le ha asignado el perfil de producto **Usuarios de Adobe LLM Optimizer** en Adobe Admin Console.

2. **Solo los miembros del grupo de administradores de LLMO pueden configurar el enrutamiento de CDN**

   **Causa:** Su cuenta no es miembro del grupo de IMS **Administrador de LMO**. Esto es necesario para que los clientes de prueba configuren el enrutamiento de CDN.

   **Recomendación:** Compruebe que su administrador de organización lo ha agregado al grupo IMS **LLMO Admin** en Adobe Admin Console.

3. **El tipo de CDN solicitado aem-cs-fastly no coincide con la CDN detectada para este dominio**

   **Causa:** Esto indica que el tipo de CDN detectado para su sitio no es *CDN administrado por AEM Cloud Service (Fastly)*.

   **Recomendación:** Compruebe que el sitio se proporciona a través de una CDN administrada por AEM Cloud Service (Fastly).

4. **Error al sondear el sitio**

   **Causa:** LLM Optimizer no pudo llegar a su sitio durante la configuración de enrutamiento. Esto puede suceder si el sitio está inactivo, inaccesible o si se ha agotado el tiempo de espera de la solicitud.

   **Recomendación:** Compruebe que el sitio es de acceso público y que devuelve una respuesta válida e inténtelo de nuevo.

5. **El sitio no devolvió una respuesta válida para el sondeo de enrutamiento**

   **Causa:** El sitio devolvió un estado HTTP inesperado (no 2xx ni 301) cuando se sondeó durante la instalación.

   **Recomendación:** Compruebe que el sitio devuelve una respuesta correcta (2xx) para la dirección URL base registrada en LLM Optimizer e inténtelo de nuevo.

6. **Error de autenticación con el servicio IMS ascendente**

   **Causa:** Es posible que la sesión haya caducado o que se haya producido un problema al autenticarse con Adobe IMS durante la solicitud de enrutamiento.

   **Recomendación:** Cierre la sesión de LLM Optimizer, vuelva a iniciarla e intente habilitar de nuevo el enrutamiento.

Si el problema persiste, póngase en contacto con el equipo de la cuenta de Adobe o `llmo-at-edge@adobe.com`.

## (Opcional) Compruebe la configuración

Una vez completada la configuración de enrutamiento, puede verificar de forma opcional que el tráfico de bots de IA se enrute a Edge Optimize y que el tráfico humano no se vea afectado.

1. **Probar tráfico de bots (debe optimizarse)**

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

2. **Probar el tráfico humano (NO debería verse afectado)**

   Simule una solicitud normal de explorador humano:

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
   ```

   La respuesta no debe contener el encabezado `x-edgeoptimize-request-id`. El contenido de la página y el tiempo de respuesta deben ser idénticos al de antes de habilitar Optimizar en Edge.

3. **Cómo diferenciar los dos escenarios**

   | Encabezado | Tráfico de bots (optimizado) | Tráfico humano (no afectado) |
   |---|---|---|
   | `x-edgeoptimize-request-id` | Presente: contiene un ID de solicitud único. | Ausente |
   | `x-edgeoptimize-fo` | Solo está presente si se produjo la conmutación por error (valor: `1`) | Ausente |

4. **Comprobar el estado de enrutamiento en LLM Optimizer**

   También puede confirmar el enrutamiento en la interfaz de usuario de LLM Optimizer. Abra **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**. Cuando el enrutamiento está activo, la sección **Implementar optimizaciones en agentes de IA** muestra **Completado**.

   ![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
