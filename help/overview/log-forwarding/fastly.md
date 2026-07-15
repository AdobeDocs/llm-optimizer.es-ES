---
title: 'Reenvío de registros: Fastly'
description: Aprenda a reenviar registros de CDN de Fastly al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-07-15T17:51:11.580Z'
TQID: 'https://experienceleague.adobe.com/HPUxzfbvA4DtdNmjgTMvVVv-WqtjPcAUeZmg8JdvL-s'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 100%

---


# Reenvío de registros: Fastly {#log-forwarding-fastly}

En esta página se explica cómo reenviar registros CDN de Fastly al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos que se indican en esta página para configurar el reenvío de registros en la consola web de Fastly.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Configuración**

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la pestaña **Configuración de la CDN**.

   ![Pestaña Configuración de la CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Empezar**.
1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)
1. Seleccione **Fastly (BYOCDN)**.

   ![Seleccione Fastly](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. Haga clic en **Incorporar**.

## Paso 2: Crear un punto final S3 en Fastly {#step-2}

Para crear un punto final S3, en el **Panel de control de Fastly**:

1. En el panel de control de Fastly, vaya a **Servicios de CDN** (no a Servicios de computación).
1. En el área de **Amazon Web Services S3**, haga clic en **Crear punto final**.
1. Rellene los campos de **Crear un punto final de Amazon S3**:

| Campo | Descripción |
| --- | --- |
| **Nombre** | Nombre legible en lenguaje natural para el punto final. |
| **Ubicación** | Predeterminado |
| **Formato de registro** | Utilice la cadena de formato de registro que se muestra en la sección **Cadena de formato de registro** que viene a continuación. |
| **Formato de marca de tiempo** | `%Y-%m-%dT%H:%M:%S.000` |
| **Nombre del bloque** | Copie el **Nombre del bloque** en la página de configuración de LLM Optimizer. ![Nombre del bloque](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Dominio** | Copie el **Nombre de dominio** de la página de configuración de LLM Optimizer. ![Nombre de dominio](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **Método de acceso** | **Credenciales de usuario** |
| **Credenciales de usuario** | Copie la **Clave de acceso** y la **Clave secreta** en la página de configuración de LLM Optimizer. ![Claves de acceso](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Período** | `300` |

**Cadena de formato de registro:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>Los administradores de contraseñas pueden rellenar automáticamente el campo **Clave secreta** con su contraseña de Fastly. Si la integración con AWS falla, introduzca la clave secreta manualmente.

Después de completar los pasos anteriores, haga clic en **Opciones avanzadas** y establezca lo siguiente:

| Campo | Descripción |
| --- | --- |
| **Ruta** | Copie **Ruta** en la página de configuración de LLM Optimizer. ![Ruta](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **Seleccionar un formato de línea de registro** | En blanco |
| **Compresión** | Gzip |
| **Nivel de redundancia** | Estándar |
| **ACL** | Ninguna |
| **Cifrado del lado del servidor** | Ninguna |
| **Bytes máximos** | 0 |

Después de configurar las opciones avanzadas:

1. Haga clic en **Crear** para crear el punto final.
1. En el menú **Activar**, seleccione **Activar en producción** para implementar.

>[!NOTE]
>
>Fastly transmite los registros de forma continua a S3, pero el sitio web y la API de S3 solo permiten que los archivos estén disponibles una vez finalizada la carga.

### Ejemplo de entrada de registro {#example}

A continuación se presenta un ejemplo de cadena de formato para enviar datos a Amazon S3:

```json
{
  "timestamp": "2026-02-10T05:05:36+0000",
  "host": "example.com",
  "url": "/my/path",
  "request_method": "GET",
  "request_referer": "https://example.com/my/other/path",
  "request_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
  "response_status": 200,
  "response_content_type": "text/css; charset=utf-8",
  "client_country_code": "argentina",
  "time_to_first_byte": "0.138"
}
```
