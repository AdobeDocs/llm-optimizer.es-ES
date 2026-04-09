---
title: 'Reenvío de registros: CloudFront (CLI de AWS)'
description: Reenvíe los registros de CDN de CloudFront al bloque S3 de Adobe mediante la CLI de AWS para la configuración y las operaciones de entrega.
feature: Agentic Traffic
source-git-commit: 0d51bbde954c399dc6595522fa70b576461f458a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# Reenvío de registros: CloudFront (CLI de AWS) {#log-forwarding-cloudfront-cli}

Esta página detalla cómo reenviar los registros de CDN de CloudFront al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos proporcionados en esta página para configurar el reenvío de registros mediante la [Interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/) en [Paso 2](#step-2-cli).

>[!NOTE]
>
> En esta guía se explica cómo configurar el reenvío de registros mediante la [Interfaz de línea de comandos de AWS](https://aws.amazon.com/cli/). Si desea configurar el reenvío de registros usando la **IU de CloudFront**, consulte [Reenvío de registros: CloudFront](/help/overview/log-forwarding/cloudfront.md).

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

## Paso 2: Configurar el reenvío de registros de CDN con AWS CLI {#step-2-cli}

Configure el reenvío de registros de CDN con la CLI de AWS de la siguiente manera:

### Configurar las credenciales de CLI de AWS

Configure la credencial MAC de CLI de AWS. Abra ~/.aws/credentials e introduzca los valores de las variables siguientes:

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### Prueba de la conexión

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

### Inicializar variables

Reemplace `REPLACEME123@AdobeOrg` por su ID de organización de Adobe IMS de organización y ejecute el comando siguiente. El identificador de salida de este comando se denominará `TRANSFORM_IMS_ID`.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

Escriba los valores de `CUSTOMER`, `CDN_ID`, `ACCT1` y `TRANSFORM_IMS_ID` siguiendo las directrices que se indican a continuación y, a continuación, ejecute comandos desde el terminal.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>-ams  ## Replace TRANSFORM_IMS_ID with the output of the command above 
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### Creación del origen de entrega

Desde el mismo terminal en el que se ejecutó el paso 3, ejecute el siguiente comando:

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>Si recibe el siguiente error, busque el origen de entrega existente: *Se produjo un error (ConflictException) al llamar a la operación PutDeliverySource: ResourceId ya se ha utilizado en otra Source de entrega de esta cuenta.*
>
>Para buscar el origen de entrega existente, ejecute este comando:
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>En el siguiente comando, utilice el nombre de origen de entrega de los resultados del comando anterior.

### Creación de la configuración de envío

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

&lt;!—Alinee `--record-fields` y `--s3-delivery-configuration` con la lista de campos y el sufijo de ruta que se muestra en la página de configuración de CDN de LLM Optimizer si cambian los valores de la documentación o del producto.—>
