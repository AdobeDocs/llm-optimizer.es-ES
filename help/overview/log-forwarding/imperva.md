---
title: 'Reenvío de registros: Imperva'
description: Aprenda a reenviar registros de CDN de Imperva al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:52:22.260Z'
TQID: 'https://experienceleague.adobe.com/y2ticpRCNZjPYJ6wHg-V3QWxBnGF--mQfqGBYjVjKXY'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 4%

---


# Reenvío de registros: Imperva {#log-forwarding-imperva}

En esta guía se explica cómo reenviar los registros de CDN de Imperva al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos proporcionados en esta página para configurar el reenvío de registros desde la consola web de Imperva.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Configuración**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la ficha **Configuración de CDN**.

   ![Ficha Configuración de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Haga clic en **Comenzar**.
1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)
1. Seleccione **Imperva (BYOCDN)**.

   ![Seleccionar Imperva](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Haga clic en **Incorporar**.

## Paso 2: Configurar el reenvío de registros en Imperva {#step-2}

En la [consola Imperva](https://my.imperva.com):

>[!NOTE]
>
>Los registros deben enviarse diariamente.

1. Inicie sesión en su cuenta de Imperva en [https://my.imperva.com](https://my.imperva.com).

2. En la barra lateral, vaya a **Registros** > **Configuración de registro** (o **Integración de registro**).

3. Seleccione **Amazon S3 ARN** como tipo de conexión (destino de registro).

4. Escriba lo siguiente:

   | Campo | Descripción | Nota |
   |---|---|---|
   | **Nombre de conexión** | Un nombre descriptivo para la conexión (por ejemplo, registros de Production S3). Puede cambiar el nombre del valor predeterminado. | |
   | **Ruta** | Ubicación de la carpeta donde se almacenarán los archivos de registro. Usar el formato `<Amazon S3 bucket name>/<log folder>`. Por ejemplo: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name` es el **nombre del contenedor** de la página de configuración de LLM Optimizer. ![Nombre del contenedor](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) La carpeta de registro es **Ruta** de la página de configuración de LLM Optimizer. ![Ruta](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Haga clic en **Probar conexión**. Imperva ejecuta una prueba completa en la que un archivo de prueba (sin datos reales) se envía a la carpeta designada y luego se elimina cuando se completa la transferencia.

   - **Disponible**: los detalles de almacenamiento son válidos; puede configurar registros para utilizar esta conexión.
   - **Sin definir**: faltan los detalles necesarios o la prueba ha fallado.

6. Haga clic en **Guardar** para almacenar la configuración.

7. Configure las opciones de registro (tipos de registro, nivel de registro, formato y compresión) y **Niveles de registro**. Puede obtener los valores desde la página de configuración de LLM Optimizer.

   | Campo | Nota |
   |---|---|
   | Modo de integración de registros | ![Modo de integración de registros](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Método de envío | ![Método de envío](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Tipos de registro | ![Tipos de registro](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Nivel de registro | ![Nivel de registro](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Formato | ![Formato](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Comprimir registros | ![Comprimir registros](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
