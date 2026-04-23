---
title: Presencia de marca
description: Aprenda a utilizar el panel de control Presencia de marca para comprender cómo se percibe su marca en el nivel de respuestas generadas por IA.
feature: Brand Presence
source-git-commit: be88e6a5fbabbc9c1ceb75b49b883cde92ab98b2
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 96%

---


# Presencia de marca {#brand-presence}

El panel de control Presencia de marca proporciona una descripción detallada sobre cómo se percibe su marca en el nivel de respuestas generadas por IA. Muestra dónde, con qué frecuencia y en qué contexto se menciona su marca. Puede utilizar el panel de control para medir la visibilidad, hacer un seguimiento de las citas y explorar las tendencias de opinión. El panel de control se divide en varias secciones, cada una de las cuales proporciona diferentes perspectivas. También hay filtros personalizables para perfeccionar los datos mostrados.

![descripción general de la Presencia de marca](/help/dashboards/assets/brand-main.png)

Esta página detalla lo siguiente:

* [Filtros](#filters)
* [Métricas de resumen](##key-metrics)
* [Comparativa de competidores](##others-comparison)
* [Tendencia de opinión](#sentiment-trend)
* [Información de datos](#data-insights)

Si está en la experiencia de Brand Centric, vaya a **Presencia de marca**. En la lista desplegable de marca, selecciona la marca que desees analizar o elige **Todas las marcas** para revisar la visibilidad de tu conjunto de marcas completo.

![Presencia de marca con selector de marca (experiencia centrada en la marca)](/help/assets/brand-centric-experience/brand-presence-brand-centric.png)

## Filtros {#filters}

En la parte superior de la página, puede aplicar filtros para restringir la vista. Los filtros que elija tendrán un impacto en **todas** las secciones presentes en el panel de control. Puede personalizar lo siguiente:

* **Intervalo de fecha**: seleccione el lapso de tiempo para los datos mostrados. Por ejemplo, las últimas cuatro semanas. También tiene la opción de personalizar el período de tiempo seleccionando la opción **Semanas personalizadas**.
* **Categoría**: filtre los resultados mostrados por categorías predefinidas o por categorías personalizadas.
* **Tema**: filtre por tema para analizar los temas de contenido y las áreas temáticas en las que su marca aparece en las respuestas de IA.
* **Plataforma**: elija qué motor de IA desea analizar. LLM Optimizer es compatible actualmente con ChatGPT, Google AI Overviews, Modo IA de Google, Microsoft Copilot, Google Gemini y Perplexity.
* **Origen de indicaciones**: elija el origen de las indicaciones. El origen puede ser introducido por el usuario o generado por IA.
* **Indicación de identidad de la marca**: filtre los resultados mediante indicaciones con o sin marca.
* **Región**: filtre los resultados por ubicación geográfica. No todas las regiones estarán disponibles en el momento del lanzamiento.

Después de seleccionar el filtro deseado, haga clic en **Aplicar filtros** para aplicar la selección al panel de control.

## Métricas de resumen {#overview-metrics}

El panel de control destaca tres métricas muy importantes en la parte superior de la página: puntuación de visibilidad, menciones y citas. Cuanto menor sea el recuento de estas métricas, peor se percibirá su marca y deberá actuar para mejorar su presencia de marca. A continuación se presenta una breve descripción de cada métrica y lo que representa.

![Métricas generales](/help/dashboards/assets/overview-metrics.png)

### Puntuación de visibilidad {#visibility-score}

La puntuación de visibilidad está compuesta por factores como: menciones, citas, opinión y clasificación. Cada factor tiene un cierto “peso” asociado que se suma a la puntuación final.

### Menciones de la marca {#mentions}

Esta métrica representa el número total de veces que su marca o sus categorías se mencionaron en las preguntas de IA muestreadas. Por ejemplo, si tiene la marca “”Café B”, con las categorías “Máquinas” y “Accesorios”, esta métrica cuenta el número total de veces que aparecen en las respuestas de IA muestreadas.

### Citas {#citations}

Esta métrica representa el número de veces que se hizo referencia al sitio como origen.

Los indicadores de tendencia de cada métrica clave muestran cómo cambian estos valores con el paso del tiempo en comparación con el periodo anterior.

## Comparativa de competidores {#others-comparison}

En la sección de Comparativa de competidores puede seleccionar hasta cinco marcas más y comparar sus menciones y citas con su marca. De este modo, puede ver y comparar su rendimiento en relación con otras marcas.

![Comparativa de competidores](/help/dashboards/assets/other-comparison.png)

Las otras marcas se seleccionan en la lista desplegable y los gráficos se actualizan al hacer clic en **Aplicar filtros**. Los gráficos muestran menciones de la marca semanales y citas semanales de marcas en paralelo. También puede situar el ratón sobre el gráfico para ver la evolución de los datos a lo largo del lapso de tiempo semanal.

## Análisis de tendencias de opinión {#sentiment-trend}

En la sección análisis de tendencias de opinión puede realizar un seguimiento de cómo se percibe su marca en las respuestas de IA muestreadas. La métrica de tendencia de opinión puede ser positiva, neutra o negativa. Por ejemplo, puede ser positivo si las respuestas resaltan la calidad del producto o negativo si mencionan un servicio deficiente. El gráfico de tendencias muestra los cambios en la percepción de marca de una semana a otra. Esta sección se rellena solo después de mencionar su marca.

![Tendencia de opinión](/help/dashboards/assets/sentiment-trend.png)

## Data Insights y cuota de voz {#data-insights}

Para redondear el panel de control, tenemos dos tablas importantes: data insights y cuota de voz. La información presentada en estas tablas le ayudará a identificar dónde es sólida su marca y dónde se necesita optimización.

Al utilizar la tabla de **data insights**, puede explorar temas y preguntas del usuario para evaluar y optimizar el impacto del contenido. Los resultados se detallan por temas e indicaciones. Mientras tanto, la tabla **cuota de voz** compara la voz de su marca con otras marcas en todos los temas y le ayuda a identificar lagunas y a priorizar temas futuros.

![Data Insights](/help/dashboards/assets/data-insights.png)

Ambas tablas tienen un campo de búsqueda para acceder rápidamente a los temas y puede personalizar qué métricas se muestran haciendo clic en el botón **Configurar columnas**. También puede usar la opción **Exportar** para descargar la tabla .CSV y compartir la información con tu equipo o incluir las tablas en informes ejecutivos.

Haga clic en las pestañas a continuación para obtener detalles sobre cada tabla y las métricas asociadas.

>[!BEGINTABS]

>[!TAB Data Insights]

La tabla de data insights le ayuda a explorar los temas y las indicaciones de los usuarios para evaluar y optimizar el impacto de los contenidos. Muestra las siguientes métricas:

* **Tema**: la categoría del tema representa palabras clave de SEO y preguntas de los usuarios relacionadas con su marca. Puede hacer clic para expandir cada tema y ver indicaciones individuales analizadas para determinar la presencia de marca. Cada tema tiene el botón **Detalles** al pasar el ratón sobre él. Al hacer clic en el botón, se muestra una ventana separada con más detalles.
* **Región**: muestra la región de las indicaciones.
* **Popularidad**: la categoría de popularidad representa el volumen de búsqueda de este tema en relación con todos los demás temas en el análisis. El valor puede ser Alto, Medio o Bajo.
* **Puntuación de visibilidad**: la puntuación de visibilidad para ese tema. Refleja factores ponderados como menciones, citas, opinión y clasificación.
* **Menciones**: número de veces que se mencionó su marca en las respuestas de IA para este tema o esta combinación de tema/indicación.
* **Opinión**: la percepción de la marca en las respuestas de IA en relación con cada tema, calculada como un promedio de todas las semanas. Solo se rellena cuando realmente se menciona su marca.
* **Posición**: la prominencia relativa de su marca en las respuestas de IA, calculada como un promedio de todas las semanas.
* **Todas las citas**: número de fuentes únicas citadas en las respuestas de IA para este tema o esta combinación de tema/indicación (incluye citas propias).
* **Citas propias**: número de veces que se citó su marca en las respuestas de IA para esta palabra clave o esta combinación de palabra clave y pregunta.
  <!--* **Executions**-->

También puede ver detalles adicionales de cada tema haciendo clic en el ícono **Detalles** al final de cada fila.

>[!TAB Cuota de voz]

La tabla Cuota de voz proporciona una visión comparativa de cómo se desempeña su marca en temas clave en las respuestas de IA generativa. Le ayuda a identificar brechas de visibilidad, realizar un seguimiento del desempeño competitivo y priorizar áreas de optimización. Muestra las siguientes métricas:

* **Tema**: el tema analizado.
* **Popularidad**: volumen de búsqueda para este tema en relación con todos los demás temas del análisis.
* **Menciones**: número de veces que se mencionó su marca en las respuestas de IA para este tema o esta combinación de tema/indicación.
* **Clasificación**: la clasificación de la cuota de voz de su marca en relación con todas las marcas competidoras identificadas.
* **Cuota de voz**: el porcentaje del total de menciones que su marca tiene en las respuestas generadas por IA.
* **Cinco marcas competidoras principales**: las cinco marcas principales mencionadas con más frecuencia para los mismos temas. Las marcas se organizan por su cuota de voz (de mayor a menor).

>[!ENDTABS]

### Uso de la tabla de Data Insights {#using-data-insights}

La tabla de Data Insights le ayuda a pasar de las métricas a las acciones desglosando el rendimiento a nivel de tema e indicación.

Principales formas de utilizar la tabla:

* Priorice los temas de alta popularidad con baja visibilidad: concéntrese en la optimización donde la demanda del público es fuerte, pero la presencia de su marca es débil.
* Seguimiento de turnos de opinión: identifique los temas en los que las menciones sean tendencias negativas o neutras y coordine la respuesta.
* Comparar citas con citas propias: identifique las indicaciones en las que se menciona su marca, pero se cita contenido de otra, lo que indica una brecha de contenido.
* Evaluar el rango de posiciones: monitorice si su marca aparece al principio de las respuestas de IA (posiciones 1-3) o más abajo (6-10).
