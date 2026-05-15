---
title: 'Reenvío de registros: CloudFront'
description: Aprenda a reenviar registros de CDN de CloudFront al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:43:07.178Z'
TQID: 'https://experienceleague.adobe.com/TXnY-eK1SUuKrlVoGWd2hZO5bjUqEspvyFmcyOuei3Q'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 0%

---


# Reenvío de registros: CloudFront {#log-forwarding-cloudfront}

En esta página se explica cómo reenviar registros de CDN de CloudFront al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos proporcionados en esta página para configurar el reenvío de registros en la consola del panel de CloudFront.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Panel de configuración del cliente**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la ficha **Configuración de CDN**.

   ![Ficha Configuración de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Comenzar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Escriba su **ID de cuenta de AWS**.

   ![ID de cuenta de AWS](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. Seleccione **CloudFront (BYOCDN)**.

   ![Seleccionar CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Haga clic en **Incorporar**.

   ![Botón de incorporación](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Paso 2: Habilitar el registro estándar (consola de CloudFront) {#step-2}

Para habilitar el registro estándar, en [AWS Management console](https://aws.amazon.com/console/):

1. Acceda a la consola [CloudFront](https://console.aws.amazon.com/cloudfront/v4/home) y [actualice una distribución existente](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure).

1. Abra la ficha **Registro**.

1. Elija **Add** y, a continuación, seleccione el servicio para recibir registros, en este caso **Amazon S3**.

1. Para **Destino**, seleccione o cree el recurso. Escriba el **nombre del contenedor**, puede copiar el valor desde la página de configuración de CDN de LLM Optimizer.

   ![Nombre del contenedor de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. Configurar **ajustes adicionales**:

   - **Selección de campo**: elija los campos del archivo de registro. Consulte los campos obligatorios en la página de configuración de CDN de LLM Optimizer.

     ![Selección de campo de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **Partición**: copie el **sufijo de ruta** de la página de configuración de LLM Optimizer.

     ![Partición de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **Formato de salida** — el formato debe ser JSON.

     ![Formato de salida de CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. Complete los pasos para actualizar o crear la distribución.

1. En la página **Registros**, confirme que **Habilitado** aparece junto a la distribución.

## Habilitar el registro estándar para la entrega entre cuentas {#cross-account}

La **cuenta de origen** (con la distribución de CloudFront) envía registros de acceso a la **cuenta de destino** (el contenedor de S3 que se muestra en la página de configuración de CDN de LLM Optimizer). Ambas cuentas deben tener los permisos adecuados.

Por ejemplo: la cuenta de origen `111111111111` envía registros a un bloque S3 en la cuenta de destino `222222222222`. Puede usar la [Interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/).

>[!NOTE]
>
>En los comandos siguientes, reemplace el valor ARN de destino de entrega (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) por el valor de **ARN de destino de entrega** de la página de configuración de LLM Optimizer.

![ARN de destino de envío](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### Configuración de la cuenta de origen {#source-account}

A continuación, debe configurar la cuenta de origen:

1. **Crear un origen de entrega**; reemplace el nombre y el ARN de distribución:

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **Cree la entrega** - vincule el origen al destino; use el ARN de destino desde el paso &quot;Configurar la cuenta de destino&quot;:

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **Verificar:**

   - En la cuenta de **source**: consola de CloudFront > su distribución > pestaña **Registro**. En **Tipo** debería ver el envío de registro entre cuentas de S3.
   - En la cuenta de **destination**: consola S3 > contenedor. Debería ver el prefijo (por ejemplo, `MyLogPrefix`) y los registros de esa carpeta.
