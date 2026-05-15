---
title: Análisis de Opinión de Reddit
description: Aprenda cómo LLM Optimizer analiza los hilos de Reddit para encontrar recomendaciones que mejoren la percepción y visibilidad de su marca en los resultados de Búsqueda por IA.
feature: Opportunities
autotag-review: '2026-05-15T17:56:59.489Z'
TQID: 'https://experienceleague.adobe.com/LRC3nhHrAZoODy4gfsZiR7gc0i8n-IYqvZFj1TAUxsQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1163
ht-degree: 1%

---


# Análisis de Opinión de Reddit

Reddit es una fuente de datos crítica para los modelos de idiomas grandes. Cuando los usuarios preguntan a los asistentes de IA sobre su marca, las respuestas se ven influidas por la opinión de contenido de Reddit. El modo en que se analiza la marca en los subreddits determina directamente cómo los sistemas de IA la comprenden y la representan en las respuestas generadas.

La oportunidad de Análisis de Opinión de Reddit aparece cuando los hilos de Reddit se detectan como citas para peticiones de datos en el conjunto de peticiones de datos del panel de Presencia de marca. Se analizan los hilos citados y sus comentarios en busca de opinión, cuota de voz y temas recurrentes. A continuación, surge la oportunidad de hacer recomendaciones priorizadas para mejorar la forma en que los sistemas de IA perciben y citan su marca.

Analiza su marca en cuatro dimensiones:

- **Publicaciones analizadas** — Número de publicaciones de Reddit examinadas para menciones de la marca y opinión.
- **Comentarios analizados**: número de comentarios examinados en todas las publicaciones analizadas.
- **Menciones de la marca (subprocesos)**: la frecuencia con la que se menciona su marca en los subprocesos analizados.
- **opinión general (subprocesos)**: opinión agregada hacia su marca en todos los subprocesos analizados.

>[!NOTE]
>El análisis de Opinión de Reddit está actualmente en fase beta. Las funciones y la disponibilidad pueden cambiar a medida que la capacidad sigue desarrollándose.

![Panel de análisis de Opinión de Reddit](/help/dashboards/opportunities/assets/reddit-sentiment-overview.png)

## Funcionamiento

LLM Optimizer supervisa los hilos de Reddit citados por los sistemas de IA para buscar indicaciones en el conjunto de peticiones de datos del panel de Presencia de marca. Cuando se detectan subprocesos citados, se analizan esos subprocesos y sus comentarios en busca de menciones de la marca, opinión, cuota de voz y citas de IA. Compara el rendimiento de su marca con los competidores del mercado, identifica los temas recurrentes que impulsan la opinión y genera recomendaciones para abordar las brechas de percepción.

Si no se citan subprocesos de Reddit para las peticiones de datos del conjunto de peticiones de datos, esta oportunidad no aparecerá en el tablero.

Los resultados se muestran en dos fichas: **Sugerencias** y **Rendimiento**.

## Sugerencias

Esta pestaña muestra recomendaciones para mejorar la percepción de tu marca en Reddit. Las sugerencias están organizadas en tres subpestañas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**.

![Ficha Sugerencias](/help/dashboards/opportunities/assets/reddit-sentiment-suggestions.png)

La tabla de sugerencias incluye las siguientes columnas:

- **Sugerencia**: La mejora recomendada para resolver una brecha de percepción.
- **Prioridad**: nivel de urgencia (crítico, alto, Medium, bajo).
- **Elementos de acción**: abre un panel con pasos específicos para implementar la recomendación, incluidos los equipos responsables (por ejemplo, relaciones públicas, administración de la comunidad o marketing de producto).
- **Evidencia**: abre una tabla de orígenes que muestra los subprocesos de Reddit detrás de la sugerencia.

Al expandir una sugerencia, se muestra una sección **Análisis de IA** con:

- **Por qué esto necesita mejorarse**: Una explicación de la brecha de percepción identificada, que incluye el contexto competitivo y cómo se está formando el problema en los hilos de Reddit.
- **Cómo mejorar**: instrucciones específicas sobre qué contenido o acciones solucionarían la brecha.
- **Resultado esperado**: El resultado esperado de implementar la recomendación.

La tabla **Sources** muestra los subprocesos de Reddit que dirigen la sugerencia, con las siguientes columnas:

- **Hilo** — Título y vínculo al hilo de Reddit.
- **Subreddit**: el subreddit donde se publicó el subproceso.
- **Participación** — Nivel de participación (baja, Medium, alta).
- **Menciones de la marca**: recuento de sus menciones de la marca frente al total de menciones en el hilo.
- **Cuota de voz**: la cuota de menciones de tu marca en relación con todas las marcas mencionadas.
- **Principales 5 marcas**: las marcas más mencionadas en el hilo.
- **Opinión**: opinión general hacia su marca en el hilo.
- **Citas de IA**: número de respuestas de IA que citaron este hilo.

## Rendimiento

