---
title: 'Reenvío de registros: otros (carga manual)'
description: Aprenda a cargar manualmente registros de CDN al bloque S3 de Adobe para la recopilación de datos de tráfico agéntico en LLM Optimizer cuando utilice un proveedor de CDN no compatible.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:54:15.685Z'
TQID: 'https://experienceleague.adobe.com/YBfhS4oM0qYRkFvS3zPzzcFAeLNBucRH5QmMBUH8h4E'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 670
ht-degree: 100%

---


# Reenvío de registros: otros (carga manual) {#log-forwarding-other}

El método de aprovisionamiento **Otro BYOCDN** es una opción general para los clientes que desean proporcionar registros de CDN a LLM Optimizer cuando:

- Se prefieren **cargas manuales**: por ejemplo, los equipos operativos exportan los registros y los cargan periódicamente.
- Se utilizan **procesos automatizados ad hoc**: scripts únicos, exportaciones programadas, trabajos sin servidor.
- El cliente utiliza una **CDN que no es compatible de forma nativa** con las integraciones de reenvío de registros integradas.

Este método imita el modelo de “reenvío continuo”: los registros se generan y se cargan en la ubicación S3 prevista y, finalmente, son procesados automáticamente por las canalizaciones de ingesta.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En [LLM Optimizer](https://llmo.now/):

1. Vaya a **Configuración**

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la pestaña **Configuración de la CDN**.

   ![Pestaña Configuración de la CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Empezar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Seleccione **Otros**.

   ![Seleccionar otros](/help/overview/assets/log-forwarding/other/other-select.png)

1. Haga clic en **Incorporar**.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Paso 2: Preparar y cargar los registros {#step-2}

### Formato de registro obligatorio (líneas JSON) {#log-format}

Los registros deben cargarse en formato JSON delimitado por saltos de línea (**un objeto JSON por línea**). Cada línea de registro debe incluir los siguientes campos **tal y como se indica a continuación**.

#### Esquema campo por campo {#schema}

| Campo | Tipo | Descripción | Ejemplos |
|---|---|---|---|
| **timestamp** | Cadena | La marca de tiempo de la solicitud que tiene el formato **ISO 8601**. | `"2025-02-01T23:00:05Z"` |
| **host** | Cadena | El dominio web que solicitó el cliente. | `"www.example.com"` |
| **URL** | Cadena | La **ruta** y los **parámetros de consulta** son obligatorios, mientras que el dominio **no** debe incluirse. | `"/home?utm_source=google"` |
| **request_method** | Cadena | El método de petición HTTP, a veces denominado verbos HTTP. | `"GET"` |
| **request_user_agent** | Cadena | El encabezado de solicitud Usuario-Agente HTTP | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | Cadena | El encabezado de la solicitud Persona que recomienda el HTTP (puede estar vacío). | `"https://chatgpt.com"` |
| **response_status** | Entero | El código de estado de respuesta HTTP. | `200` |
| **response_content_type** | Cadena | El encabezado de respuesta Content-Type de HTTP | `"text/html; charset=utf-8"` |
| **time_to_first_byte** | Entero | Tiempo transcurrido entre la creación de una conexión con el servidor y la descarga del contenido de una página web en **milisegundos**. Establezca este valor en cero si se desconoce o no está disponible. | `42` |

#### Ejemplo de líneas de registro {#example}

En el siguiente ejemplo se muestran tres líneas de registro:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Descargo de responsabilidad crítico (ortografía y tipos) {#disclaimer}

Las canalizaciones de ingesta y agregación son estrictas sobre los **nombres de campo y tipos de datos**.

- Los nombres de campo deben coincidir **exactamente** (mayúsculas y minúsculas y ortografía).
- Los tipos de datos deben ser correctos, tal como se indica a continuación:
   - **timestamp** debe ser una cadena con formato **ISO 8601**. Es posible que las marcas de tiempo similares a UNIX no funcionen.
   - **response_status** debe ser un número entero.
   - **time_to_first_byte** debe ser un número entero y utilzar milisegundos.
   - Las cadenas deben ser cadenas JSON válidas.
- Un JSON con formato incorrecto o campos que falten o son incorrectos pueden provocar que los registros se omitan o no se analicen, lo que daría lugar a la pérdida de datos en los informes.

### Ubicación de la carga y cadencia de procesamiento {#upload-location}

#### Regla de ruta {#path-rule}

Cargue los registros en la ruta de acceso de la carpeta correspondiente con el formato: **`yyyy/mm/dd/`** (con barras diagonales).

Un registro de ejemplo del 1 de febrero de 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Regla de procesamiento {#processing-rule}

- Las canalizaciones procesan los registros cargados durante un **día UTC** determinado **cerca del final de ese día UTC** (ejecución diaria).
- Los registros cargados en **carpetas de días anteriores** (relleno) se **detectan y procesan** en un plazo de 24 horas.

## Escenarios {#scenarios}

### Escenario 1: registros en Splunk/Elasticsearch: exportar y cargar en S3 {#scenario-splunk}

**Meta**: recuperar los registros de plataformas de observabilidad existentes y enviarlos a la ubicación S3.

- Extraiga los campos obligatorios de los eventos de búsqueda de Splunk/Elastic.
- Transforme cada evento en un objeto JSON siguiendo el esquema anterior (líneas JSON).
- Cargue el o los archivos resultantes en el bloque designado de S3 y la ruta de acceso **día UTC actual**: `…/byocdn-other/yyyy/mm/dd/`
- Los registros se procesarán automáticamente al final del día UTC.

### Escenario 2: función Lambda/Azure: formatear y cargar en S3 {#scenario-serverless}

**Meta**: utilizar el equipo sin servidor para recuperar o recibir registros de CDN, normalizarlos y enviarlos a la ubicación S3.

- La función recupera registros de la fuente del cliente (almacén de registros, cola, almacenamiento de los blob, etc.).
- La función asigna campos al esquema previsto y emite **Líneas JSON**.
- La función carga el resultado en: `…/byocdn-other/yyyy/mm/dd/`
- Los registros se procesarán automáticamente al final del día UTC.

## Lista de comprobación rápida {#checklist}

- **Un objeto JSON por línea** (líneas JSON)
- **Ortografía exacta del campo** según lo especificado
- Tipos de datos correctos
- **time_to_first_byte** en milisegundos (entero)
- Cargar en la carpeta UTC apropiada: **dd/mm/aaaa/** en **byocdn-other**
