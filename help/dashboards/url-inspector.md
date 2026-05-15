---
title: Inspector de URL
description: Aprenda a utilizar el Inspector de URL para analizar el rendimiento de páginas específicas de su dominio en las búsquedas por IA.
feature: URL Inspector
autotag-review: '2026-05-15T18:10:59.172Z'
TQID: 'https://experienceleague.adobe.com/n5IgVprujFrB8bImxkgzcAzK1fT6bsvnwNzSdBaV-4E'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: aedaee53-dfb4-4ab4-9d23-fa6188148769
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 718
ht-degree: 95%

---


# Inspector de URL

El inspector de URL le ayuda a analizar el rendimiento de páginas específicas de su dominio en las búsquedas por IA. Combina visibilidad, tráfico agéntico y datos de referencia a nivel de la URL para ofrecerle una vista granular de las direcciones URL que se citan y de la frecuencia con la que aparecen en las respuestas.

![Inspector de URL](/help/dashboards/assets/url-insp.png)

Si está en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), vaya a **Inspector de URL** y seleccione el sitio para el cual desea ver las perspectivas.

![Inspector de URL: selector de sitio (experiencia centrada en la marca)](/help/assets/brand-centric-experience/url-inspector-dashboard.png)

## Filtros

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija tendrán un impacto en **todas** las secciones presentes en el panel de control. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas cuatro semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías.
* **Plataforma**: elija qué motor de IA desea analizar.
* **Tipo de contenido de página**: filtre por el tipo de contenido.
* **Región**: filtre los resultados por ubicación geográfica. No todas las regiones estarán disponibles en el momento del lanzamiento.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel de control.

## Métricas de resumen

El Inspector de URL proporciona varias métricas de resumen para que pueda evaluar rápidamente el rendimiento de sus páginas en las búsquedas por IA. Se proporcionan las siguientes métricas:

* **Indicaciones únicas con citas propias**: el número total de indicaciones de IA con citas propias.
* **Total de indicaciones únicas**: el número total de indicaciones de IA únicas.
* **URL citadas únicas**: el número de URL propias únicas que se han citado.
* **Total de veces que se ha citado**: el número total de veces que se ha citado una URL propia en las respuestas generadas por IA.
* **Total de visitas agénticas**: el número total de visitas de los agentes de IA en las URL.
* **Visitas de referencia de los LLM**: el número total de visitas dirigidas desde las respuestas generadas por IA a las URL.

Los indicadores de tendencia de cada métrica de resumen muestran cómo cambian estos valores con el paso del tiempo en comparación con el período anterior.

## Sus URL citadas

La vista de URL citadas enumera todas las direcciones URL de su marca que se han citado en las respuestas generadas por IA, con las métricas de compatibilidad. Ambas tablas contienen un campo de búsqueda para acceder rápidamente a los temas y puede personalizar qué métricas se muestran haciendo clic en el botón **Configurar columnas**. Además, puede usar la opción **Exportar** para descargar el archivo .CSV de la tabla y compartir la información con su equipo o incluir la tabla en los informes ejecutivos.

![URL citadas](/help/dashboards/assets/cited-urls.png)

Se proporcionan las siguientes métricas:

* **URL**: la URL analizada.
* **Veces citado**: el número de veces que la dirección URL se ha citado en respuestas generadas por IA.
* **Indicaciones citadas en**: el número de indicaciones de IA únicas que han citado la dirección URL.
* **Categorías**: categorías de productos o temas asociados con la URL.
* **Regiones**: región geográfica en la que se citó la URL.
* **Visitas agénticas**: el número total de visitas de agentes de IA en las URL
* **Visitas de referencia**: el número de visitas dirigidas desde las respuestas generadas por IA a las direcciones URL.

## URL en tendencias que compiten por citas

Las URL en tendencia que compiten por la vista de citas destacan las URL externas que se citan actualmente en las respuestas relevantes para su marca, midiendo quién está ganando citas en su espacio. La tabla de datos contiene un campo de búsqueda para acceder rápidamente a direcciones URL específicas. Además, puede usar la opción **Exportar** para descargar el archivo .CSV de la tabla y compartir la información con su equipo o incluir la tabla en los informes ejecutivos.

![URL en tendencia que compiten por citas](/help/dashboards/assets/trend-url.png)

Se proporcionan las siguientes métricas:

* **URL**: la URL analizada
* **Tipo de contenido**: el tipo de contenido (propio, social, obtenido, otros).
* **Veces citado**: el número de veces que la dirección URL se ha citado en respuestas generadas por IA.
* **Indicaciones citadas en**: el número de indicaciones de IA únicas que han citado la dirección URL.
* **Categorías**: categorías de productos o temas asociados con la URL.
* **Regiones**: región geográfica en la que se citó la URL.

### Ventana de detalles

Tanto para la vista de tendencias como para la vista citada, las direcciones URL tienen un botón **Detalles** al final de cada fila. Al hacer clic en el botón, se muestra una ventana independiente con detalles adicionales. La ventana de detalles muestra la frecuencia con la que se cita la dirección URL, <!--the sentiment of AI responses where it is mentioned,--> los temas y las indicaciones en los que aparece, así como las tendencias en el contenido y el tráfico de referencia a lo largo del tiempo (para las direcciones URL propias).

![Ventana de detalles](/help/dashboards/assets/details-url.png)
