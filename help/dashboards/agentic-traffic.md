---
title: Tráfico de agente
description: Aprenda a utilizar el tablero Tráfico agéntico para ver cómo los agentes de IA interactúan con el sitio.
source-git-commit: e8ea9ae0d6592ea3d1e9945ec117f852112ba9d7
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Tráfico de agente {#agentic-traffic}

El panel Tráfico agéntico le muestra cómo los agentes de IA (rastreadores y bots de chat) interactúan con su sitio. Con esta vista puede realizar un seguimiento de la cantidad total de solicitudes y de las métricas generales relacionadas con el rendimiento. También puede ver la distribución del tráfico entre mercados, categorías, páginas y agentes. Los datos que usa este panel proceden de los registros de CDN, por lo que debe configurar **el reenvío de registros de CDN** para poder mostrar las métricas. También hay filtros personalizables para ayudarle a refinar los datos mostrados.

Esta página detalla lo siguiente:

* [Filtros](#filters)
* [Configuración de CDN](#cdn-setup)
* [Distribución del tráfico](#traffic-distribution)
* [Tendencias del tráfico agéntico](#agentic-trends)
* [Movimientos superior e inferior](#top-bottom-movers)
* [Análisis del rendimiento del agente de usuario y la URL](#user-url-performance)

## Configuración de CDN {#cdn-setup}

En el primer inicio de sesión, el tablero Tráfico agéntico está en blanco. Para ver interacciones reales, debe configurar **reenvío de registros de CDN**. **TBD señala a la configuración de CDN en inicio rápido/incorporación?**

![Configuración de CDN](/help/dashboards/assets/ag-log-forward.png)

1. Seleccione su proveedor de CDN (por ejemplo, Akamai, Fastly administrado por Adobe, Fastly, AWS Cloudfront, CDN de Azure, Cloudflare u otro).
2. Introduzca un correo electrónico de contacto principal.
3. Haga clic en **Solicitar activación** para habilitar el reenvío de registros.

Una vez activados, los registros se incorporan y el tablero se rellena con métricas como interacciones totales del agente, tasa de éxito, visitas por mercado, análisis de agentes de usuario y rendimiento a nivel de URL.

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija afectarán **todas** las secciones presentes en el panel. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas 4 semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías predefinidas. También puede agregar categorías personalizadas a este campo (**SR**-how?).
* **Plataforma**: elige qué motor de IA analizar.
* **Tipo de agente**: filtre por el tipo de agente de IA que interactuó con el sitio. Puede filtrar entre rastreadores, bots de chat o todos los agentes.
* **Tasa de éxito** - Filtre por la calidad de la interacción (alta, media o baja). Esta métrica representa el porcentaje de solicitudes HTTP correctas, incluidas las respuestas correctas directas y las redirecciones.
* **Tipo de contenido** - Filtre por tipo de contenido, ya sea HTML o txt.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel.

## Distribución del tráfico {#traffic-distribution}

La vista Distribución del tráfico muestra cómo se distribuye el tráfico del agente entre mercados, categorías y tipos de página. Como tal, esta vista le ayuda a determinar a qué regiones geográficas, áreas de producto o formatos de contenido acceden con mayor frecuencia los agentes de IA al interactuar con el sitio.

![Distribución de tráfico](/help/dashboards/assets/ag-main.png)

En la parte superior de la página, hay tres métricas clave que debe tener en cuenta:

* **Interacciones activas**: esta métrica representa el número total de solicitudes realizadas por los agentes de IA al sitio web. Esto incluye todo el tráfico de motores de búsqueda, bots de chat y otro tráfico que no sea humano.
* **Tasa de éxito**: esta métrica representa el porcentaje de solicitudes HTTP correctas, incluidas las respuestas correctas directas y las redirecciones.
* **Promedio de TTFB** - Tiempo hasta el primer byte (TTFB) mide el tiempo que tarda el primer byte de datos en recibirse del servidor. Los valores más bajos indican tiempos de respuesta del servidor más rápidos.

Los indicadores de tendencia de cada métrica clave muestran cómo cambian estos valores con el paso del tiempo en comparación con el periodo anterior.

## Tendencias del tráfico agéntico {#agentic-trends}

Utilice el gráfico Tendencias de tráfico agente para realizar un seguimiento de los totales semanales de visitas individuales correctas, fallidas y generales. Como tal, puede monitorizar los cambios en la actividad y el rendimiento del agente a lo largo del tiempo. También puede situar el ratón sobre el gráfico para ver la evolución de los datos a lo largo del lapso de tiempo semanal.

![Tendencias de tráfico agente](/help/dashboards/assets/ag-trends.png)

## Movimientos superior e inferior {#top-bottom-movers}

Estas dos métricas ordenan las direcciones URL de la siguiente manera:

* **Principales visitantes**: Las direcciones URL con el mayor aumento en el tráfico auténtico de la semana más antigua a la más reciente.
* **Modificadores inferiores**: URL con la mayor disminución del tráfico auténtico de la semana más antigua a la más reciente.

## Análisis del rendimiento del agente de usuario y la URL {#user-url-performance}

Las vistas Agente de usuario y Análisis de rendimiento de URL proporcionan más desgloses de datos sobre cómo los rastreadores y bots de chat interactúan con el sitio. Haga clic en las pestañas a continuación para obtener descripciones detalladas.

![Análisis de rendimiento del agente de usuario y la URL](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB Análisis del agente de usuario]

La tabla Análisis de agente de usuario proporciona un desglose del tráfico por tipo de página y tipo de agente (por ejemplo, rastreadores frente a bots de chat). De este modo, es fácil comprender qué agentes de IA rastrean qué partes del sitio. Contiene las siguientes categorías:

* **Tipo de página** - El tipo de página.
* **Tipo de agente**: el agente de IA está rastreando la página, ya sea un rastreador o un bot de chat.
* **Visitas**: el número total de solicitudes realizadas por agentes de inteligencia artificial para ese tipo de página específico.

También puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir el análisis del agente con su equipo o incluirlo en los informes ejecutivos.

>[!TAB Análisis de rendimiento de URL]

La tabla Análisis de Rendimiento de URL muestra una vista detallada de las direcciones URL individuales. Esto incluye visitas, agentes únicos, agentes principales, tasas de éxito y categorías. De este modo, puede identificar páginas de alto valor, detectar huecos de rastreo y optimizar el contenido para los motores de IA. Las direcciones URL se clasifican por volumen de tráfico. La tabla contiene las siguientes categorías:

* **URL** - La URL examinada.
* **Visitas totales**: número total de solicitudes realizadas por agentes de inteligencia artificial a la dirección URL.
* **Agentes únicos**: número de agentes de IA diferentes que accedieron a la dirección URL.
* **Agente principal**: El agente de IA que generó la mayor cantidad de tráfico en la dirección URL.
* **Tipo de agente principal**: el tipo de agente de IA que generó la mayor cantidad de tráfico en esta dirección URL.
* **Tasa de éxito**: porcentaje de solicitudes HTTP correctas, incluidas las respuestas correctas directas y las redirecciones.
* **Categoría**: La categoría que más se asemeja al contenido de su página.

La tabla de rendimiento de URL tiene un campo de búsqueda para acceder rápidamente a las URL. Además, puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla en los informes ejecutivos.

>[!ENDTABS]
