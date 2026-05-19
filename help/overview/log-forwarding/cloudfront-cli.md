---
title: 'Reenvío de registros: CloudFront (CLI de AWS)'
description: Reenvíe registros de CDN de CloudFront al bloque S3 de Adobe mediante la CLI de AWS para las operaciones de configuración y envío.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:42:44.992Z'
TQID: 'https://experienceleague.adobe.com/NoVv3qv1RbtqAWGMPYC1Rz4wO-5Au1yL2e8tRKd9Hao'
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
source-wordcount: 379
ht-degree: 100%

---


# Reenvío de registros: CloudFront (CLI de AWS) {#log-forwarding-cloudfront-cli}

En esta página se explica con detalle cómo reenviar registros de CDN de CloudFront al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos que se indican en esta página para configurar el reenvío de registros mediante la [Interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/) en el [Paso 2](#step-2-cli).

>[!NOTE]
>
> En esta guía se explica cómo configurar el reenvío de registros mediante la [Interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/). Si desea configurar el reenvío de registros usando la **IU de CloudFront**, consulte [Reenvío de registros: CloudFront](/help/overview/log-forwarding/cloudfront.md).

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

<!--  ![AWS Account ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)-->

1. Seleccione **CloudFront (BYOCDN)**.

   ![Seleccionar CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Haga clic en **Incorporar**.

<!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Paso 2: Configurar el reenvío de registros de CDN con la CLI de AWS {#step-2-cli}

Configure el reenvío de registros de CDN con la CLI de AWS de la siguiente manera:

### Configurar las credenciales de CLI de AWS

Configure las credenciales de CLI de AWS en MAC. Abra ~/.aws/credentials e introduzca los valores de las variables siguientes:

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### Probar la conexión

Ejecute el siguiente comando para probar la conexión:

```bash
aws sts get-caller-identity --profile LLMO
```

Ejemplo de salida correcta:

```bash
aws sts get-caller-identity --profile LLMO
{
    "UserId": "AxxxxxxxxxxxP:user",
    "Account": "012345678912",
    "Arn": "arn:aws:sts::012345678912:assumed-role/klam-master-role-BatlY3dnPVinQLC/user"
}
```

### Inicializar las variables

Reemplace `REPLACEME123@AdobeOrg` por su ID de organización de Adobe IMS de organización y ejecute el comando siguiente. El identificador de salida de este comando se denominará `TRANSFORM_IMS_ID`.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

Escriba los valores de `CUSTOMER`, `CDN_ID`, `ACCT1` y `TRANSFORM_IMS_ID` siguiendo las directrices que se indican a continuación y ejecute los comandos desde el terminal.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>-ams  ## Replace TRANSFORM_IMS_ID with the output of the command above
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### Crear la fuente de envío

Desde el mismo terminal en el que se ejecutó el paso 3, ejecute el siguiente comando:

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>Si recibe el siguiente error, busque la fuente de envío existente: *Se produjo un error (ConflictException) al llamar a la operación PutDeliverySource: este ResourceId ya se ha utilizado en otra Fuente de envío en esta cuenta.*
>
>Para buscar la fuente de envío existente, ejecute este comando:
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>En el siguiente comando, utilice el nombre de la fuente de envío de los resultados del comando anterior.

### Crear la configuración del envío

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

&lt;!--Alinee `--record-fields` y `--s3-delivery-configuration` con la lista de campos y el sufijo de ruta que se muestra en la página de configuración de la CDN de LLM Optimizer si cambian los valores de la documentación o del producto.-->
