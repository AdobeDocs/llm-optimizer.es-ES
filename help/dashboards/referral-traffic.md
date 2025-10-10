---
title: Tráfico de referencia
description: Aprenda a utilizar el panel Tráfico de referencia para ver cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia.
source-git-commit: e8ea9ae0d6592ea3d1e9945ec117f852112ba9d7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Tráfico de referencia

Tráfico de referencia muestra cómo llegan los visitantes al sitio desde plataformas externas, citas de IA y vínculos de referencia. Rastrea y analiza fuentes de tráfico, patrones de referencia y métricas de conversión de sitios web y plataformas externas. Esto le ayudará a comprender qué fuentes, regiones y páginas generan el tráfico más atractivo. Los datos provienen de los registros de la red de distribución de contenido (CDN) o de la telemetría operativa de AEM **(agregar vínculo)**. Ambas fuentes preservan la privacidad y no capturan datos personales de los usuarios.

También hay filtros personalizables para ayudarle a refinar los datos mostrados.

Esta página detalla lo siguiente:

* [Configuración](#setup)
* [Filtros](#filters)
* [Rendimiento general de referencia](#overall-performance)
* [Direcciones URL de referencia principales](#top-referrals)
* [Detalles del tráfico de referencia](#traffic-details)

## Configuración {#setup}

Al iniciar sesión por primera vez, el panel Tráfico de referencia puede aparecer en blanco. Para ver los datos, debe configurar un proveedor de tráfico de referencia.

![Configuración de referencia](/help/dashboards/assets/referral-setup.png)

1. Seleccione su Source (registros de CDN o telemetría operativa de AEM).
2. Introduzca un correo electrónico de contacto principal.
3. Haga clic en **Solicitar activación** para habilitar la ingesta de datos.

Una vez activado, el tablero se rellenará con métricas de tráfico de referencia.

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija afectarán **todas** las secciones presentes en el panel. Puede personalizar lo siguiente:

**Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas 4 semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
**Plataforma**: elige una fuente de tráfico específica, como Google, OpenAI o medios sociales.
**Canal**: filtra entre canales como ganados o pagados. Si prefiere una mezcla entre los dos, seleccione la opción **Todos los canales**.
**Canal Source**: filtre por el origen del canal. las opciones incluyen: visualización, búsqueda, referencia, vídeo y social. También puede usar **Todas las plataformas** para mostrar todos los orígenes de canales.
**Tipo de dispositivo** - Analice el tráfico según el tipo de dispositivo del visitante, ya sea de escritorio, móvil o todos los dispositivos.
**Región**: vea patrones de referencia en diferentes regiones geográficas.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel.

## Rendimiento general de referencia {#overall-performance}

El panel resalta el rendimiento general de la referencia al mostrar las siguientes métricas clave:

* **Tráfico total de referencia**: el tráfico total de referencia de todas las fuentes.
* **Tasa de consentimiento**: porcentaje de visitantes que aceptan una solicitud de consentimiento.
* **Tasa de salida hacia otro sitio** - El porcentaje de sesiones de orígenes de referencia que no tuvieron evento de participación.

![Página de referencia](/help/dashboards/assets/referral-traffic.png)

Además de las métricas de rendimiento generales presentadas anteriormente, el panel **Regiones principales** desglosa el tráfico por ubicación geográfica. Mientras tanto, el panel **Principales fuentes de referencia** muestra las plataformas que generan la mayor cantidad de visitas.

## Direcciones URL de referencia principales {#top-referrals}

La lista Direcciones URL de referencia principales muestra las páginas más visitadas del sitio a partir de las direcciones de referencia.

![Direcciones URL de referencia principales](/help/dashboards/assets/top-url.png)

## Detalles del tráfico de referencia {#traffic-details}

La tabla Detalles del tráfico de referencia le ayuda a evaluar el volumen y la calidad del tráfico. Proporciona un desglose detallado por fuente, incluidos los recuentos de visitas, las tasas de salida hacia otro sitio y el tipo de canal.

![Detalles de tráfico de referencia](/help/dashboards/assets/traffic-details.png)

La tabla contiene las siguientes categorías:

**Source**: origen del tráfico de referencia.
**Visitas**: número total de visitas para cada origen.
**Tasa de salida hacia otro sitio** - El porcentaje de sesiones del origen de referencia que no tuvieron evento de participación.
**Canal**: el canal del origen, ya sea ganado, pagado o ambos.

Puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla de tráfico de referencia en los informes ejecutivos.
