---
title: Inspector de URL
description: Aprenda a utilizar el Inspector de URL para analizar el rendimiento de páginas específicas del dominio en búsquedas de IA.
source-git-commit: a699f8f3c50f77d07f29cd354fd1ef8e6eed8ff9
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Inspector de URL

El Inspector de URL le ayuda a analizar el rendimiento de páginas específicas del dominio en búsquedas de IA. Combina visibilidad, tráfico auténtico y datos de referencia en el nivel de URL para ofrecerle una vista granular de las direcciones URL que se citan y de la frecuencia con la que aparecen en las respuestas.

![Inspector de URL](/help/dashboards/assets/url-insp.png)

## Filtros

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija afectarán **todas** las secciones presentes en el panel. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas 4 semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías.
* **Plataforma**: elige qué motor de IA analizar.
* **Tipo de contenido de página** - Filtre por tipo de contenido.
* **Región**: filtre los resultados por ubicación geográfica. No todas las regiones estarán disponibles en el momento del lanzamiento.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel.

## Métricas de información general

El Inspector de URL proporciona varias métricas de información general para que pueda evaluar rápidamente el rendimiento de sus páginas en las búsquedas de IA. Se proporcionan las siguientes métricas:

* **Mensajes únicos con citas propias**: el número total de mensajes únicos de IA con citas propias.
* **Total de peticiones de datos únicas** - Número total de peticiones de datos únicos de IA.
* **URL citadas únicas**: el número de URL de propiedad única que se han citado.
* **Veces totales citadas**: Veces totales que se ha citado una dirección URL propia en respuestas generadas por IA.
<!-- * **Total agentic hits** - The total number of hits from AI agents on your URLs.
* **Referral hits from LLMs** - The total number of hits directed from AI-generated answers to your URLs.-->

Los indicadores de tendencia de cada métrica de información general muestran cómo cambian estos valores con el paso del tiempo en comparación con el período anterior.

## Sus URL citadas

La vista de direcciones URL citadas enumera todas las direcciones URL de su marca que se han citado en respuestas generadas por IA, con métricas de compatibilidad. La tabla de datos también tiene un campo de búsqueda para acceder rápidamente a direcciones URL específicas. Además, puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla en los informes ejecutivos.

![URL citadas](/help/dashboards/assets/cited-urls.png)

Se proporcionan las siguientes métricas:

* **URL**: la URL analizada.
* **Veces citada**: el número de veces que la dirección URL se ha citado en respuestas generadas por IA.
* **Indicadores citados en**: el número de indicadores de IA únicos que citaron la dirección URL.
* **Categorías**: las categorías de productos o temas asociados con la dirección URL.
* **Regiones**: La región geográfica donde se citó la dirección URL.
* **Visitas de agente**: el número total de visitas de agentes de inteligencia artificial en las direcciones URL.
* **Visitas de referencia**: el número de visitas dirigidas desde respuestas generadas por IA a las direcciones URL.

## URL de tendencias que compiten por citas

Las URL de tendencias que compiten por la vista de citas destacan las URL externas que se citan actualmente en respuestas relevantes para su marca, midiendo quién gana citas en su espacio. La tabla de datos tiene un campo de búsqueda para acceder rápidamente a direcciones URL específicas. Además, puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla en los informes ejecutivos.

![URL de tendencias compitiendo por las citas](/help/dashboards/assets/trend-url.png)

Se proporcionan las siguientes métricas:

* **URL**: la URL analizada
* **Tipo de contenido**: el tipo de contenido (propio, social, ganado, competidor).
* **Veces citada**: el número de veces que la dirección URL se ha citado en respuestas generadas por IA.
* **Indicadores citados en**: el número de indicadores de IA únicos que citaron la dirección URL.
* **Categorías**: las categorías de productos o temas asociados con la dirección URL.
* **Regiones**: La región geográfica donde se citó la dirección URL.

### Ventana de detalles

Tanto para la vista de tendencias como para la vista citada, las direcciones URL tienen un botón **Detalles** cuando pasa el ratón sobre una dirección URL específica. Al hacer clic en el botón, se muestra una ventana independiente con detalles adicionales. La ventana de detalles muestra la frecuencia con la que se cita la dirección URL, la opinión de las respuestas de IA donde se menciona, los temas y las indicaciones en los que aparece y las tendencias del tráfico auténtico y de referencia a lo largo del tiempo (para las direcciones URL propias).

![Ventana de detalles](/help/dashboards/assets/details-url.png)
