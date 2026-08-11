---
title: Análisis de opinión de YouTube
description: Descubra cómo LLM Optimizer analiza los vídeos y comentarios de YouTube para mostrar recomendaciones que mejoran la percepción y visibilidad de su marca en los resultados de la búsqueda por IA.
feature: Opportunities
autotag-review: '2026-07-15T18:00:20.630Z'
TQID: 'https://experienceleague.adobe.com/qWlMzK13noSQULxakuUKHlDGZ-307yJjGJ4vsru2W6M'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
subfeature_v2:
  - id: fe92ae96-fc87-4fea-96a0-adc06310d4f4
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: fc314d1d-7cb9-4a38-8dbd-8f9b6478f40d
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: ht
source-wordcount: 1255
ht-degree: 100%

---


# Análisis de opinión de YouTube

YouTube es una de las plataformas más influyentes a la hora de moldear la percepción de los consumidores y la reputación de las marcas. Cuando los sistemas de IA responden a preguntas sobre su marca, citan cada vez más los vídeos de YouTube como fuentes, lo que hace que la forma en que se habla de su marca en ese contenido sea una entrada directa en las respuestas generadas por IA.

La oportunidad de Análisis de opinión de YouTube aparece cuando los vídeos de YouTube se detectan como citas para las indicaciones del conjunto de indicaciones del panel Presencia de marca. Analiza esos videos mencionados y sus comentarios para determinar la opinión general, la cuota de voz y los temas recurrentes. A continuación, muestra las recomendaciones priorizadas para mejorar la forma en que se percibe y representa su marca en las respuestas generadas por IA.

Analiza su marca en seis dimensiones:

- **Vídeos analizados**: número de vídeos de YouTube examinados para detectar menciones y opiniones de la marca.
- **Comentarios analizados**: número de comentarios examinados en todos los vídeos analizados.
- **Menciones de marca (vídeos)**: la frecuencia con la que se menciona su marca en el contenido de vídeo.
- **Menciones de marca (comentarios)**: la frecuencia con la que se menciona su marca en los comentarios.
- **Opinión general (vídeos)**: opinión añadida sobre su marca en el contenido del vídeo.
- **Opinión general (comentarios)**: opinión agregada sobre su marca en los comentarios.

>[!NOTE]
>El análisis de opinión de YouTube está actualmente en fase Beta. Las funciones y la disponibilidad pueden cambiar a medida que la funcionalidad sigue desarrollándose.

![Panel de control Análisis de opinión de YouTube](/help/dashboards/opportunities/assets/youtube-sentiment-overview.png)

## Funcionamiento

LLM Optimizer supervisa los vídeos de YouTube citados por los sistemas de IA para buscar indicaciones en el conjunto de indicaciones del panel de control Presencia de marca. Cuando se detectan vídeos citados, analiza esos vídeos y sus comentarios en busca de menciones a la marca, opiniones, la cuota de voz y las citas de IA. Compara el rendimiento de su marca con el de la competencia del mercado y las marcas asociadas, identifica los temas recurrentes que influyen en la opinión y ofrece recomendaciones para subsanar las diferencias de percepción.

Si no se citan vídeos de YouTube para las indicaciones del conjunto de indicaciones, esta oportunidad no aparecerá en el panel de control.

Los resultados se muestran en dos pestañas: **Sugerencias** y **Rendimiento**.

## Sugerencias

Esta pestaña muestra recomendaciones para mejorar la percepción de su marca en YouTube. Las sugerencias están organizadas en tres subpestañas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**.

![Pestaña Sugerencias](/help/dashboards/opportunities/assets/youtube-sentiment-suggestions.png)

La tabla de sugerencias incluye las siguientes columnas:

- **Sugerencia**: la mejora recomendada para subsanar una diferencia de percepción.
- **Prioridad**: nivel de urgencia (crítica, alta, media, baja).
- **Elementos de acción**: abre un panel con pasos específicos para implementar la recomendación, incluidos los equipos responsables (por ejemplo, Estrategia de contenido, Marketing de influencers, Marketing de producto).
- **Evidencia**: abre una tabla de Fuentes que muestra los vídeos que respaldan la sugerencia.

Al expandir una sugerencia, aparece una sección **Análisis de IA** con los siguientes elementos:

- **Por qué esto necesita una mejora**: una explicación de la diferencia de percepción identificada, incluyendo el contexto competitivo y cómo se está manifestando el problema en los contenidos de YouTube.
- **Cómo mejorar**: directrices específicas sobre qué contenido o acciones permitirían subsanar esta carencia.
- **Resultado esperado**: el resultado esperado de la implementación de la recomendación.

La tabla **Fuentes** muestra los vídeos de YouTube que generan la sugerencia, con las siguientes columnas:

- **Vídeo**: título y vínculo al vídeo de YouTube.
- **Canal**: el canal de YouTube que publicó el video.
- **Participación**: el nivel de participación (bajo, medio, alto).
- **Menciones de marca**: número de menciones de su marca en comparación con el total de menciones en el video.
- **Cuota de voz**: la proporción de menciones de su marca en comparación con todas las marcas mencionadas.
- **Cinco marcas principales**: las marcas más mencionadas en el vídeo.
- **Opinión**: opinión general sobre su marca en el vídeo.
- **Citas de IA**: número de respuestas de IA que citaron este vídeo.

## Rendimiento

La pestaña **Rendimiento** ofrece un desglose detallado del rendimiento de su marca en los contenidos de YouTube. Se organiza en cuatro secciones.

