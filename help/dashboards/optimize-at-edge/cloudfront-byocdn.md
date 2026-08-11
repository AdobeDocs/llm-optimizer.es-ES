---
title: 'Optimizar en Edge: CloudFront (BYOCDN)'
description: Obtenga información sobre cómo configurar CloudFront BYOCDN para Optimizar en Edge en LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:46:25.674Z'
TQID: 'https://experienceleague.adobe.com/yIEUTzlnvOX-WBf276KQcAN8sGYDpZNVibJt024VMWU'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e1b649f0-0a61-46e4-9082-64d5cb2576c6id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3aid: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: e36ee407933e2d3d56cadf1c9517f23f24d41d91
workflow-type: tm+mt
source-wordcount: 2360
ht-degree: 95%

---


# CloudFront (BYOCDN)

Esta configuración enruta el tráfico agéntico (solicitudes de bots de IA y agentes de usuario LLM) al servicio de back-end de Edge Optimize (`live.edgeoptimize.net`). Los visitantes humanos y los bots de SEO se siguen sirviendo desde su origen como de costumbre. Para probar la configuración, una vez completados los ajustes, busque el encabezado `x-edgeoptimize-request-id` en la respuesta.

**Requisitos previos**

Antes de establecer la configuración de CloudFront, asegúrese de que dispone de lo siguiente:

