---
title: 'Reenvío de registros: Cloudflare'
description: Aprenda a reenviar registros de CDN de Cloudflare al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:41:23.688Z'
TQID: 'https://experienceleague.adobe.com/AfhcMa7tZ3L-4qCbNKiblInALmHaKxWLtL-O-Hkvc-U'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 0%

---


# Reenvío de registros: Cloudflare {#log-forwarding-cloudflare}

Esta página detalla cómo reenviar los registros de CDN de Cloudflare al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos proporcionados en esta página para configurar el reenvío de registros en la consola del panel de Cloudflare.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Panel de configuración del cliente**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la ficha **Configuración de CDN**.

   ![Ficha Configuración de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Comenzar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Seleccione **Cloud Flare (BYOCDN)**.

   ![Seleccionar Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. Haga clic en **Incorporar**.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Paso 2: Crear un trabajo de Logpush en Cloudflare {#step-2}

En el [tablero de Cloudflare](https://dash.cloudflare.com/login), siga estos pasos:

1. Vaya a la página **Logpush** en el nivel **Dominio (zona)**.
1. Seleccione **Crear un trabajo Logpush**.
1. En **Seleccionar un destino**, elija **Amazon S3**.
1. Introduzca la siguiente información de destino:

   - **Bucket**: el nombre del contenedor de S3. Copie el valor de la página Configuración de CDN de LLM Optimizer.

     ![Nombre del contenedor](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **Ruta**: la ubicación del contenedor dentro del contenedor de almacenamiento. Copie el valor de la página Configuración de CDN de LLM Optimizer.

     ![Ruta de acceso de Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **Organizar registros en subcarpetas diarias** (recomendado).

     ![Subcarpetas diarias](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **Región del contenedor**: copie el valor de la página Configuración de CDN de LLM Optimizer.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - Si no se necesita cifrado del lado del servidor, deje sin marcar.

   Después de completar los pasos anteriores, selecciona **Continuar**.

1. Para probar la propiedad, Cloudflare enviará un archivo a su destino designado. Para encontrar el token, haga clic en el botón **Abrir** en la ficha **Información general** del archivo de desafío de propiedad. Copie el token de propiedad de la página de configuración de la CDN de LLM Optimizer y péguelo en el panel de Cloudflare para comprobar su acceso al bloque. Escriba el token de propiedad y seleccione **Continuar**.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. Seleccione el conjunto de datos **Solicitudes HTTP** que desea insertar en el servicio de almacenamiento.

1. Configure el trabajo de Logpush:

   - Escriba **Nombre de trabajo**.

   - En **Enviar los campos siguientes**, vea los valores en la página de configuración de LLM Optimizer.

     ![Campos Logpush](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **Formato de registro**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. En **Opciones avanzadas**:

   - Elija el formato de los campos de marca de tiempo en los registros: `RFC3339`.

     ![Formato de marca de hora](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - Para las tasas de muestreo, seleccione **Todos los registros**.

     ![Velocidad de muestreo](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Seleccione **Enviar** una vez que haya terminado de configurar el trabajo Logpush.