La pestaña **Rendimiento** proporciona un desglose detallado del rendimiento de tu marca en el contenido de Reddit. Está organizado en cuatro secciones.

### Panorama del mercado

Compara el rendimiento de su marca con el de marcas asociadas y competidores del mercado basándose en las menciones de los hilos.

![Mercado horizontal](/help/dashboards/opportunities/assets/reddit-sentiment-landscape.png)

Muestra lo siguiente:

- **Menciones de la marca en subprocesos**: su cuota de voz frente a marcas asociadas y competidores del mercado.
- **Seguimiento del mercado**: Un gráfico filtrable donde puede seleccionar hasta cinco marcas de la competencia para comparar la cuota de voz entre subprocesos.

### Análisis de opinión

Registra la percepción de la marca en los subprocesos analizados con un gráfico de **Distribución de la Opinión** que muestra el desglose porcentual de la opinión favorable, neutra y desfavorable en los subprocesos.

![Análisis de Opinión](/help/dashboards/opportunities/assets/reddit-sentiment-distribution.png)

### Hilos

Una tabla detallada de los hilos de Reddit analizados con las siguientes columnas:

- **Hilo** — Título y vínculo al hilo de Reddit.
- **Subreddit**: el subreddit donde se publicó el subproceso.
- **Participación** — Nivel de participación (baja, Medium, alta).
- **Menciones de la marca**: recuento de sus menciones de la marca frente al total de menciones en el hilo.
- **Cuota de voz**: la cuota de menciones de tu marca en relación con todas las marcas mencionadas.
- **Principales 5 marcas**: las marcas más mencionadas en el hilo.
- **Opinión**: opinión general hacia su marca en el hilo.
- **Citas de IA**: número de respuestas de IA que citaron este hilo.

### Temas

Una tabla de temas recurrentes identificados en los subprocesos analizados que muestra lo siguiente:

- **Tema**: tema o asunto recurrente identificado.
- **Menciones de la marca**: número de menciones de la marca asociadas con el tema.
- **Opinión**: opinión general asociada al tema.

Al hacer clic en **Detalles** en cualquier tema, se abre un panel desplegable con dos fichas:

- **Análisis**: un resumen de cómo se analiza su marca en los subprocesos asociados con ese tema.
- **Fuentes**: los subprocesos de Reddit específicos que contribuyen a la señal de opinión del tema.

## Probar en la demostración

Vea la oportunidad de Análisis de Opinión de Reddit en acción usando el entorno de demostración de Frescopa.

[Ver análisis de Opinión de Reddit en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/reddit-analysis/b7e4d9a0-3c1f-4e2b-9d5a-8f2c1e0a7b4d?siteId=frescopa-demo)

## Preguntas frecuentes

**¿Por qué Reddit es importante para la Búsqueda por IA?**

Reddit es una de las fuentes más pesadas en los datos de formación LLM y la recuperación en tiempo real. Cuando los sistemas de IA generan respuestas acerca de marcas, productos y temas, las discusiones de Reddit informan con frecuencia el tono, el marco y las afirmaciones fácticas en esas respuestas. Una marca que se discute desfavorablemente o incorrectamente en Reddit es más probable que se represente de esa manera en las respuestas generadas por IA.

**¿Por qué no se muestra esta oportunidad en mi panel?**

Esta oportunidad solo aparece cuando los hilos de Reddit se detectan como citas para mensajes en el conjunto de mensajes del panel de Presencia de marca. Si no se citan hilos de Reddit para esas indicaciones, no se mostrará la oportunidad. A medida que su marca gana más cobertura de Reddit y esos hilos son citados por los sistemas de IA para su conjunto de mensajes, la oportunidad estará disponible.

**¿Qué significa Opinión general?**

La opinión general refleja el tono agregado de los hilos donde se menciona su marca: favorable, neutro o desfavorable calculado en todos los hilos analizados.

**¿Qué es la Cuota de voz?**

La cuota de voz es el porcentaje de menciones de la marca totales de su marca dentro de un hilo determinado o en todos los hilos analizados, en relación con todas las demás marcas mencionadas.

**¿Qué son las citas de IA?**

Las citas de IA muestran cuántas respuestas de IA citaron un hilo determinado. Los recuentos más altos de citas de IA indican que los sistemas de IA están utilizando activamente el hilo al generar respuestas sobre temas relacionados, lo que hace que la opinión en esos hilos sea especialmente importante para la representación de IA de su marca.

**¿Cómo se identifican los competidores del mercado?**

Los competidores se identifican automáticamente en función del sector de su marca y de las marcas que se mencionan conjuntamente con más frecuencia en los hilos analizados. También puede seleccionar manualmente hasta cinco marcas para comparar en el gráfico de seguimiento de mercado.

**¿Con qué frecuencia se actualiza el análisis?**

El análisis de Reddit refleja el contenido analizado hasta la fecha que se muestra en el encabezado del panel. Vuelva a visitar la oportunidad, después de implementar las recomendaciones, para rastrear los cambios en la opinión y la cuota de voz.
