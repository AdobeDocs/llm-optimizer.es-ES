---
title: Tráfico de referencia
description: Aprenda a utilizar el panel Tráfico de referencia para ver cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia.
source-git-commit: a699f8f3c50f77d07f29cd354fd1ef8e6eed8ff9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Tráfico de referencia

Tráfico de referencia muestra cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia. Rastrea y analiza fuentes de tráfico, patrones de referencia y métricas de conversión de sitios web y plataformas externas. Esto le ayudará a comprender qué fuentes, regiones y páginas generan el tráfico más atractivo. Los datos provienen de los registros de la red de distribución de contenido (CDN) o de la [telemetría operativa de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service). Ambas fuentes preservan la privacidad y no capturan datos personales de los usuarios. También hay filtros personalizables para ayudarle a refinar los datos mostrados.

![Página de referencia](/help/dashboards/assets/referral-traffic.png)

Esta página detalla lo siguiente:

* [Configuración](#setup)
* [Filtros](#filters)
* [Rendimiento general de referencia](#overall-performance)
* [Direcciones URL de referencia principales](#top-referrals)
* [Detalles del tráfico de referencia](#traffic-details)

## Configuración {#setup}

Al iniciar sesión por primera vez, el panel Tráfico de referencia puede aparecer en blanco. Para ver los datos, debe configurar un proveedor de tráfico de referencia seleccionando **Ir a la configuración**.

![Configuración de referencia](/help/dashboards/assets/referral-setup1.png)

<!--- 1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM-->

Una vez seleccionado un proveedor de tráfico de referencia, el tablero se rellenará con métricas de tráfico de referencia.

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija afectarán **todas** las secciones presentes en el panel. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas 4 semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Plataforma**: elige una fuente de tráfico específica, como Google, OpenAI o medios sociales.
* **Calidad de la página** - Filtrar el tráfico de referencia por la intención del usuario.
* **Canal Source**: filtre por el origen del canal. Las opciones incluyen: LLM, canales de referencia ganados, pagados o mixtos.
* **Tipo de dispositivo** - Analice el tráfico según el tipo de dispositivo del visitante, ya sea de escritorio, móvil o todos los dispositivos.
  **Región**: vea patrones de referencia en diferentes regiones geográficas.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel.

## Rendimiento general de referencia {#overall-performance}

El panel resalta el rendimiento general de la referencia al mostrar métricas clave, entre ellas:

* **Tráfico total de referencia**: el tráfico total de referencia de todas las fuentes.
* **Tasa de consentimiento**: porcentaje de visitantes que aceptan una solicitud de consentimiento.
* **Tasa de salida hacia otro sitio** - El porcentaje de sesiones de orígenes de referencia que no tuvieron evento de participación.

![Página de referencia](/help/dashboards/assets/referral-traffic.png)

Además de las métricas de rendimiento generales presentadas anteriormente, el panel **Regiones principales** desglosa el tráfico por ubicación geográfica. Mientras tanto, el panel **Principales fuentes de referencia** muestra las plataformas que generan la mayor cantidad de visitas. Los indicadores de tendencia de las métricas muestran cómo cambian estos valores con el paso del tiempo en comparación con el periodo anterior.

<!--## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site’s most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)-->

## Detalles de fuentes de referencia y análisis de rendimiento de URL {#traffic-details}

Las tablas Detalles de fuentes de referencia y Análisis de rendimiento de URL le ayudan a evaluar el volumen y la calidad del tráfico. Haga clic en cada pestaña a continuación para obtener más detalles:

![Detalles de tráfico de referencia](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB Detalles de orígenes de referencia]

La vista Detalles de fuentes de referencia desglosa el tráfico proveniente de diferentes plataformas, como OpenAI, Microsoft, Google y Perplexity. Muestra métricas clave como visitas, tasa de salida hacia otro sitio y tipo de canal, lo que le ayuda a comprender qué fuentes de IA y búsqueda dirigen el tráfico más comprometido a su sitio.

* **Source**: origen del tráfico de referencia.
* **Visitas**: número total de visitas para cada origen.
* **Tasa de salida hacia otro sitio** - El porcentaje de sesiones del origen de referencia que no tuvieron evento de participación.
* **Canal**: el canal del origen, ya sea ganado, pagado o ambos.

>[!TAB Análisis de rendimiento de URL]

La vista Análisis de rendimiento de URL clasifica las páginas de mayor rendimiento según el volumen de tráfico de referencia de los LLM y otras fuentes. Resalta métricas como el tráfico, la tasa de salida hacia otro sitio, la tasa de consentimiento y la intención de página, lo que le ayuda a identificar qué páginas atraen y retienen a los visitantes más comprometidos a partir de referencias impulsadas por IA. La tabla tiene un campo de búsqueda para acceder rápidamente a los temas.

>[!ENDTABS]

En ambas tablas, puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla de tráfico de referencia en los informes ejecutivos.
