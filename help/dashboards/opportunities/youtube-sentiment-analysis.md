---
title: Análisis de Opinión de YouTube
description: Descubra cómo LLM Optimizer analiza los vídeos y comentarios de YouTube para mostrar recomendaciones que mejoran la percepción y visibilidad de su marca en los resultados de Búsqueda por IA.
feature: Opportunities
autotag-review: '2026-05-15T18:12:18.358Z'
TQID: 'https://experienceleague.adobe.com/XevtwbOrmn6QTjMxnErSTI91WUv9m6GYWJ7LeLXdXXg'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1255
ht-degree: 1%

---


# Análisis de Opinión de YouTube

YouTube es una de las plataformas más influyentes que modela la percepción del consumidor y la reputación de la marca. Cuando los sistemas de IA responden a preguntas sobre su marca, cada vez más citan los vídeos de YouTube como fuentes, lo que hace que la forma en que se habla de su marca en ese contenido sea una entrada directa en las respuestas generadas por IA.

La oportunidad de análisis de Opinión de YouTube aparece cuando los vídeos de YouTube se detectan como citas para mensajes en el conjunto de mensajes del panel de Presencia de marca. Se analizan los videos citados y sus comentarios para opinión, cuota de voz y temas recurrentes. A continuación, aparecen recomendaciones priorizadas para mejorar la forma en que se percibe y representa su marca en las respuestas generadas por IA.

Analiza su marca en seis dimensiones:

- **Vídeos analizados**: número de vídeos de YouTube examinados para detectar menciones de la marca y opinión.
- **Comentarios analizados**: número de comentarios examinados en todos los vídeos analizados.
- **Menciones de la marca (vídeos)**: la frecuencia con la que se menciona su marca en el contenido de vídeo.
- **Menciones de la marca (comentarios)**: la frecuencia con la que se menciona su marca en los comentarios.
- **opinión general (vídeos)**: opinión agregada hacia su marca en el contenido de vídeo.
- **opinión general (comentarios)**: opinión agregada hacia su marca en los comentarios.

>[!NOTE]
>El análisis de Opinión de YouTube está actualmente en fase beta. Las funciones y la disponibilidad pueden cambiar a medida que la capacidad sigue desarrollándose.

![Panel de análisis de Opinión de YouTube](/help/dashboards/opportunities/assets/youtube-sentiment-overview.png)

## Funcionamiento

LLM Optimizer supervisa los vídeos de YouTube citados por los sistemas de IA para buscar indicadores en el conjunto de mensajes del panel de Presencia de marca. Cuando se detectan vídeos citados, se analizan esos vídeos y sus comentarios en busca de menciones de la marca, opinión, cuota de voz y citas de IA. Compara el rendimiento de su marca con los competidores del mercado y las marcas asociadas, identifica los temas recurrentes que impulsan la opinión y genera recomendaciones para abordar las brechas de percepción.

Si no se citan vídeos de YouTube para las indicaciones del conjunto de indicaciones, esta oportunidad no aparecerá en el tablero.

Los resultados se muestran en dos fichas: **Sugerencias** y **Rendimiento**.

## Sugerencias

Esta pestaña muestra recomendaciones para mejorar la percepción de su marca en YouTube. Las sugerencias están organizadas en tres subpestañas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**.

![Ficha Sugerencias](/help/dashboards/opportunities/assets/youtube-sentiment-suggestions.png)

La tabla de sugerencias incluye las siguientes columnas:

- **Sugerencia**: La mejora recomendada para resolver una brecha de percepción.
- **Prioridad**: nivel de urgencia (crítico, alto, Medium, bajo).
- **Elementos de acción**: abre un panel con pasos específicos para implementar la recomendación, incluidos los equipos responsables (por ejemplo, Estrategia de contenido, Marketing influenciador, Marketing de productos).
- **Evidencia**: abre una tabla de orígenes que muestra los vídeos detrás de la sugerencia.

Al expandir una sugerencia, se muestra una sección **Análisis de IA** con:

- **Por qué esto necesita mejorarse**: Una explicación de la brecha de percepción identificada, que incluye el contexto competitivo y cómo se está formando el problema en el contenido de YouTube.
- **Cómo mejorar**: instrucciones específicas sobre qué contenido o acciones solucionarían la brecha.
- **Resultado esperado**: El resultado esperado de implementar la recomendación.

La tabla **Sources** muestra los vídeos de YouTube que dirigen la sugerencia, con las siguientes columnas:

- **Vídeo**: título y vínculo al vídeo de YouTube.
- **Canal**: El canal de YouTube que publicó el vídeo.
- **Participación** — Nivel de participación (baja, Medium, alta).
- **Menciones de la marca**: recuento de menciones de la marca frente al total de menciones del vídeo.
- **Cuota de voz**: la cuota de menciones de tu marca en relación con todas las marcas mencionadas.
- **Principales 5 marcas**: Las marcas más mencionadas en el vídeo.
- **Opinión**: opinión general hacia su marca en el vídeo.
- **Citas de IA** — Cantidad de respuestas de IA que citaron este video.

## Rendimiento

La ficha **Rendimiento** proporciona un desglose detallado del rendimiento de su marca en el contenido de YouTube. Está organizado en cuatro secciones.

### Panorama del mercado

Compara el rendimiento de su marca con las marcas asociadas y con los competidores del mercado en función de las menciones.