* Una distribución existente de CloudFront que atiende su sitio web.
* Permisos IAM de AWS para crear funciones de Lambda, funciones de IAM, distribuciones de CloudFront y directivas de caché.
* Haber recuperado una clave de API de Edge Optimize de la IU de LLM Optimizer. Para ver los pasos, consulte [Recuperar las claves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para probar el enrutamiento de ensayo, consulte [Clave de API de ensayo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Paso 1: Crear el origen de optimización de Edge

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Pestaña Orígenes

1. Haga clic en **Crear origen**.

2. Configure el origen:
   * **Dominio de origen:** `live.edgeoptimize.net`
   * **Nombre:** `EdgeOptimize_Origin`

3. Deje los demás campos con sus valores predeterminados.

4. Añada encabezados personalizados:

   | Encabezado | Value |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Su clave de API |
   | `x-forwarded-host` | `www.example.com` |
   | `x-edgeoptimize-fetcher-key` | Su clave de recuperación (solo en el caso de la inclusión en la lista de permitidos de WAF) |

   Reemplace `www.example.com` por su dominio real del sitio web y `Your API key` por la clave de API de Edge Optimize proporcionada por su representante de Adobe.

5. Haga clic en **Crear origen**.

![Creación de origen de Cloudfront](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

## Paso 2: Crear una función de solicitud de visor

**Navegación:** Consola de AWS > CloudFront > Funciones

1. Haga clic en **Crear función**.

2. Configuración de:
   * **Nombre:** `edgeoptimize-routing`
   * **Tiempo de ejecución:** `cloudfront-js-2.0`

3. Reemplace el código predeterminado por el código de [viewer-request.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/cloudfront-function/viewer-request.js).

   Antes de publicar, personalice los siguientes valores del código:

   * `YOUR_DEFAULT_ORIGIN`: reemplace por el nombre de su origen predeterminado existente (que se encuentra en CloudFront > Distribuciones > [Su distribución] > pestaña Orígenes).
   * `TARGETED_PATHS`: establézcalo en `null` para que se aplique a todas las páginas HTML, o establézcalo en una matriz de rutas específicas, por ejemplo, `['/', '/products', '/about']`.

4. Haga clic en **Guardar cambios** > **Publicar función**.

![Creación de funciones de Cloudfront](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


## Paso 3: Configurar la política de caché

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

Verifique la directiva de la caché actualmente asociada a su comportamiento. Haga clic en **Editar** en su comportamiento y examine la sección **Clave de caché y solicitudes de origen** para identificar su escenario:

* **Escenario A (heredado):** verá un botón de opción etiquetado como **Configuración de caché heredada** seleccionado. No hay un menú desplegable para el nombre de la directiva; en su lugar, verá la configuración de TTL y del encabezado en línea.
* **Escenario B (directiva personalizada):** Verá **Directiva de caché** seleccionada con un nombre de directiva que usted o su equipo crearon (no una directiva proporcionada por AWS).
* **Escenario C (directiva administrada):** Verá **Directiva de caché** seleccionada con un nombre proporcionado por AWS como `CachingOptimized`, `CachingDisabled` o `CachingOptimizedForUncompressedObjects`; no se pueden editar.

### Escenario A: configuración de caché heredada

Si su comportamiento utiliza la configuración de caché heredada:

1. En **Clave de caché y solicitudes de origen**, verá **Configuración de caché heredada** seleccionada.

2. Añada `x-edgeoptimize-config` y `x-edgeoptimize-url` a la lista de elementos permitidos **Encabezados**:

   * Seleccione **Incluir los siguientes encabezados** en el menú desplegable.
   * Añada `x-edgeoptimize-config` y `x-edgeoptimize-url`.
     ![Caché de Cloudfront heredada](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   Si ya tiene seleccionado **Todo** en el menú desplegable Encabezados, omita este paso: todos los encabezados se reenviarán automáticamente al origen.

3. Compruebe la configuración del **almacenamiento en caché de objetos**:

   * Si se establece en **Personalizar**, se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si su TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.
   * Si se establece en **Usar encabezados de caché de origen**, no será necesario realizar ningún cambio.

4. Haga clic en **Guardar cambios**.

### Escenario B: no heredado con una directiva de caché personalizada

Si su comportamiento ya utiliza una directiva de caché personalizada (una que usted creó, no una directiva administrada por AWS):

**Navegación:** Consola de AWS > CloudFront > Políticas > Caché

1. Haga clic en su directiva existente.

2. Haga clic en **Editar**.

3. Se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si su TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.
   ![Configuración de TTL de la directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. En **Configuración de clave de caché** > **Encabezados**, junto con sus inclusiones existentes, añada `x-edgeoptimize-config` y `x-edgeoptimize-url`.
   ![Encabezados de la directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Haga clic en **Guardar cambios**.

### Escenario C: no heredado con una directiva de caché administrada (AWS)

Si su comportamiento utiliza una directiva de caché administrada por AWS (por ejemplo, `CachingOptimized`), no podrá editarla. Debe crear una nueva directiva de caché personalizada que replique la configuración de la directiva administrada existente y añada los encabezados de Edge Optimize encima.

**Parte 1: Anotar la configuración actual de la directiva de caché administrada**

**Navegación:** Consola de AWS > CloudFront > Directivas > Caché

1. Busque y haga clic en la directiva de caché administrada actualmente asociada a su comportamiento (por ejemplo, `CachingOptimized`).

2. Anote todas las configuraciones existentes:
   * TTL mínimo, TTL máximo, TTL predeterminado
   * Encabezados incluidos en la clave de caché
   * Cookies incluidas en la clave de caché
   * Cadenas de consulta incluidas en la clave de caché
   * Compatibilidad con la compresión (Gzip, Brotli)

**Parte 2: Crear una nueva directiva de caché personalizada con la misma configuración + configuración de Edge Optimize**

**Navegación:** Consola de AWS > CloudFront > Directivas > Caché

1. Haga clic en **Crear directiva de caché**.

2. **Nombre:** `edgeoptimize-cache`

   ![Nombre de la directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Repita toda la configuración mencionada en la parte 1, con las siguientes modificaciones:

   * Se recomienda establecer **TTL mínimo** en `0`. Sin embargo, si su TTL mínimo actual ya es muy corto, es posible que no necesite cambiarlo.

   ![Configuración de TTL de la directiva de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * En **Configuración de clave de caché** > **Encabezados**, incluya todo lo que tenía la directiva administrada, además de añadir `x-edgeoptimize-config` y `x-edgeoptimize-url`.

   ![Encabezados de directivas de caché](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Haga clic en **Crear**.

5. Vuelva al comportamiento y asocie la directiva recién creada:

   **Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

   1. Edite su comportamiento.
   2. En **Solicitudes de origen y clave de caché**, seleccione **Directiva de caché**.
   3. Elija `edgeoptimize-cache` en la lista desplegable.
   4. Haga clic en **Guardar cambios**.

## Paso 4: Crear la función Lambda@Edge (solicitud de origen y respuesta)

>[!IMPORTANT]
>Las funciones de Lambda@Edge **deben crearse en la región `us-east-1` (Virginia del norte)**. Se trata de un requisito de AWS. Aunque la función se crea en `us-east-1`, AWS la replica automáticamente en todas las ubicaciones perimetrales de CloudFront en todo el mundo, de modo que se ejecute en la ubicación perimetral más cercana al visor. Asegúrese de que se encuentra en la región `us-east-1` de la consola de AWS antes de continuar.

### Creación de la función Lambda

**Navegación:** Consola de AWS > Lambda

1. Haga clic en **Crear función**.

2. Seleccione **Autor desde cero**.

3. Configuración de:
   * **Nombre de función:** `edgeoptimize-origin`
   * Deje los demás campos con sus valores predeterminados.

4. Haga clic en **Crear función**.

5. En el editor de código, reemplace el código predeterminado por el código de [origin-request-response.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/origin-request-response.js).

6. Haga clic en **Implementar** para guardar el código.

7. Anote el **nombre de función de ejecución** que aparece en **Configuración** > **Permisos** (por ejemplo, `edgeoptimize-origin-role-xxxxx`). Esto es necesario en los pasos siguientes.

### Actualizar la directiva de confianza del rol de ejecución

La función creada automáticamente solo confía en `lambda.amazonaws.com`. Para Lambda@Edge, también debe añadir `edgelambda.amazonaws.com`.

**Navegación:** Consola de AWS > IAM > Funciones > [su función del paso anterior] > pestaña Relaciones de confianza

1. Haga clic en **Editar directiva de confianza**.

2. Reemplace la directiva por el contenido de [trust-policy.json](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/trust-policy.json).

3. Haga clic en **Actualizar directiva**.

>[!WARNING]
>El principal del servicio `edgelambda.amazonaws.com` es **obligatorio** para Lambda@Edge. Sin él, CloudFront no puede invocar la función en ubicaciones perimetrales.

### Corregir la directiva de permisos Registros de CloudWatch

La función creada automáticamente viene con una directiva `AWSLambdaBasicExecutionRole` configurada para Lambda normal, que tiene la región y el nombre de grupo de registro incorrectos para Lambda@Edge. Tiene que actualizarla.

**Navegación:** Consola de AWS > IAM > Funciones > [su función] > pestaña Permisos > haga clic en el nombre de la directiva adjunta (por ejemplo, `AWSLambdaBasicExecutionRole-xxxx`)

1. Haga clic en **Editar**.

2. Reemplace la directiva por el contenido de [cloudwatch-policy.json](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/cloudwatch-policy.json).

   En el JSON, reemplace `ACCOUNT_ID` por su ID de cuenta de AWS real (que se encuentra en la esquina superior derecha de la consola de AWS) y `FUNCTION_NAME` por el nombre de su función Lambda (por ejemplo, `edgeoptimize-origin`).

3. Haga clic en **Guardar cambios**.

>[!WARNING]
>La región de ARN debe ser `*`: Lambda@Edge se ejecuta en la ubicación perimetral más cercana al visor, por lo que los registros se escriben en CloudWatch en la región de la ubicación perimetral (por ejemplo, `ap-south-1`, `eu-west-1`), no necesariamente en `us-east-1`. El grupo de registros usa un nombre con prefijo de región: `/aws/lambda/us-east-1.FUNCTION_NAME`, donde `us-east-1` es siempre la región de inicio de la función.

### Corregir el vínculo de registros de CloudWatch

De manera predeterminada, el acceso directo **Ver registros de CloudWatch** en la consola Lambda vincula a `/aws/lambda/FUNCTION_NAME` en `us-east-1`, el grupo de registro incorrecto para Lambda@Edge. Configure un grupo de registro personalizado para que el vínculo apunte a la ruta correcta.

**Navegación:** Consola de AWS > Lambda > [su función] > Configuración > Herramientas de supervisión y operaciones

1. Haga clic en **Editar**.

2. En el **grupo de registro CloudWatch**, seleccione **Personalizado**.

3. Establezca el nombre del grupo de registro personalizado en `/aws/lambda/us-east-1.edgeoptimize-origin`.

4. En **Permisos**, deje la casilla de verificación **Añadir permisos necesarios** **sin marcar**.

   ![Configuración del grupo de registro personalizado Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-custom-log-group.png)

5. Haga clic en **Guardar**.

>[!NOTE]
>Incluso después de esta corrección, el vínculo **Ver registros de CloudWatch** abre el nombre de grupo de registro correcto, pero es posible que no muestre datos si se encuentra en la región incorrecta. Los registros de Lambda@Edge se escriben en CloudWatch en la región que atendió la solicitud (por ejemplo, `eu-west-1`, `ap-south-1`), no `us-east-1`. Aún debe cambiar a la región correcta en Cloud Watch para ver los registros.

### Publicar una versión

1. En la página de funciones, haga clic en **Acciones** (parte superior derecha) > **Publicar nueva versión**.

2. Añada una descripción.

3. Haga clic en **Publicar**.
   ![Publicación de Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Copie o anote el **ARN de función**; lo necesitará en el siguiente paso.
   ![ARN de Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

## Paso 5: Asociar las funciones y la política de caché con el comportamiento

**Navegación:** Consola de AWS > CloudFront > Distribuciones > [Su distribución] > Comportamientos

1. Edite su comportamiento.

2. Si creó una nueva directiva de caché en el paso 3 (escenario C), establezca **Directiva de caché** en `edgeoptimize-cache`.
   ![Directiva de caché](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. En **Asociaciones de funciones**, configure:

   * **Solicitud del visor:** `edgeoptimize-routing`
   * **Solicitud de origen:** ARN de función con versiones del paso 4 (en **Publicar una versión**)
   * **Respuesta de origen:** ARN de función con versiones del paso 4 (en **Publicar una versión**)

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Haga clic en **Guardar cambios**.

## Permitir Optimize en Edge mediante reglas de cortafuegos (opcional)

{{waf-allowlist-setup}}

## Paso 6: Prueba de la configuración

**1. Probar el tráfico de bots (debe optimizarse)**

Envíe una solicitud con un agente de usuario de bots agéntico. En la **primera solicitud**, Edge Optimize puede devolver una respuesta proxy (no optimizada) mientras procesa y almacena en caché la página. La puede identificar mediante el encabezado `x-edgeoptimize-proxy: 1` de la respuesta.

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

**4. Verificar que los registros fluyan correctamente**

Después de ejecutar las solicitudes de prueba anteriores, compruebe que se escriben registros tanto para la función CloudFront como para la función Lambda@Edge.

*Registros de funciones de CloudFront (`edgeoptimize-routing`)*

**Navegación:** Consola de AWS > CloudWatch > Grupos de registros (en `us-east-1` o en la región donde está configurada su distribución de CloudFront)

1. Busque un grupo de registros denominado `/aws/cloudfront/function/edgeoptimize-routing`.
2. Abra el flujo de registro más reciente.
3. Para solicitudes agénticas, deberían aparecer entradas como:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. Para las solicitudes que no son agénticas, debería aparecer lo siguiente:
   * `Routing to Default origin for userAgent: ...`

También puede marcar la pestaña **Métricas** en **Consola AWS > CloudFront > Funciones > edgeoptimize-routing** para ver los recuentos de invocaciones y las tasas de errores.

*Registros de Lambda@Edge (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Los registros de Lambda@Edge se escriben en CloudWatch en la **región de la ubicación perimetral** que atendió la solicitud, no en `us-east-1`. Consulte CloudWatch en la región de AWS más cercana al lugar donde ejecutó el comando curl.

**Navegación:** Consola de AWS > CloudWatch > Grupos de registros (asegúrese de que se encuentra en la región correcta)

1. Busque un grupo de registros denominado `/aws/lambda/us-east-1.edgeoptimize-origin`.
2. Abra el flujo de registro más reciente.
3. Para solicitudes agénticas, deberían aparecer entradas como:
   * `Calling Edge Optimize Origin for agentic requests`: ruta principal
   * `Calling Default Origin in case of failover for agentic requests`: ruta de conmutación por error
   * `Failover Triggered for agentic requests`: detección de conmutación por error en origen-respuesta

Si el grupo de registros no está presente, compruebe que los permisos de IAM se actualizaron correctamente en el paso 4. Compruebe también otras regiones de AWS cercanas: la ubicación perimetral que atendió su solicitud puede ser diferente de lo que esperaba.

## Resolución de problemas

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| No hay ningún `x-edgeoptimize-request-id` en la respuesta para las solicitudes agénticas | El grupo de origen no se está dirigiendo hacia Edge Optimize | Verifique que `YOUR_DEFAULT_ORIGIN` se haya reemplazado correctamente en el código de función de CloudFront (paso 2). |
| Errores 403 en solicitudes agénticas | Falta la clave API o no es válida | Compruebe el valor del encabezado `x-edgeoptimize-api-key` en los encabezados personalizados de origen de Edge Optimize (paso 1). |
| No se encontraron registros de CloudWatch para Lambda@Edge | Permisos de IAM incorrectos | Compruebe que se ha actualizado la directiva de permisos de registros de CloudWatch (paso 4). Nota: Los registros de Lambda@Edge aparecen en la región perimetral que atendió la solicitud, no necesariamente `us-east-1`. |
| La caché no respeta `cache-control: no-store` | El TTL mínimo puede ser demasiado alto | Establezca el TTL mínimo en `0` en la directiva de caché (paso 3). Si el TTL mínimo ya es muy corto, es posible que este no sea el problema. |
| Tráfico normal (no agéntico) interrumpido tras la configuración | Error de configuración de la directiva de caché | Si ha creado una nueva directiva de caché (Escenario C), asegúrese de que ha replicado toda la configuración de la directiva administrada original. |

## Desactivación y reactivación de Optimize en Edge

La función de Lambda@Edge (`edgeoptimize-origin`) está asociada a los eventos de solicitud de origen y respuesta de origen del comportamiento de CloudFront. Dado a que se ejecuta en línea en cada solicitud que pasa por ese comportamiento —tanto de personas como agéntica— una interrupción de Lambda@Edge afectará todo el tráfico en directo, no solo a las solicitudes agénticas. Si detecta una interrupción de Lambda@Edge, quite las asociaciones de funciones inmediatamente para restaurar el flujo de tráfico normal a su origen predeterminado.

### Cómo detectar una interrupción de Lambda@Edge

* **AWS Service Health Dashboard**: compruebe el [AWS Service Health Dashboard](https://health.aws.amazon.com/health/status) para ver si hay algún incidente activo que afecte a **Amazon CloudFront** o **AWS Lambda**. Una interrupción global o regional notificada aquí es la forma más rápida de confirmar que el problema se encuentra en la infraestructura de AWS y no en su configuración.
* **Errores de Lambda@Edge**: vaya a **Consola de AWS > CloudFront > Monitorización >[Su distribución]**. Abra la pestaña **Errores de Lambda@Edge** y revise el gráfico **Errores de ejecución** para detectar errores de ejecución. Si estos valores son altos, Lambda@Edge podría estar inactivo.

### Desasociar la función Lambda@Edge

**Navegación:** Consola de AWS > CloudFront > Distribuciones >[Su distribución] > Comportamientos

1. Haga clic en **Editar** en su comportamiento.

2. Desplácese hacia abajo hasta la sección **Asociaciones de funciones**.

3. Establezca las siguientes asociaciones en **Ninguna asociación**:

   | Evento | Cambiar a |
   |---|---|
   | Solicitud del visor | Ninguna asociación |
   | Solicitud de origen | Ninguna asociación |
   | Respuesta de origen | Ninguna asociación |

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Haga clic en **Guardar cambios**.

5. Espere a que finalice la implementación de la distribución de CloudFront. El estado cambia de **Implementando** a la fecha de última modificación, normalmente en cuestión de minutos.

Una vez implementada, todo el tráfico se dirigirá directamente a su origen predeterminado. No se elimina ninguna configuración; la función Lambda y sus asociaciones se pueden restaurar en cualquier momento.

### Volver a adjuntar la función Lambda@Edge

**Navegación:** Consola de AWS > CloudFront > Distribuciones >[Su distribución] > Comportamientos

1. Haga clic en **Editar** en su comportamiento.

2. Desplácese hacia abajo hasta la sección **Asociaciones de funciones**.

3. Restaure las asociaciones:

   | Evento | Establecer en |
   |---|---|
   | Solicitud del visor | `edgeoptimize-routing` (función CloudFront) |
   | Solicitud de origen | ARN de Lambda con versión del paso 4 |
   | Respuesta de origen | ARN de Lambda con versión del paso 4 |

   Use el **ARN de la función** con versiones que anotó en el paso 4 (en **Publicar una versión**).

   ![Configuración de asociaciones de funciones](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Haga clic en **Guardar cambios**.

5. Espere a que la distribución termine de implementarse y, a continuación, compruebe que las solicitudes agénticas devuelven el encabezado `x-edgeoptimize-request-id` tal como se describe en el paso 6.

{{return-to-overview}}
