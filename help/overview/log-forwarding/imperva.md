---
title: 'Reenvío de registros: Imperva'
description: Aprenda a reenviar registros de CDN de Imperva al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-07-15T17:57:30.264Z'
TQID: 'https://experienceleague.adobe.com/l-DYz7pXzFDqZn1rnZWUOG9PpRqosq00LmGrlsOMqNk'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: dd952468-5202-43af-a365-6e0d2e67a703
  - id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: ht
source-wordcount: 352
ht-degree: 100%

---


# Reenvío de registros: Imperva {#log-forwarding-imperva}

En esta guía se explica cómo reenviar registros de CDN de Imperva al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos que se indican en esta página para configurar el reenvío de registros desde la consola web de Imperva.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Configuración**

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la pestaña **Configuración de la CDN**.

   ![Pestaña Configuración de la CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Haga clic en **Empezar**.
1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)
1. Seleccione **Imperva (BYOCDN)**.

   ![Seleccionar Imperva](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Haga clic en **Incorporar**.

## Paso 2: Configurar el reenvío de registros en Imperva {#step-2}

En la [consola de Imperva](https://my.imperva.com):

>[!NOTE]
>
>Los registros deben enviarse diariamente.

1. Inicie sesión en su cuenta de Imperva en [https://my.imperva.com](https://my.imperva.com).

2. En la barra lateral, vaya a **Registros** > **Configuración de registro** (o **Integración de registro**).

3. Seleccione **Amazon S3 ARN** como tipo de conexión (destino de registro).

4. Escriba lo siguiente:

   | Campo | Descripción | Nota |
   |---|---|---|
   | **Nombre de la conexión** | Un nombre descriptivo para la conexión (por ejemplo, registros S3 de producción). Puede cambiar el nombre del valor predeterminado. | |
   | **Ruta** | Ubicación de la carpeta donde se almacenarán los archivos de registro. Utilice el formato `<Amazon S3 bucket name>/<log folder>`. Por ejemplo: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name` es el **Nombre del bloque** de la página de configuración del LLM Optimizer. ![Nombre del bloque](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) La carpeta de registro es **Ruta** en la página de configuración de LLM Optimizer. ![Ruta](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Haga clic en **Probar conexión**. Imperva realiza una prueba completa en la que se envía un archivo de prueba (sin datos reales) a la carpeta designada y, una vez completada la transferencia, se elimina.

   - **Disponible**: los detalles de almacenamiento son válidos; puede configurar los registros para utilizar esta conexión.
   - **Sin definir**: faltan los detalles necesarios o la prueba falló.

6. Haga clic en **Guardar** para guardar la configuración.

7. Configure las opciones de registro (tipos de registro, nivel de registro, formato, compresión) y **niveles de registro**. Puede obtener los valores en la página de configuración de LLM Optimizer.

   | Campo | Nota |
   |---|---|
   | Modo de integración de registro | ![Modo de integración de registro](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Método de envío | ![Método de envío](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Tipos de registros | ![Tipos de registros](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Nivel de registro | ![Nivel de registro](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Formato | ![Formato](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Comprimir registros | ![Comprimir registros](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