![Mercado horizontal](/help/dashboards/opportunities/assets/youtube-sentiment-market-landscape.png)

Muestra lo siguiente:

- **Menciones de la marca en vídeos**: su cuota de voz frente a marcas asociadas y competidores del mercado.
- **Menciones de la marca en comentarios**: la misma comparación entre el contenido de los comentarios.
- **Seguimiento del mercado**: Un gráfico filtrable donde puedes seleccionar hasta cinco marcas de la competencia para comparar la cuota de voz entre vídeos y comentarios.

### Análisis de opinión

Registra la percepción de la marca en el contenido analizado con un gráfico de **Distribución de Opinión** que muestra el desglose porcentual de la opinión favorable, neutral y desfavorable tanto para vídeos como para comentarios.

![Análisis de Opinión](/help/dashboards/opportunities/assets/youtube-sentiment-distribution.png)

### Vídeos

Una tabla detallada de los vídeos de YouTube analizados con las siguientes columnas:

- **Vídeo**: título y vínculo al vídeo de YouTube.
- **Canal**: El canal de YouTube que publicó el vídeo.
- **Participación** — Nivel de participación (baja, Medium, alta).
- **Menciones de la marca**: recuento de menciones de la marca frente al total de menciones del vídeo.
- **Cuota de voz**: la cuota de menciones de tu marca en relación con todas las marcas mencionadas.
- **Principales 5 marcas**: Las marcas más mencionadas en el vídeo.
- **Opinión**: opinión general hacia su marca en el vídeo.
- **Citas de IA**: número de señales de citas de IA asociadas con el vídeo.

La ficha Rendimiento muestra los paneles **Vídeos** y **Temas** en una vista (con **Vídeos** seleccionados). La siguiente figura incluye la tabla de nivel de vídeo y, debajo, el resumen de **Temas**.

![Tablas de vídeos y temas en la ficha Rendimiento](/help/dashboards/opportunities/assets/youtube-sentiment-videos.png)

### Comentarios

Una tabla detallada de comentarios de YouTube analizados con las mismas columnas que la tabla Vídeos, filtrados a datos de nivel de comentario.

### Temas

Una tabla de temas recurrentes identificados en el contenido analizado que muestra lo siguiente:

- **Tema**: tema o asunto recurrente identificado.
- **Menciones de la marca**: número de menciones de la marca asociadas con el tema.
- **Opinión**: opinión general asociada al tema.

La tabla **Temas** aparece en la misma vista Rendimiento que la tabla Vídeos; consulte la figura en la sección [Vídeos](#videos) anterior.

## Probar en la demostración

Vea la oportunidad de análisis de Opinión de YouTube en acción usando el entorno de demostración de Frescopa.

[Ver análisis de Opinión de YouTube en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/youtube-analysis/971280f5-6a07-4506-85bf-d7419dca9803?siteId=frescopa-demo)

## Preguntas frecuentes

**¿Por qué YouTube es importante para la Búsqueda por IA?**

Los sistemas de IA citan cada vez más vídeos de YouTube al generar respuestas sobre marcas, productos y temas. Cuando los vídeos citados analizan su marca de forma desfavorable o inexacta, esa opinión se incorpora directamente en la forma en que los sistemas de IA representan su marca. La mejora de la forma en que se analiza su marca en el contenido de YouTube que los sistemas de IA ya citan es una de las formas más directas de influir en la percepción de la marca generada por IA.

**¿Por qué no se muestra esta oportunidad en mi panel?**

Esta oportunidad solo aparece cuando los vídeos de YouTube se detectan como citas para mensajes en el conjunto de mensajes del panel de Presencia de marca. Si no se cita ningún vídeo de YouTube para esas indicaciones, no se mostrará la oportunidad. A medida que su marca obtenga más cobertura de YouTube y que los sistemas de IA citen esos vídeos para su conjunto de mensajes, la oportunidad estará disponible.

**¿Qué significa Opinión general?**

La opinión general refleja el tono agregado del contenido donde se menciona su marca: favorable, neutral o desfavorable. Se calcula por separado para los vídeos y los comentarios, ya que pueden diferir considerablemente.

**¿Qué es la Cuota de voz?**

La cuota de voz es el porcentaje de menciones de la marca totales de su marca dentro de un fragmento de contenido determinado o en todo el contenido analizado, en relación con todas las demás marcas mencionadas.

**¿Qué son las citas de IA?**

Las citas de IA muestran cuántas respuestas de IA citaron un vídeo determinado. Los recuentos más altos de citas de IA indican que los sistemas de IA están utilizando activamente el vídeo al generar respuestas sobre temas relacionados, lo que hace que la opinión en esos vídeos sea especialmente importante para la representación de IA de su marca.

**¿Cómo se identifican los competidores del mercado?**

Los competidores se identifican automáticamente en función del sector de su marca y de las marcas que se mencionan conjuntamente con más frecuencia en el contenido analizado. También puede seleccionar manualmente hasta cinco marcas para comparar en el gráfico de seguimiento de mercado.

**¿Con qué frecuencia se actualiza el análisis?**

El análisis de YouTube refleja el contenido analizado hasta la fecha que se muestra en el encabezado del panel. Vuelva a visitar la oportunidad, después de implementar las recomendaciones, para rastrear los cambios en la opinión y la cuota de voz.
