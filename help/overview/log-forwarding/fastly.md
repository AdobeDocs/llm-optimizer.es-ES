---
title: 'Reenvío de registros: Fastly'
description: Aprenda a reenviar registros de CDN de Fastly al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 4%

---


# Reenvío de registros: Rápido {#log-forwarding-fastly}

En esta página se explica cómo reenviar registros de CDN de Fastly al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico. Utilizará la página de configuración de CDN de LLM Optimizer para incorporarse a LLM Optimizer. Una vez completado el proceso de incorporación, siga los pasos proporcionados en esta página para configurar el reenvío de registros en la consola web de Fastly.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En la página de LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vaya a **Configuración**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la ficha **Configuración de CDN**.

   ![Ficha Configuración de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Comenzar**.
1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)
1. Seleccione **Fastly (BYOCDN)**.

   ![Seleccionar rápidamente](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. Haga clic en **Incorporar**.

## Paso 2: Crear un extremo S3 en Fastly {#step-2}

Para crear un extremo S3, en el **Panel de control de Campaign de Fastly**:

1. En el panel de Fastly, vaya a **servicios CDN** (no servicios de cómputo).
1. En el área de **Amazon Web Service S3**, haga clic en **Crear extremo**.
1. Rellene los campos **Crear un extremo de Amazon S3**:

| Campo | Descripción |
| --- | --- |
| **Nombre** | Nombre legible en lenguaje natural para el punto final. |
| **Ubicación** | Predeterminado |
| **Formato de registro** | Utilice la cadena de formato de registro que se muestra en la sección **Cadena de formato de registro** a continuación. |
| **Formato de marca de hora** | `%Y-%m-%dT%H:%M:%S.000` |
| **Nombre del contenedor** | Copie el **Nombre del contenedor** de la página de configuración de LLM Optimizer. ![Nombre del contenedor](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Dominio** | Copie el **Nombre de dominio** de la página de configuración de LLM Optimizer. ![Nombre de dominio ](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **Método de acceso** | **Credenciales de usuario** |
| **Credenciales de usuario** | Copie la **clave de acceso** y la **clave secreta** de la página de configuración de LLM Optimizer. ![Claves de acceso](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Período** | `300` |

**Cadena de formato de registro:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>Los administradores de contraseñas pueden rellenar automáticamente el campo **Clave secreta** con su contraseña de Fastly. Si la integración de AWS falla, introduzca la clave secreta manualmente.

Después de completar los pasos anteriores, haga clic en **Opciones avanzadas** y establezca:

| Campo | Descripción |
| --- | --- |
| **Ruta** | Copie **Ruta** de la página de configuración de LLM Optimizer. ![Ruta](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **Seleccionar un formato de línea de registro** | En blanco |
| **Compresión** | Gzip |
| **Nivel de redundancia** | Estándar |
| **ACL** | Ninguna |
| **Cifrado del lado del servidor** | Ninguna |
| **Bytes máximos** | 0 |

Después de configurar las opciones avanzadas:

1. Haga clic en **Crear** para crear el extremo.
1. En el menú **Activar**, seleccione **Activar en producción** para implementar.

>[!NOTE]
>
>Transmite rápidamente los registros continuamente a S3, el sitio web y la API de S3 solo hacen que los archivos estén disponibles una vez completada la carga.

### Ejemplo de entrada de registro {#example}

A continuación se muestra un ejemplo de cadena de formato para enviar datos a Amazon S3:

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
