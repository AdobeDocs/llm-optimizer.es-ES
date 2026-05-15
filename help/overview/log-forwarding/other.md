---
title: 'Reenvío de registros: otro (carga manual)'
description: Obtenga información sobre cómo cargar manualmente registros de CDN al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer cuando se utiliza un proveedor de CDN no compatible.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:54:15.685Z'
TQID: 'https://experienceleague.adobe.com/YBfhS4oM0qYRkFvS3zPzzcFAeLNBucRH5QmMBUH8h4E'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 670
ht-degree: 2%

---


# Reenvío de registros: otro (carga manual) {#log-forwarding-other}

El método de aprovisionamiento **Other BYOCDN** es una opción global para los clientes que desean proporcionar registros de CDN a LLM Optimizer cuando:

- Se prefieren las **cargas manuales**; por ejemplo, los equipos operativos exportan los registros y los cargan periódicamente.
- Se utilizan **procesos automatizados específicos**: scripts únicos, exportaciones programadas y trabajos sin servidor.
- El cliente usa una **CDN que no es compatible de forma nativa** con las integraciones de reenvío de registro integradas.

Este método imita el modelo de &quot;reenvío continuo&quot;: los registros se producen y cargan en la ubicación S3 esperada y, finalmente, las canalizaciones de ingesta los procesan automáticamente.

## Paso 1: Incorporación en LLM Optimizer {#step-1}

En [LLM Optimizer](https://llmo.now/):

1. Vaya a **Configuración**.

   ![Botón Configuración](/help/overview/assets/log-forwarding/common/config-button.png)

1. Haga clic en la ficha **Configuración de CDN**.

   ![Ficha Configuración de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Haga clic en **Comenzar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Junto a **Activar perspectivas de tráfico de IA**, haga clic en **Configurar**.

   ![Configuración](/help/overview/assets/log-forwarding/common/configure.png)

1. Seleccione **Otro**.

   ![Seleccionar otro](/help/overview/assets/log-forwarding/other/other-select.png)

1. Haga clic en **Incorporar**.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Paso 2: Preparar y cargar registros {#step-2}

### Formato de registro requerido (líneas JSON) {#log-format}

Los registros deben cargarse como JSON delimitado por una nueva línea (**un objeto JSON por cada línea**). Cada línea de registro debe incluir los siguientes campos **exactamente como se escribe debajo**.

#### Esquema campo a campo {#schema}

| Campo | Tipo | Descripción | Ejemplos |
|---|---|---|---|
| **timestamp** | Cadena | La marca de tiempo de la solicitud según el formato **ISO 8601**. | `"2025-02-01T23:00:05Z"` |
| **host** | Cadena | El dominio web solicitado por el cliente. | `"www.example.com"` |
| **URL** | Cadena | Se requieren **path** y **parámetros de consulta**, mientras que el dominio debe **no** incluirse. | `"/home?utm_source=google"` |
| **método_de_solicitud** | Cadena | El método de petición HTTP, también conocido como verbos HTTP. | `"GET"` |
| **request_user_agent** | Cadena | El encabezado de solicitud del agente de usuario HTTP. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | Cadena | El encabezado de la solicitud del referente HTTP (puede estar vacío). | `"https://chatgpt.com"` |
| **estado_de_respuesta** | Entero | El código de estado de respuesta HTTP. | `200` |
| **response_content_type** | Cadena | El encabezado de respuesta HTTP Content-Type. | `"text/html; charset=utf-8"` |
| **tiempo_hasta_primer_byte** | Entero | Tiempo transcurrido entre la creación de una conexión con el servidor y la descarga del contenido de una página web en **milisegundos**. Establezca este valor en cero si no se conoce o no está disponible. | `42` |

#### Ejemplo de líneas de registro {#example}

El siguiente ejemplo muestra tres líneas de registro:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Descargo de responsabilidad crítico (ortografía y tipos) {#disclaimer}

Las canalizaciones de ingesta y agregación son estrictas en cuanto a **nombres de campo y tipos de datos**.

- Los nombres de campo deben coincidir con **exactamente** (mayúsculas y minúsculas y ortografía).
- Los tipos de datos deben ser correctos, como se indica a continuación:
   - **timestamp** debe ser una cadena con formato **ISO 8601**. Es posible que las marcas de tiempo similares a UNIX no funcionen.
   - **response_status** debe ser un número entero.
   - **time_to_first_byte** debe ser un número entero y usar milisegundos.
   - Las cadenas deben ser cadenas JSON válidas.
- El formato incorrecto de los campos JSON o los campos que faltan o son incorrectos pueden hacer que los registros se omitan o no se analicen, lo que provoca la falta de datos en los informes.

### Cargar ubicación y cadencia de procesamiento {#upload-location}

#### Regla de ruta {#path-rule}

Cargue los registros en la ruta de acceso de la carpeta correspondiente con el formato: **`yyyy/mm/dd/`** (con barras diagonales).

Un registro de ejemplo del 1 de febrero de 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Regla de procesamiento {#processing-rule}

- Las canalizaciones **procesan los registros cargados durante un** día UTC **determinado cerca del final de ese día UTC** (ejecución diaria).
- Los registros cargados en **carpetas de días anteriores** (relleno) se **detectan y procesan** en un plazo de 24 horas.

## Escenarios {#scenarios}

### Escenario 1: Registros en Splunk/Elasticsearch, exportar y cargar en S3 {#scenario-splunk}

**Objetivo**: Recupere registros de plataformas de observabilidad existentes y envíelos a la ubicación S3.

- Extraiga los campos obligatorios de los eventos de búsqueda de Splunk/Elastic.
- Transforme cada evento en un objeto JSON siguiendo el esquema anterior (líneas JSON).
- Cargue los archivos resultantes en el contenedor designado de S3 y la ruta de acceso **día UTC actual**: `…/byocdn-other/yyyy/mm/dd/`
- Los registros se procesarán automáticamente al final del día UTC.

### Escenario 2: función Lambda/Azure: formatear y cargar en S3 {#scenario-serverless}

**Objetivo**: utilice el equipo sin servidor para recuperar o recibir registros de CDN, normalizarlos y enviarlos a la ubicación S3.

- La función recupera registros del origen del cliente (almacén de registros, cola, almacenamiento de blob, etc.).
- La función asigna campos al esquema esperado y emite **Líneas JSON**.
- La función carga el resultado en: `…/byocdn-other/yyyy/mm/dd/`
- Los registros se procesarán automáticamente al final del día UTC.

## Lista de comprobación rápida {#checklist}

- **Un objeto JSON por línea** (líneas JSON)
- **Escritura exacta del campo** según lo especificado
- Tipos de datos correctos
- **tiempo_hasta_el_primer_byte** en milisegundos (entero)
- Cargue en la carpeta UTC apropiada: **aaaa/mm/dd/** en **byocdn-other**
