---
title: Tráfico de referencia
description: Aprenda a utilizar el panel de control Tráfico de referencia para ver cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia.
feature: Referral Traffic
source-git-commit: ea4cf80dc5f789f7938c800354bc8d8d3246704c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 79%

---


# Tráfico de referencia

El tráfico de referencia muestra cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia. Rastrea y analiza las fuentes de tráfico, los patrones de referencia y las métricas de conversión de sitios web y plataformas externas. Esto le ayudará a comprender qué fuentes, regiones y páginas generan el tráfico más interesado. <!--Data is sourced from the CDN logs, a privacy-preserving source that does not capture personal user data.--> También hay filtros personalizables para perfeccionar los datos mostrados.

>[!NOTE]
>De manera predeterminada, este tablero genera perspectivas de tráfico a partir de **registros de CDN**. Si su organización está en una oferta de pago, puede conectar **Adobe Analytics** para agregar datos que midan el descubrimiento impulsado por IA y la participación en el sitio. Estos datos están disponibles en la ficha **Impacto en la empresa**. Sin la integración con Adobe Analytics, la pestaña no se rellena. Consulte [Integración de Adobe Analytics](/help/dashboards/adobe-analytics-integration.md) para obtener más información.

![Página de referencia](/help/dashboards/assets/referral-traffic.png)

Esta página detalla lo siguiente:

* [Configuración](#setup)
* [Filtros](#filters)
* [Rendimiento general de referencia](#overall-performance)
* [Direcciones URL de referencia principales](#top-referrals)
* [Detalles del tráfico de referencia](#traffic-details)

Si está en la experiencia centrada en la marca, vaya al **Tráfico de referencia** y seleccione el sitio para el cual desea ver las perspectivas del Tráfico de referencia LLM.

![Tráfico de referencia — selector de sitio (experiencia centrada en la marca)](/help/assets/brand-centric-experience/referral-traffic-dashboard.png)

## Configuración {#setup}

Al iniciar sesión por primera vez, el panel de control tráfico de referencia puede aparecer en blanco. Para ver los datos, debe configurar el reenvío de registros de CDN.

Para los clientes que se encuentran en la experiencia centrada en la marca, así es como puede agregar información de reenvío de registros de CDN. Vaya a **Brands Management** y haga clic en la etiqueta **CDN**. Consulte también [Tráfico de agente — Configuración de CDN](/help/dashboards/agentic-traffic.md#cdn-setup).

**Configuración del cliente (experiencia clásica):** Configure el [reenvío de registros de CDN](/help/dashboards/customer-configuration.md#cdn-configuration) seleccionando **Ir a la configuración**.

![Configuración de la referencia](/help/dashboards/assets/referral-setup1.png)

<!--
1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM
-->

Una vez activado, el panel de control se rellena con las métricas del tráfico de referencia.

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija tendrán un impacto en **todas** las secciones presentes en el panel de control. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas cuatro semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Plataforma**: elija una fuente de tráfico específica, como Google, OpenAI o redes sociales.
* **Intención de la página**: filtre el tráfico de referencia por la intención del usuario.
* **Origen del canal**: filtre por el origen del canal. Las opciones incluyen: LLM, canales de referencia ganados, pagados o mixtos.
* **Tipo de dispositivo**: analice el tráfico según el tipo de dispositivo del visitante, ya sea de escritorio, móvil o todos los dispositivos.
* **Región**: vea patrones de referencia en diferentes regiones geográficas.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel de control.

## Rendimiento general de referencia {#overall-performance}

El panel de control resalta el rendimiento general de la referencia al mostrar métricas clave, entre ellas, las siguientes:

* **Tráfico de referencia total**: el tráfico de referencia total procedente de todas las fuentes.
* **Tráfico de referencia de LLM**: el tráfico de referencia total procedente de los LLM.
* **Tasa de consentimiento**: porcentaje de visitantes que aceptan una indicación de consentimiento.
* **Porcentaje de rechazo**: el porcentaje de sesiones de fuentes de referencia que no tuvieron evento de participación.

![Página de referencia](/help/dashboards/assets/referral-traffic.png)

Además de las métricas de rendimiento general presentadas anteriormente, hay tres paneles adicionales que muestran la distribución del tráfico en diferentes mercados, fuentes de referencia y categorías de intención de página <!-- the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits. Trend indicators for the metrics show how these values are changing over time compared to the previous period.-->

<!--
## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site's most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)
-->

## Detalles de fuentes de referencia y análisis de rendimiento de URL {#traffic-details}

Las tablas Detalles de fuentes de referencia y Análisis de rendimiento de URL le ayudan a evaluar el volumen y la calidad del tráfico. Haga clic en cada pestaña a continuación para obtener más detalles:

![Detalles del tráfico de referencia](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB Detalles de fuentes de referencia]

La vista Detalles de fuentes de referencia desglosa el tráfico proveniente de diferentes plataformas, como OpenAI, Microsoft, Google y Perplexity. Muestra métricas clave como visitas, porcentaje de rechazo y tipo de canal, lo que le ayuda a comprender qué fuentes de IA y búsqueda dirigen el tráfico más implicado a su sitio.

* **Fuente**: origen del tráfico de referencia.
* **Visitas**: número total de visitas para cada fuente.
* **Porcentaje de rechazo**: el porcentaje de sesiones de la fuente de referencia que no tuvieron ningún evento de participación.
* **Canal**: el canal de la fuente, ya sea ganado, pagado o ambos.

>[!TAB Análisis de rendimiento de URL]

La vista Análisis de rendimiento de URL clasifica las páginas de mayor rendimiento según el volumen de tráfico de referencia de los LLM y otras fuentes. Resalta métricas como el tráfico, el porcentaje de rechazo, la tasa de consentimiento y las intención de la página, lo que le ayuda a identificar qué páginas atraen y retienen a los visitantes más activos a partir de referencias basadas en la IA. La tabla contiene un campo de búsqueda para acceder rápidamente a los temas.

>[!ENDTABS]

En ambas tablas, puede usar la opción **Exportar** para descargar el archivo .CSV de la tabla y compartir la información con su equipo o incluir las tablas en los informes ejecutivos. Además, en ambas tablas, puede personalizar qué métricas se muestran haciendo clic en el botón **Configurar columnas**.