### Panorama del mercado

Compare el rendimiento de su marca con las marcas asociadas y la competencia del mercado en función de las menciones.

![Panorama del mercado](/help/dashboards/opportunities/assets/youtube-sentiment-market-landscape.png)

Incluye lo siguiente:

- **Menciones de marca en vídeos**: su cuota de voz frente a las marcas asociadas y la competencia del mercado.
- **Menciones de marca en comentarios**: la misma comparación aplicada al contenido de los comentarios.
- **Seguimiento del mercado**: un gráfico filtrable donde puede seleccionar hasta cinco marcas competidoras para comparar la cuota de voz en vídeos y comentarios.

### Análisis de opinión

Realiza un seguimiento de la percepción de la marca en todo el contenido analizado con un gráfico **Distribución de opiniones** que muestra el desglose porcentual de la opinión favorable, neutral y desfavorable tanto para videos como para comentarios.

![Análisis de opinión](/help/dashboards/opportunities/assets/youtube-sentiment-distribution.png)

### Vídeos

Una tabla detallada de los vídeos de YouTube analizados con las siguientes columnas:

- **Vídeo**: título y vínculo al vídeo de YouTube.
- **Canal**: el canal de YouTube que publicó el video.
- **Participación**: el nivel de participación (bajo, medio, alto).
- **Menciones de marca**: número de menciones de su marca en comparación con el total de menciones en el video.
- **Cuota de voz**: la proporción de menciones de su marca en comparación con todas las marcas mencionadas.
- **Cinco marcas principales**: las marcas más mencionadas en el vídeo.
- **Opinión**: opinión general sobre su marca en el vídeo.
- **Citas de IA**: número de señales de citas de IA asociadas al vídeo.

La pestaña Rendimiento muestra los paneles **Vídeos** y **Temas** en una vista (con la opción **Vídeos** seleccionada). En la siguiente figura se incluye la tabla a nivel de vídeo y, debajo, el resumen de **Temas**.

![Tablas Vídeos y Temas en la pestaña Rendimiento](/help/dashboards/opportunities/assets/youtube-sentiment-videos.png)

### Comentarios

Una tabla detallada de comentarios de YouTube analizados con las mismas columnas que la tabla Vídeos, filtrada para mostrar los datos a nivel de comentario.

### Temas

Una tabla de temas recurrentes identificados en el contenido analizado que muestra lo siguiente:

- **Tema**: tema o asunto recurrente identificado.
- **Menciones de marca**: número de menciones de la marca asociadas a tema.
- **Opinión**: opinión general asociada al tema.

La tabla **Temas** aparece en la misma vista Rendimiento que la tabla Vídeos; consulte la figura en la sección [Vídeos](#videos) anterior.

## Probar en la demostración

Vea la oportunidad de Análisis de opinión de YouTube en acción usando el entorno de demostración de Frescopa.

[Ver Análisis de opinión de YouTube en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/youtube-analysis/971280f5-6a07-4506-85bf-d7419dca9803?siteId=frescopa-demo)

## Preguntas frecuentes

**¿Por qué YouTube es importante para la búsqueda por IA?**

Los sistemas de IA citan cada vez más vídeos de YouTube a la hora de generar respuestas sobre marcas, productos y temas. Cuando esos vídeos citados hablan de su marca de forma desfavorable o inexacta, esa opinión se incorpora directamente en la forma en que los sistemas de IA representan su marca. Mejorar la forma en que se habla de su marca en el contenido de YouTube que los sistemas de IA ya citan es una de las formas más directas de influir en la percepción de la marca generada por IA.

**¿Por qué no aparece esta oportunidad en mi panel de control?**

Esta oportunidad solo aparece cuando los vídeos de YouTube se detectan como citas para las indicaciones de conjunto de indicaciones del panel de control Presencia de marca. Si no se cita ningún vídeo de YouTube para esas indicaciones, no se mostrará la oportunidad. A medida que su marca obtenga más cobertura de YouTube y que los sistemas de IA citen esos vídeos para su conjunto de indicaciones, la oportunidad estará disponible.

**¿Qué significa Opinión general?**

La opinión general refleja el tono agregado del contenido donde se menciona su marca: favorable, neutral o desfavorable. Se calcula por separado para los vídeos y los comentarios, ya que pueden diferir considerablemente.

**¿Qué es la Cuota de voz?**

La cuota de voz es el porcentaje que representa su marca respecto al total de menciones de marcas en un fragmento de contenido determinado o en todo el contenido analizado, en comparación con todas las demás marcas mencionadas.

**¿Qué son las citas de IA?**

Las citas de IA muestran cuántas respuestas de IA citaron un vídeo determinado. Un mayor número de citas de IA indica que los sistemas de IA utilizan activamente el vídeo a la hora de generar respuestas sobre temas relacionados, lo que hace que la opinión de esos vídeos sea especialmente importante para la representación de IA de su marca.

**¿Cómo se identifican a los competidores del mercado?**

Los competidores se identifican automáticamente en función del sector de su marca y de las marcas que se mencionan conjuntamente con más frecuencia en el contenido analizado. También puede seleccionar manualmente hasta cinco marcas para comparar en el gráfico Seguimiento del mercado.

**¿Con qué frecuencia se actualiza el análisis?**

El análisis de YouTube refleja el contenido analizado hasta la fecha que se muestra en el encabezado del panel de control. Vuelva a visitar la oportunidad, después de implementar las recomendaciones, para efectuar el seguimiento de los cambios en la opinión y la cuota de voz.
