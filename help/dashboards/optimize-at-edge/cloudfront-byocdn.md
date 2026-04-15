---
title: 'Optimizar en Edge: CloudFront (BYOCDN)'
description: Obtenga información sobre cómo configurar CloudFront BYOCDN para optimizar en Edge en LLM Optimizer.
feature: Opportunities
source-git-commit: 001ed59e25975c718367f543b2e35fedbce686f5
workflow-type: tm+mt
source-wordcount: '2223'
ht-degree: 1%

---


# CloudFront (BYOCDN)

Esta configuración enruta el tráfico auténtico (solicitudes de bots de IA y agentes de usuario LLM) al servicio back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completada la instalación, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de establecer la configuración de CloudFront, asegúrese de lo siguiente:

* Una distribución existente de CloudFront que sirve a su sitio web.
* Permisos de AWS IAM para crear funciones de Lambda, funciones de IAM, distribuciones de CloudFront y directivas de caché.
* Se ha completado el proceso de incorporación de LLM Optimizer.
* Reenvío de registro de CDN completado a LLM Optimizer.
* Una clave de API de Edge Optimize recuperada de la interfaz de usuario de LLM Optimizer.
* (Opcional) Para probar el enrutamiento de ensayo, consulte **Opcional: Prueba del enrutamiento en un nombre de host de ensayo** al final de esta página.

{{retrieve-byocdn-api-key}}

**Paso 1: Crear origen de optimización de Edge**

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Pestaña Orígenes

1. Haga clic en **Crear origen**.

2. Configure el origen:
   * **Dominio de origen:** `live.edgeoptimize.net`
   * **Nombre:** `EdgeOptimize_Origin`

3. Deje los demás campos con sus valores predeterminados.

4. Añadir encabezados personalizados:

   | Encabezado | Value |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Su clave de API |
   | `x-forwarded-host` | `www.example.com` |

   Reemplace `www.example.com` por su dominio real del sitio web y `Your API key` por la clave de API de Edge Optimize proporcionada por su representante de Adobe.

5. Haga clic en **Crear origen**.

