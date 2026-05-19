---
title: 'Reenvío de registros: Akamai'
description: Aprenda a reenviar registros de CDN de Akamai al bloque S3 de Adobe para la recopilación de datos del tráfico agéntico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:35:22.816Z'
TQID: 'https://experienceleague.adobe.com/cO-qqOveWFee1-QnVSlzmO-n383sptHl59Ni2qQcvAU'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 100%

---


# Reenvío de registros: Akamai {#log-forwarding-akamai}

Esta página se explica cómo reenviar registros de CDN de Akamai al bloque S3 de Adobe para la recopilación de datos del tráfico agéntico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos que se indican en esta página para configurar el reenvío de registros en el Panel de control de Akamai.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya al **panel de control Configuración del cliente**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la pestaña **Configuración de la CDN**.

   ![Pestaña Configuración de la CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Empezar**.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Seleccione **Akamai (BYOCDN)**.

   ![Seleccionar Akamai](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. Haga clic en **Incorporar**.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Paso 2: Crear un flujo en Akamai. {#step-2}

En el panel de control de Akamai [https://control.akamai.com/](https://control.akamai.com/), siga los pasos de la documentación oficial de Akamai para [crear un flujo](https://techdocs.akamai.com/datastream2/docs/create-stream).

## Paso 3: Elegir parámetros de datos {#step-3}

Después de crear el flujo, en el panel de control de Akamai, haga clic en Siguiente para continuar hasta la pestaña **Conjuntos de datos**. Siga los pasos de la documentación oficial de Akamai para elegir los [parámetros de datos](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters). Se necesitarán los siguientes campos de la configuración de LLM Optimizer:

![Campos de configuración de LLMO](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

La asignación debe ser la siguiente:

* **Información de registro**
reqTimeSec -> Hora de solicitud
* **Datos geográficos**
país -> País/Región
* **Datos de intercambio de mensajes**
reqHost -> Host de solicitud
reqPath -> Ruta de solicitud
queryStr -> Cadena de consulta
reqMethod -> Método de solicitud
ua -> Usuario-Agente
statusCode -> Código de estado HTTP
rspContentType -> Tipo de contenido de respuesta
* **Datos del encabezado de solicitud**
referer -> Referente
* **Datos de rendimiento de la red**
timeToFirstByte -> Tiempo hasta el primer byte

Los campos del conjunto de datos de Akamai (incluidos los ID) son los siguientes:

1100, # reqTimeSec -> Hora de solicitud
2012, # country -> País/Región
1011, # reqHost -> Host de solicitud
1013, # reqPath -> Ruta de solicitud
2009, # queryStr -> Cadena de consulta
1012, # reqMethod -> Método de solicitud
1017, # ua -> Usuario-Agente
1008, # statusCode -> Código de estado HTTP
1032, # referer -> Referente
1016, # rspContentType -> Tipo de contenido de respuesta
2025 # timeToFirstByte -> Tiempo hasta el primer byte

## Paso 4: Configurar el destino {#step-4}

Después de crear los flujos de datos y elegir los parámetros, debe configurar el destino. Para configurar el destino, siga estos pasos:

1. En **Destino**, seleccione **S3**.
2. En **Nombre**, escriba una descripción legible en lenguaje natural para el destino.
3. En **Bloque**, copie **Nombre del bloque** de la página de configuración de LLM Optimizer.

   ![Nombre del bloque](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. En **Ruta de la carpeta**, copie la **Ruta** en la página de configuración de LLM Optimizer.

   ![Configuración de ruta](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. En **Región**, copie la **Región** en la página de configuración de LLM Optimizer.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. En **Identificador de clave de acceso** y **Clave de acceso secreta**, copie ambos valores de la página de configuración de LLM Optimizer.

   ![Claves de acceso](/help/overview/assets/log-forwarding/common/access-keys.png)

7. Haga clic en **Validar y guardar** para validar la conexión con el destino y guarde los detalles que ha proporcionado. Como parte de este proceso de validación, el sistema utiliza el identificador de clave de acceso y la clave de acceso secreta proporcionados para crear un archivo de verificación en la carpeta S3, con una marca de tiempo en el nombre de archivo con el formato `Akamai_access_verification_[TimeStamp].txt`. Solo puede ver este archivo si el proceso de validación se ha realizado correctamente y tiene acceso al bloque y a la carpeta de Amazon S3 a los que está intentando enviar registros.

8. En el menú **Opciones de envío**, edite el campo **Nombre de archivo** de la siguiente manera:

   a. Cambie el **prefijo**. Copie el valor de la página de configuración de LLM Optimizer en **Prefijo del archivo de registro**:

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b. Cambie el **sufijo**. Copie el valor de la página de configuración de LLM Optimizer en **Sufijo del archivo de registro**.

9. Cambie la **Frecuencia de inserción**. Copie el valor de la página de configuración de LLM Optimizer en **Intervalo de registro**.

   ![Intervalo de registro](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. Haga clic en **Siguiente** para completar el proceso.

Antes de la validación final, la configuración debería ser similar a la de este ejemplo:

![Validación de la configuración](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
