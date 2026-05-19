---
title: Tráfico agéntico
description: Aprenda a utilizar el panel de control Tráfico agéntico para ver cómo los agentes de IA interactúan con el sitio.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:33:15.711Z'
TQID: 'https://experienceleague.adobe.com/3dWNUxcquDVip4Gg1WMYfwv8MUSbZYWqJYnkQ3aZkmc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1407
ht-degree: 100%

---


# Tráfico agéntico {#agentic-traffic}

El panel de control Tráfico agéntico muestra cómo los agentes de IA (rastreadores y bots de chat) interactúan con el sitio. Con esta vista puede realizar un seguimiento de la cantidad total de solicitudes y de las métricas generales relacionadas con el rendimiento. También puede ver la distribución del tráfico entre mercados, categorías, páginas y agentes. Los datos que este panel de control utiliza proceden de los registros de CDN, por lo que debe configurar **el reenvío de registros de CDN** para poder mostrar las métricas. También hay filtros personalizables para perfeccionar los datos mostrados.

![Distribución del tráfico](/help/dashboards/assets/ag-main.png)

Esta página detalla lo siguiente:

* [Filtros](#filters)
* [Configuración de CDN](#cdn-setup)
* [Distribución del tráfico](#traffic-distribution)
* [Tendencias del tráfico agéntico](#agentic-trends)
* [Mayores y menores variaciones](#top-bottom-movers)
* [Análisis de agente de usuario y de rendimiento de URL](#user-url-performance)

Si se encuentra en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), vaya a **Tráfico agéntico** y seleccione el sitio para el que desea ver las perspectivas del tráfico agéntico.

![Tráfico agéntico: selector del sitio (experiencia centrada en la marca)](/help/assets/brand-centric-experience/agentic-traffic-dashboard.png)

## Reenvío de registros de CDN {#cdn-setup}

Sin **reenvío de registros de CDN**, el panel de control Tráfico agéntico está en blanco. Para ver interacciones reales, debe configurar **Reenvío de registros de CDN**.

### Configuración del cliente (navegación clásica)

Al iniciar sesión por primera vez, verá un mensaje tal como se muestra en la siguiente imagen.

![Configuración de CDN](/help/dashboards/assets/ag-log-forward1.png)

Seleccione **Ir a configuración** y navegará automáticamente a la pestaña **Configuración de CDN** del [panel de control Configuración del cliente](/help/dashboards/customer-configuration.md).

![Incorporación de configuración de CDN](/help/dashboards/assets/ag-log-forward2.png)

En esta pestaña, seleccione **Incorporar CDN**. Y aparece la ventana del proveedor de CDN.

<!-- [CDN Provider](/help/dashboards/assets/ag-log-forward3.png)-->
En la ventana **Incorporar proveedor de CDN**:

1. Seleccione su proveedor de CDN (por ejemplo, Akamai, Fastly administrado por Adobe, Fastly, AWS Cloudfront, CDN de Azure, Cloudflare u otro).
2. Haga clic en **Incorporar** para habilitar el reenvío de registros.

Si selecciona **Otro**, tendrá que ponerse en contacto con llmo-now@adobe.com para obtener ayuda.

>[!NOTE]
>Para obtener más información sobre el reenvío de registros al utilizar una CDN administrada por el cliente (BYOCDN), consulte [Información general sobre el reenvío de registros BYOCDN](/help/overview/log-forwarding/log-forwarding-overview.md)

Una vez activados, los registros se incorporan y el panel de control se rellena con métricas como interacciones totales del agente, tasa de éxito, visitas por mercado, análisis de agente de usuario y rendimiento a nivel de URL.

### Experiencia centrada en la marca

Si se encuentra en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), puede añadir la información de reenvío de registros de CDN accediendo a **Administración de marcas** y haciendo clic en la etiqueta **CDN**.

![Administración de marcas: reenvío de registros de CDN](/help/assets/brand-centric-experience/brands-management-cdn.png)

LLM Optimizer procesa un subconjunto de campos de los registros de CDN. Aunque los nombres de los campos de registro sin procesar varían según el proveedor de CDN, se normalizan y presentan de la siguiente manera:

* URL (parámetros de ruta y consulta)
* Agente de usuario
* Código de estado
* Encabezado de referente
* Encabezado de host
* Tiempo hasta el primer byte (TTFB)
* Método de solicitud
* Marca de tiempo
* Tipo de contenido

Estos campos normalizados se exponen a través de la vista agéntica. En el panel de control [Tráfico de referencia](/help/dashboards/referral-traffic.md), los registros de CDN se utilizan para mostrar las métricas de visitas a la página. No se procesa ni almacena información de identificación personal (PII) en ninguna fase de la ingesta de registros de CDN ni en la posterior gestión de datos.

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija tendrán un impacto en **todas** las secciones presentes en el panel de control. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas cuatro semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías predefinidas o personalizadas.
* **Plataforma**: elija qué motor de IA desea analizar.
* **Tipo de agente**: filtre por el tipo de agente de IA que interactuó con el sitio. Puede filtrar entre rastreadores, bots de chat o todos los agentes.
* **Tasa de éxito**: filtre por la calidad de la interacción (alta, media o baja). Esta métrica representa el porcentaje de solicitudes HTTP correctas, incluidas tanto las respuestas correctas directas (códigos de estado 2xx) como las redirecciones (códigos de estado 3xx).
* **Tipo de contenido**: consulte la interacción agéntica para diferentes tipos de contenido, como HTML, PDF, etc.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel de control.

## Distribución del tráfico {#traffic-distribution}

La vista Distribución del tráfico muestra cómo se distribuye el tráfico del agente entre mercados, categorías y tipos de página. Como tal, esta vista le ayuda a determinar a qué regiones geográficas, áreas de producto o formatos de contenido acceden con mayor frecuencia los agentes de IA al interactuar con el sitio.

![Distribución del tráfico](/help/dashboards/assets/ag-main.png)

En la parte superior de la página, hay tres métricas clave que debe tener en cuenta:

* **Interacciones activas**: esta métrica representa el número total de solicitudes realizadas por los agentes de IA al sitio web. Esto incluye todo el tráfico de motores de búsqueda, bots de chat y otro tráfico que no sea humano.
* **Tasa de éxito**: esta métrica representa el porcentaje de solicitudes HTTP correctas, incluidas las respuestas correctas directas y los redireccionamientos.
* **Promedio de TTFB**: Time To First Byte (TTFB) mide el tiempo que tarda el primer byte de datos en recibirse desde el servidor. El valor promedio se pondera en función del número de solicitudes que devuelven cada código y excluye las solicitudes que resultaron en respuestas 5xx. Los valores más bajos indican tiempos de respuesta del servidor más rápidos.

Los indicadores de tendencia de cada métrica clave muestran cómo cambian estos valores con el paso del tiempo en comparación con el periodo anterior.

## Tendencias del tráfico agéntico {#agentic-trends}

Utilice el gráfico Tendencias de tráfico agéntico para realizar un seguimiento de los totales semanales de visitas individuales correctas, erróneas y generales. Como tal, puede monitorizar los cambios en la actividad y el rendimiento del agente a lo largo del tiempo. También puede situar el ratón sobre el gráfico para ver la evolución de los datos a lo largo del lapso de tiempo semanal.

![Tendencias del tráfico agéntico](/help/dashboards/assets/ag-trends.png)

## Mayores y menores variaciones {#top-bottom-movers}

La vista Mayores subidas y Mayores bajadas resalta las direcciones URL con los mayores cambios de una semana a otra en el tráfico agéntico: visitas o accesos de sistemas de IA que acceden a su contenido. **Mayores subidas** muestra las páginas que ganan visibilidad o participación, mientras que **Mayores bajadas** muestra las direcciones URL con las bajadas más pronunciadas. Esto le ayuda a identificar rápidamente qué contenido tiende al alza, cuál puede necesitar atención y dónde están cambiando los patrones de detección basados en la IA.

![Mayores y menores variaciones](/help/dashboards/assets/movers.png)

## Análisis de agente de usuario y de rendimiento de URL {#user-url-performance}

Las vistas de análisis de agente de usuario y de rendimiento de URL proporcionan más desgloses de datos sobre cómo los rastreadores y bots de chat interactúan con el sitio. Haga clic en las pestañas siguientes para obtener descripciones detalladas.

![Análisis de agente de usuario y de rendimiento de URL](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB Análisis de agente de usuario]

La tabla Análisis de agente de usuario proporciona un desglose del tráfico por tipo de página y tipo de agente (por ejemplo, rastreadores frente a bots de chat). De este modo, es fácil comprender qué agentes de IA rastrean qué partes del sitio. Contiene las siguientes categorías:

* **Tipo de página**: el tipo de página.
* **Tipo de agente**: el agente de IA que rastrea la página, ya sea un rastreador o un bot de chat.
* **Visitas**: el número total de solicitudes realizadas por agentes de IA para ese tipo de página específico.

Puede personalizar qué métricas se muestran haciendo clic en el botón **Configurar columnas**.

>[!TAB Análisis de rendimiento de URL]

La tabla Análisis de rendimiento de URL muestra una vista detallada de las direcciones URL individuales. Esto incluye visitas, agentes únicos, agentes principales, tasas de éxito y categorías. De este modo, puede identificar páginas de alto valor, detectar lagunas de rastreo y optimizar el contenido para los motores de IA. Las direcciones URL se clasifican por volumen de tráfico. La tabla contiene las siguientes categorías:

* **URL**: la URL examinada.
* **Visitas totales**: número total de solicitudes realizadas por agentes de IA a esta dirección URL.
* **Agentes únicos**: número de agentes de IA diferentes que accedieron a esta dirección URL.
* **Agente principal**: tipo del agente de IA que generó la mayor cantidad de tráfico a esta dirección URL.
* **Tipo de agente principal**: tipo del agente de IA que generó la mayor cantidad de tráfico a esta dirección URL.
* **Tasa de éxito**: porcentaje de solicitudes HTTP correctas, incluidas las respuestas correctas directas y las redirecciones.
* **Categoría**: categoría que se asemeja más al contenido de la página.
* **Promedio de TTFB (ms)**: Time To First Byte (TTFB) mide el tiempo que tarda el primer byte de datos en recibirse desde el servidor (milisegundos). El valor promedio se pondera en función del número de solicitudes que devuelven cada código y excluye las solicitudes que resultaron en respuestas 5xx. Los valores más bajos indican tiempos de respuesta del servidor más rápidos.
* **Códigos de respuesta**: los códigos de estado HTTP observados para la dirección URL.

La tabla de rendimiento de URL tiene un campo de búsqueda de acceso rápido a las direcciones URL y puede personalizar las métricas que se muestran haciendo clic en el botón **Configurar columnas**. También puede ver detalles adicionales para cada URL haciendo clic en el icono **Detalles** al final de cada fila.

![Detalles de URL](/help/dashboards/assets/details.png)

La vista Detalles de la URL proporciona una comprensión integral del rendimiento de una página, que muestra con qué frecuencia se cita, la opinión de las respuestas de IA donde se menciona, los temas y las indicaciones en los que aparece y las tendencias en los contenidos y el tráfico de referencia a lo largo del tiempo.

>[!ENDTABS]

En ambas tablas, puede utilizar la opción **Exportar** para descargar la tabla `.csv` y compartir las perspectivas con su equipo o incluir las tablas en los informes ejecutivos.