![Creación de origen de Cloudfront](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**Paso 2: crear función de solicitud de visor**

**Navegación:** Consola de AWS > CloudFront > Funciones

1. Haga clic en **Crear función**.

2. Configuración de:
   * **Nombre:** `edgeoptimize-routing`
   * **Tiempo de ejecución:** `cloudfront-js-2.0`

3. Reemplace el código predeterminado por el código de [viewer-request.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/cloudfront-function/viewer-request.js).

   Antes de publicar, personalice los siguientes valores en el código:

   * `YOUR_DEFAULT_ORIGIN`: reemplace con el nombre de su origen predeterminado existente (que se encuentra en CloudFront > Distribuciones > [Su distribución] > pestaña Orígenes ).
   * `TARGETED_PATHS` — Se establece en `null` para dirigirse a todas las páginas de HTML o a una matriz de rutas específicas, por ejemplo, `['/', '/products', '/about']`.

4. Haga clic en **Guardar cambios** > **Función de publicación**.

![Creación de funciones de Cloudfront](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**Paso 3: Configurar la directiva de caché**

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

Compruebe la política de caché asociada actualmente a su comportamiento. Haga clic en **Editar** en su comportamiento y observe la sección **Clave de caché y solicitudes de origen** para identificar su escenario:

* **Escenario A (heredado):** Verá seleccionado un botón de opción denominado **Configuración de caché heredada**. No hay ningún menú desplegable de nombre de directiva; en su lugar, verá la configuración de TTL y encabezado en línea.
* **Escenario B (directiva personalizada):** Verá **Directiva de caché** seleccionada con un nombre de directiva que usted o su equipo hayan creado (no una directiva proporcionada por AWS).
* **Escenario C (directiva administrada):** Verá **Directiva de caché** seleccionada con un nombre proporcionado por AWS como `CachingOptimized`, `CachingDisabled` o `CachingOptimizedForUncompressedObjects`; estos nombres no se pueden editar.

**Escenario A: configuración de caché heredada**

Si su comportamiento utiliza la configuración de caché heredada:

1. En **Solicitudes de origen y clave de caché**, verá **Configuración de caché heredada** seleccionada.

2. Agregar `x-edgeoptimize-config` y `x-edgeoptimize-url` a la lista de permitidos **Encabezados**:

   * Seleccione **Incluir los siguientes encabezados** en el menú desplegable.
   * Agregar `x-edgeoptimize-config` y `x-edgeoptimize-url`.
     ![Heredado de caché de Cloudfront](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   Si ya ha seleccionado **Todos** en la lista desplegable Encabezados, omita este paso: todos los encabezados se reenvían automáticamente al origen.

3. Compruebe la configuración de **Almacenamiento en caché de objetos**:

   * Si se establece en **Personalizar**, se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si el TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.
   * Si se establece en **Usar encabezados de caché de origen**, no se necesita ningún cambio.

4. Haga clic en **Guardar cambios**.

**Escenario B: no heredado con una directiva de caché personalizada**

Si su comportamiento ya utiliza una directiva de caché personalizada (una que haya creado, no una directiva administrada por AWS):

**Navegación:** Consola de AWS > CloudFront > Directivas > Caché

1. Haga clic en la política existente.

2. Haga clic en **Editar**.

3. Se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si el TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.
   ![Configuración TTL de directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. En **Configuración de clave de caché** > **Encabezados**, junto con las inclusiones existentes, agregue `x-edgeoptimize-config` y `x-edgeoptimize-url`.
   ![Encabezados de directivas de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Haga clic en **Guardar cambios**.

**Escenario C: no heredado con una directiva de caché administrada (AWS)**

Si su comportamiento usa una directiva de caché administrada por AWS (por ejemplo, `CachingOptimized`), no podrá editarla. Debe crear una nueva directiva de caché personalizada que duplique la configuración de directiva administrada existente y agregue los encabezados de Edge Optimize en la parte superior.

**Parte 1: anote la configuración actual de la directiva de caché administrada**

**Navegación:** Consola de AWS > CloudFront > Directivas > Caché

1. Busque y haga clic en la directiva de caché administrada que está adjunta a su comportamiento (por ejemplo, `CachingOptimized`).

2. Tenga en cuenta todos los ajustes existentes:
   * TTL mínimo, TTL máximo, TTL predeterminado
   * Encabezados incluidos en la clave de caché
   * Cookies incluidas en la clave de caché
   * Cadenas de consulta incluidas en la clave de caché
   * Compatibilidad con compresión (Gzip, Brotli)

**Parte 2: Crear una nueva directiva de caché personalizada con la misma configuración + Configuración de optimización de Edge**

**Navegación:** Consola de AWS > CloudFront > Directivas > Caché

1. Haga clic en **Crear directiva de caché**.

2. **Nombre:** `edgeoptimize-cache`

   ![Nombre de directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Repita todos los ajustes mencionados en la parte 1, con las siguientes modificaciones:

   * Se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si el TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.

   ![Configuración TTL de directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * En **Configuración de clave de caché** > **Encabezados**, incluya todo lo que tenía la directiva administrada, además de agregar `x-edgeoptimize-config` y `x-edgeoptimize-url`.

   ![Encabezados de directivas de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Haga clic en **Crear**.

5. Vuelva al comportamiento y asocie la directiva recién creada:

   **Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

   1. Edite su comportamiento.
   2. En **Solicitudes de origen y clave de caché**, seleccione **Directiva de caché**.
   3. Elija `edgeoptimize-cache` de la lista desplegable.
   4. Haga clic en **Guardar cambios**.

**Paso 4: crear la función Lambda@Edge (solicitud de origen y respuesta)**

>[!IMPORTANT]
>Las funciones de Lambda@Edge **deben crearse en la región `us-east-1` (Virginia Norte)**. Se trata de un requisito de AWS. Aunque la función se crea en `us-east-1`, AWS la replica automáticamente en todas las ubicaciones de Edge de CloudFront en todo el mundo, de modo que se ejecute en la ubicación de Edge más cercana al visor. Asegúrese de que se encuentra en la región `us-east-1` de la consola de AWS antes de continuar.

**Crear la función Lambda**

**Navegación:** Consola de AWS > Lambda

1. Haga clic en **Crear función**.

2. Seleccione **Autor desde cero**.

3. Configuración de:
   * **Nombre de función:** `edgeoptimize-origin`
   * Deje los demás campos con sus valores predeterminados.

4. Haga clic en **Crear función**.

5. En el editor de código, reemplace el código predeterminado por el código de [origin-request-response.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/origin-request-response.js).

6. Haga clic en **Implementar** para guardar el código.

7. Observe el **nombre de rol de ejecución** que se muestra en **Configuración** > **Permisos** (por ejemplo, `edgeoptimize-origin-role-xxxxx`). Esto es necesario en los pasos siguientes.

**Actualizar la directiva de confianza del rol de ejecución**

La función creada automáticamente solo confía en `lambda.amazonaws.com`. Para Lambda@Edge, también debe agregar `edgelambda.amazonaws.com`.

**Navegación:** Consola de AWS > IAM > Roles > [su rol del paso anterior] > pestaña Relaciones de confianza

1. Haga clic en **Editar directiva de confianza**.

2. Reemplace la directiva por el contenido de [trust-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/trust-policy.json).

3. Haga clic en **Actualizar directiva**.

>[!WARNING]
>La entidad de seguridad del servicio `edgelambda.amazonaws.com` es **necesaria** para Lambda@Edge. Sin ella, CloudFront no puede invocar la función en ubicaciones de Edge.

**Corregir la directiva de permisos de registros de CloudWatch**

La función creada automáticamente viene con una directiva `AWSLambdaBasicExecutionRole` configurada para Lambda normal, que tiene la región y el nombre de grupo de registro incorrectos para Lambda@Edge. Tiene que actualizarlo.

**Navegación:** Consola de AWS > IAM > Roles > [su rol] > Pestaña Permisos > haga clic en el nombre de la directiva adjunta (por ejemplo, `AWSLambdaBasicExecutionRole-xxxx`)

1. Haga clic en **Editar**.

2. Reemplace la directiva por el contenido de [cloudwatch-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/cloudwatch-policy.json).

   En el JSON, reemplace `ACCOUNT_ID` por su ID de cuenta de AWS real (que se encuentra en la esquina superior derecha de la consola de AWS) y `FUNCTION_NAME` por el nombre de su función Lambda (por ejemplo, `edgeoptimize-origin`).

3. Haga clic en **Guardar cambios**.

>[!WARNING]
>La región de ARN debe ser `*`: Lambda@Edge se ejecuta en la ubicación de Edge más cercana al visor, por lo que los registros se escriben en CloudWatch en la región de Edge (por ejemplo, `ap-south-1`, `eu-west-1`), no necesariamente en `us-east-1`. El grupo de registro usa un nombre con prefijo de región: `/aws/lambda/us-east-1.FUNCTION_NAME`, donde `us-east-1` es siempre la región de inicio de la función.

**Publicar una versión**

1. En la página de funciones, haga clic en **Acciones** (parte superior derecha) > **Publicar nueva versión**.

2. Añada una descripción.

3. Haga clic en **Publicar**.
   ![Publicación lambda](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Copie o anote el **ARN de función**; necesita esto en el siguiente paso.
   ![Lambda ARN](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**Paso 5: asociar las funciones y la directiva de caché con el comportamiento**

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

1. Edite su comportamiento.

2. Si creó una nueva directiva de caché en el paso 3 (escenario C), establezca **Directiva de caché** en `edgeoptimize-cache`.
   ![Directiva de caché](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. En **Asociaciones de funciones**, configure:

   * **Solicitud de visor:** `edgeoptimize-routing`
   * **Solicitud de origen:** ARN de función con versión del paso 4 (en **Publicar una versión**)
   * **Respuesta de origen:** ARN de función con versión del paso 4 (en **Publicar una versión**)

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Haga clic en **Guardar cambios**.

**Permitir la optimización en Edge mediante reglas de firewall (opcional)**

{{waf-allowlist-setup}}

**Paso 6: Probar la configuración**

**1. Probar el tráfico de bots (debe optimizarse)**

Envíe una solicitud con un agente de usuario de bots auténtico. En la **primera solicitud**, Edge Optimize puede devolver una respuesta proxy (no optimizada) mientras procesa y almacena en caché la página. Esto se puede identificar mediante el encabezado `x-edgeoptimize-proxy: 1` de la respuesta.

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

**4. Verificar que los registros fluyan correctamente**

Después de ejecutar las solicitudes de prueba anteriores, compruebe que se escriben registros tanto para la función CloudFront como para la función Lambda@Edge.

*Registros de funciones de CloudFront (`edgeoptimize-routing`)*

**Navegación:** Consola de AWS > CloudWatch > Grupos de registro (en `us-east-1` o la región donde está configurada su distribución de CloudFront)

1. Busque un grupo de registro denominado `/aws/cloudfront/function/edgeoptimize-routing`.
2. Abra el flujo de registro más reciente.
3. Para solicitudes reales, debería ver entradas como:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. Para las solicitudes que no son auténticas, debería ver lo siguiente:
   * `Routing to Default origin for userAgent: ...`

También puede marcar la pestaña **Métricas** en **Consola AWS > CloudFront > Funciones > edgeoptimize-routing** para ver los recuentos de invocaciones y las tasas de error.

*Lambda@Edge registros (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Los registros de Lambda@Edge se escriben en CloudWatch en la **región de la ubicación perimetral** que proporcionó la solicitud, no en `us-east-1`. Compruebe CloudWatch en la región de AWS más cercana a donde ejecutó el comando curl.

**Navegación:** Consola de AWS > CloudWatch > Grupos de registro (asegúrese de que se encuentra en la región correcta)

1. Busque un grupo de registro denominado `/aws/lambda/us-east-1.edgeoptimize-origin`.
2. Abra el flujo de registro más reciente.
3. Para solicitudes reales, debería ver entradas como:
   * `Calling Edge Optimize Origin for agentic requests` — ruta principal
   * `Calling Default Origin in case of failover for agentic requests`: ruta de conmutación por error
   * `Failover Triggered for agentic requests`: detección de conmutación por error origen-respuesta

Si el grupo de registro no está presente, compruebe que los permisos de IAM se actualizaron correctamente en el paso 4. Compruebe también otras regiones de AWS cercanas: la ubicación de Edge que atendió su solicitud puede diferir de lo que esperaba.

**Solución de problemas**

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| No hay `x-edgeoptimize-request-id` en respuesta a solicitudes agénticas | El grupo de origen no está enrutando a Edge Optimize | Verifique que `YOUR_DEFAULT_ORIGIN` se haya reemplazado correctamente en el código de función de CloudFront (Paso 2). |
| Errores 403 en solicitudes agénticas | Falta la clave API o no es válida | Compruebe el valor del encabezado `x-edgeoptimize-api-key` en los encabezados personalizados de origen de Edge Optimize (paso 1). |
| No se encontraron registros de CloudWatch para Lambda@Edge | Permisos de IAM incorrectos | Compruebe que se ha actualizado la directiva de permisos de registros de CloudWatch (paso 4). Nota: Los registros de Lambda@Edge aparecen en la región de Edge que proporcionó la solicitud, no necesariamente `us-east-1`. |
| La caché no cumple `cache-control: no-store` | El TTL mínimo puede ser demasiado alto | Establezca el TTL mínimo en `0` en la directiva de caché (paso 3). Si el TTL mínimo ya es muy corto, es posible que este no sea el problema. |
| Tráfico normal (no auténtico) interrumpido tras la configuración | Error de configuración de directiva de caché | Si ha creado una nueva directiva de caché (Escenario C), asegúrese de que ha replicado toda la configuración de la directiva administrada original. |

**Desactivación y reactivación de Optimize en Edge**

La función Lambda@Edge (`edgeoptimize-origin`) está asociada a los eventos de solicitud de origen y respuesta de origen del comportamiento de CloudFront. Debido a que se ejecuta en línea en cada solicitud que pasa por ese comportamiento —tanto humana como auténtica— una interrupción de Lambda@Edge afectará todo el tráfico en vivo, no solo las solicitudes auténticas. Si detecta una interrupción de Lambda@Edge, quite las asociaciones de funciones inmediatamente para restaurar el flujo de tráfico normal a su origen predeterminado.

**Cómo detectar una interrupción de Lambda@Edge**

* **AWS Service Health Dashboard** — Compruebe el [AWS Service Health Dashboard](https://health.aws.amazon.com/health/status) para ver si hay algún incidente activo que afecte a **Amazon CloudFront** o **AWS Lambda**. La interrupción global o regional que se informa aquí es la forma más rápida de confirmar que el problema está en el lado de la infraestructura de AWS, no en su configuración.
* **Errores de Lambda@Edge** — Vaya a **Consola de AWS > CloudFront > Supervisión > [Su distribución]**. Abra la ficha **Errores de Lambda@Edge** y compruebe si hay errores de ejecución en el gráfico **Errores de ejecución**. Si son altos, Lambda@Edge podría estar abajo.

**Desasociando la función Lambda@Edge**

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

1. Haz clic en **Editar** en tu comportamiento.

2. Desplácese hacia abajo hasta la sección **Asociaciones de funciones**.

3. Establezca las siguientes asociaciones en **Sin asociación**:

   | Evento | Cambiar a |
   |---|---|
   | Solicitud del visor | Sin asociación |
   | Solicitud de origen | Sin asociación |
   | Respuesta de origen | Sin asociación |

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Haga clic en **Guardar cambios**.

5. Espere a que la distribución de CloudFront termine de implementarse. El estado cambia de **Implementación** a la última fecha de modificación, normalmente en unos minutos.

Una vez implementado, todas las rutas de tráfico se dirigen directamente al origen predeterminado. No se elimina ninguna configuración; la función Lambda y sus asociaciones se pueden restaurar en cualquier momento.

**Volver a adjuntar la función Lambda@Edge**

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

1. Haz clic en **Editar** en tu comportamiento.

2. Desplácese hacia abajo hasta la sección **Asociaciones de funciones**.

3. Restaurar las asociaciones:

   | Evento | Configure como. |
   |---|---|
   | Solicitud del visor | `edgeoptimize-routing` (función CloudFront) |
   | Solicitud de origen | ARN de Lambda con versión del paso 4 |
   | Respuesta de origen | ARN de Lambda con versión del paso 4 |

   Use la **ARN de función** con versión que anotó en el paso 4 (en **Publicar una versión**).

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Haga clic en **Guardar cambios**.

5. Espere a que la distribución termine de implementarse y, a continuación, compruebe que las solicitudes agénticas devuelven el encabezado `x-edgeoptimize-request-id` como se describe en el paso 6.

{{retrieve-staging-edge-optimize-api-key}}

```
curl -svo /dev/null https://staging.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

{{return-to-overview}}
