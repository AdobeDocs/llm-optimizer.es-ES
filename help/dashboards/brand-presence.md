---
title: Presencia de marca
description: Aprenda a utilizar el panel Presencia de la marca para comprender cómo se percibe su marca en el nivel de respuestas generadas por IA.
source-git-commit: a37c4e7d2e26f16dc10dc7bc39ba58ba1df77cd5
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---


# Presencia de marca {#brand-presence}

El panel Presencia de la marca proporciona una descripción detallada sobre cómo se percibe su marca en el nivel de respuestas generadas por IA. Muestra dónde, con qué frecuencia y en qué contexto se menciona su marca. Puede utilizar el tablero para medir la visibilidad, rastrear las citas y explorar las tendencias de opinión. El tablero se divide en varias secciones, cada una de las cuales proporciona diferentes perspectivas. También hay filtros personalizables para ayudarle a refinar los datos mostrados.

![Presencia de marca](/help/dashboards/assets/brand-main.png)

Esta página detalla lo siguiente:

* [Filtros](#filters)
* [Métricas de información general](##key-metrics)
* [Comparación de otros](##others-comparison)
* [Tendencia de opinión](#sentiment-trend)
* [Data Insights](#data-insights)

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija afectarán **todas** las secciones presentes en el panel. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas 4 semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías predefinidas o por categorías personalizadas.
* **Plataforma**: elige qué motor de IA analizar.
* **Origen de mensajes** - Elija el origen de los mensajes. El origen puede ser introducido por el usuario o generado por IA.
* **Promoción de marca en el mensaje**: filtre los resultados mediante mensajes con marca o sin marca.
* **Región**: filtre los resultados por ubicación geográfica. No todas las regiones estarán disponibles en el momento del lanzamiento.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel.

## Métricas de información general {#overview-metrics}

El panel destaca tres métricas muy importantes en la parte superior de la página: puntuación de visibilidad, menciones y citas. Cuanto menor sea el recuento de estas métricas, peor se percibirá su marca y deberá actuar para mejorar su presencia en la marca. A continuación se presenta una breve descripción de cada métrica y lo que representa.

![Métricas de información general](/help/dashboards/assets/overview-metrics.png)

### Puntuación de visibilidad {#visibility-score}

La puntuación de visibilidad está compuesta por factores como: menciones, citas, opiniones y rango. Cada factor tiene un cierto &quot;peso&quot; adjunto que se suma a la puntuación final.

### Menciones {#mentions}

Esta métrica representa el número total de veces que su marca o sus categorías se mencionaron en las preguntas de IA muestreadas. Por ejemplo, tiene la marca &quot;Café B&quot;, con las categorías &quot;Máquinas&quot; y &quot;Accesorios&quot; y esta métrica cuenta el número total de veces que aparecen en las respuestas de IA muestreadas.

### Citas {#citations}

Esta métrica representa el número de veces que se hizo referencia al sitio como origen.

Los indicadores de tendencia de cada métrica clave muestran cómo cambian estos valores con el paso del tiempo en comparación con el periodo anterior.

## Comparación de otros {#others-comparison}

En la sección de comparación de otros puedes seleccionar hasta cinco marcas más y comparar sus menciones y citas con tu marca. De este modo, puede ver y comparar su rendimiento en relación con otras marcas.

![Comparación de otros](/help/dashboards/assets/other-comparison.png)

Las otras marcas se seleccionan en la lista desplegable y los gráficos se actualizan al hacer clic en **Aplicar filtros**. Los gráficos muestran las menciones semanales y las citas semanales en paralelo. También puede situar el ratón sobre el gráfico para ver la evolución de los datos a lo largo del lapso de tiempo semanal.

## Análisis de tendencias de opinión {#sentiment-trend}

En la sección de análisis de tendencias de opinión puede realizar un seguimiento de cómo se percibe su marca en las respuestas de IA muestreadas. La métrica de tendencia de opinión puede ser positiva, neutra o negativa. Por ejemplo, puede ser positivo si las respuestas resaltan la calidad del producto o negativo si mencionan un servicio deficiente. El gráfico de tendencias muestra los cambios en la percepción de la marca de una semana a otra. La sección solo se rellena después de mencionar su marca.

![Tendencia de opinión](/help/dashboards/assets/sentiment-trend.png)

## Perspectivas de datos y uso compartido de la voz {#data-insights}

Para redondear el tablero, tenemos dos tablas importantes: perspectivas de datos y cuota de voz. La información presentada en estas tablas le ayudará a identificar dónde es sólida su marca y dónde se necesita optimización.

Con la tabla **data insights** puede explorar temas y preguntas de usuarios para evaluar y optimizar el impacto del contenido. Los resultados se detallan por temas y peticiones de datos. Mientras tanto, la tabla **uso compartido de la voz** compara la voz de tu marca con otras marcas en todos los temas y te ayuda a identificar brechas y a priorizar temas futuros.

![Perspectivas de datos](/help/dashboards/assets/data-insights.png)

Ambas tablas tienen un campo de búsqueda para acceder rápidamente a los temas. Además, puede usar la opción **Exportar** para descargar el archivo .csv de tabla y compartir las perspectivas con su equipo o incluir la tabla en los informes ejecutivos.

Haga clic en las pestañas siguientes para obtener detalles sobre cada tabla y las métricas asociadas.

>[!BEGINTABS]

>[!TAB Perspectivas de datos]

La tabla de perspectivas de datos le ayuda a explorar temas y mensajes del usuario para evaluar y optimizar el impacto del contenido. Muestra las siguientes métricas:

* **Tema**: la categoría del tema representa palabras clave de SEO y preguntas del usuario relacionadas con su marca. Puede hacer clic en para expandir cada tema y ver las solicitudes individuales analizadas para comprobar la presencia de la marca. Cada tema tiene un botón **Detalles** cuando pasa el ratón sobre él. Al hacer clic en el botón, se muestra una ventana independiente con más detalles.
* **Región** - muestra la región de las indicaciones.
* **Popularidad**: la categoría de popularidad representa el volumen de búsqueda de este tema en relación con todos los demás temas del análisis. El valor puede ser Alto, Medium o Bajo.
* **Puntuación de visibilidad**: la puntuación de visibilidad de ese tema. Refleja factores ponderados como menciones, citas, opiniones y rango.
* **Menciones**: la cantidad de veces que se mencionó su marca en las respuestas de IA para este tema o esta combinación de tema/solicitud.
* **Opinión**: la percepción de la marca en las respuestas de IA en relación con cada tema calculada como un promedio en todas las semanas. Solo se rellena cuando se menciona realmente su marca.
* **Posición**: la importancia relativa de su marca en las respuestas de IA, calculada como un promedio en todas las semanas.
* **Todas las citas** - El número de fuentes únicas citadas en las respuestas de IA para este tema o esta combinación de tema/petición de datos (incluye citas propias).
* **Citas en propiedad**: el número de veces que se citó su marca en las respuestas de IA para esta palabra clave o esta combinación de palabra clave y pregunta.

>[!TAB Uso compartido de voz]

La tabla Uso compartido de voz proporciona una vista comparativa del rendimiento de su marca en varios temas clave de las respuestas de IA generativas. Le ayuda a identificar lagunas de visibilidad, realizar un seguimiento del rendimiento competitivo y priorizar áreas para la optimización. Muestra las siguientes métricas:

* **Tema**: el tema analizado.
* **Popularidad**: el volumen de búsqueda del tema en relación con todos los demás temas del análisis.
* **Menciones**: número de veces que se mencionó su marca en las respuestas de IA para el tema o la combinación de tema/solicitud.
* **Clasificación**: la clasificación de la Cuota de voz de su marca en relación con todas las demás marcas identificadas.
* **Cuota de voz**: el porcentaje del total de menciones que tu marca contiene en las respuestas generadas por IA.
* **Principales 5 otras**: las cinco marcas más mencionadas para los mismos temas. Las marcas están organizadas por su Cuota de voz (de mayor a menor).

>[!ENDTABS]

### Uso de la tabla de Data Insights {#using-data-insights}

La tabla de perspectivas de datos le ayuda a pasar de métricas a acciones al desglosar el rendimiento en el nivel de tema y de solicitud.

Formas clave de utilizar la tabla:

* Priorice los temas de alta popularidad con baja visibilidad: optimización del enfoque en los que la demanda de la audiencia es fuerte, pero la presencia de la marca es débil.
* Rastree los cambios de opinión: localice los temas en los que las menciones son de tendencia negativa o neutra y coordine la respuesta.
* Comparar citas con citas propias: identifique indicaciones en las que se mencione su marca, pero en las que se cite el contenido de otra marca, lo que indica una brecha de contenido.
* Evaluar el rango de posiciones: monitorice si su marca aparece al principio de las respuestas de IA (posiciones 1-3) o más abajo (6-10).
