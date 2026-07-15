---
title: 'Reenvío de registros: CloudFront'
description: Aprenda a reenviar registros de CDN desde CloudFront al bloque S3 de Adobe para la recopilación de datos del tráfico agéntico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-07-15T17:47:22.372Z'
TQID: 'https://experienceleague.adobe.com/0aPeInYmcNRZLHUdABG2cEpT-dXb6GhEMoNUqMLMusY'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1id: e69d5a42-0217-4ca5-9396-a9a826a170daid: e06fae5f-830b-4222-a469-b5e148d36465
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 100%

---


# Reenvío de registros: CloudFront {#log-forwarding-cloudfront}

En esta página se explica cómo reenviar registros de CDN desde CloudFront al bloque S3 de Adobe para la recopilación de datos del tráfico agéntico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos que se indican en esta página para configurar el reenvío de registros en la consola del panel de control de CloudFront.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya al **panel de control Configuración del cliente**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la pestaña **Configuración de la CDN**.

   ![Pestaña Configuración de la CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Empezar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Escriba su ID de la **cuenta de AWS**

   ![ID de la cuenta de AWS](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. Seleccione **CloudFront (BYOCDN)**.

   ![Seleccionar CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Haga clic en **Incorporar**.

   ![Botón Incorporar](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Paso 2: Habilitar el registro estándar (consola de CloudFront) {#step-2}

Para habilitar el registro estándar, desde la [Consola de administración de AWS](https://aws.amazon.com/console/):

1. Acceda a la [consola de CloudFront](https://console.aws.amazon.com/cloudfront/v4/home) y [actualice una distribución existente](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure).

1. Abra la pestaña **Registro**.

1. Seleccione **Añadir** y luego seleccione el servicio para recibir registros, en este caso **Amazon S3**.

1. Para **Destino**, seleccione o cree el recurso. Escriba el **nombre del bloque**; puede copiar el valor desde la página de configuración de CDN de LLM Optimizer.

   ![Nombre del bloque de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. Defina **Configuración adicional**:

   - **Selección de campo**: elija los campos del archivo de registro. Consulte los campos obligatorios en la página de configuración de CDN de LLM Optimizer.

     ![Selección de campo de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **Particionamiento**: copie el **sufijo de ruta** en la página de configuración de LLM Optimizer.

     ![Particionamiento de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **Formato de salida**: el formato debe ser JSON.

     ![Formato de salida de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. Complete los pasos para actualizar o crear la distribución.

1. En la página **Registros**, confirme que **Habilitado** aparece junto a la distribución.

## Habilitar el registro estándar para el envío entre cuentas {#cross-account}

La **cuenta de origen** (con la distribución de CloudFront) envía registros de acceso a la **cuenta de destino** (el bloque S3 que se muestra en la página de configuración de CDN de LLM Optimizer). Ambas cuentas deben tener los permisos adecuados.

Por ejemplo: la cuenta de origen `111111111111` envía registros a un bloque S3 en la cuenta de destino `222222222222`. Puede utilizar la [interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/).

>[!NOTE]
>
>En los comandos siguientes, reemplace el valor del ARN de destino del envío (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) por el valor de **ARN de destino del envío** en la página de configuración de LLM Optimizer.

![ARN de destino del envío](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### Configurar la cuenta de origen {#source-account}

A continuación, deberá configurar la cuenta de origen:

1. **Crear un origen de envío**; reemplace el nombre y el ARN de distribución:

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **Crear el envío**: vincule el origen al destino; utilice el ARN de destino del paso “Configurar la cuenta de destino”:

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **Verificar:**

   - En la cuenta de **origen**: Consola de CloudFront > su distribución > pestaña **Registro**. En **Tipo** debería ver el envío de registros entre cuentas de S3.
   - En la cuenta de **destino**: consola S3 > bloque. Debería ver el prefijo (por ejemplo, `MyLogPrefix`) y los registros de esa carpeta.
