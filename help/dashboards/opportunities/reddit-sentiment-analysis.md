---
title: Análisis de opinión de Reddit
description: Descubra cómo LLM Optimizer analiza los hilos de Reddit para mostrar recomendaciones que mejoren la percepción y visibilidad de su marca en los resultados de la búsqueda por IA.
feature: Opportunities
autotag-review: '2026-05-15T17:56:59.489Z'
TQID: 'https://experienceleague.adobe.com/LRC3nhHrAZoODy4gfsZiR7gc0i8n-IYqvZFj1TAUxsQ'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1163
ht-degree: 100%

---


# Análisis de opinión de Reddit

Reddit es una fuente de datos vital para los LLM (Large Language Models) Cuando los usuarios preguntan a los asistentes de IA sobre su marca, las respuestas se ven influidas por la opinión de contenido de Reddit. El modo en que se habla de la marca en los subreddits determina directamente cómo los sistemas de IA la comprenden y la representan en las respuestas generadas.

La oportunidad de Análisis de opinión de Reddit aparece cuando los hilos de Reddit se detectan como citas para las indicaciones en el conjunto de indicaciones del panel de control Presencia de marca. Analiza esos hilos citados y sus comentarios en busca de opinión, cuota de voz y temas recurrentes. A continuación, muestra recomendaciones priorizadas para mejorar la forma en que los sistemas de IA perciben y citan su marca.

Analiza su marca en cuatro dimensiones:

- **Publicaciones analizadas**: número de publicaciones de Reddit examinadas en busca de las menciones a la marca y la opinión.
- **Comentarios analizados**: número de comentarios examinados en todas las publicaciones analizadas.
- **Menciones de marca (hilos)**: la frecuencia con la que se menciona su marca en los hilos analizados.
- **Opinión general (hilos)**: opinión agregada sobre su marca en todos los hilos analizados.

>[!NOTE]
>El Análisis de opinión de Reddit está actualmente en fase Beta. Las funciones y la disponibilidad pueden cambiar a medida que la funcionalidad sigue desarrollándose.

![Panel de control Análisis de opinión de Reddit](/help/dashboards/opportunities/assets/reddit-sentiment-overview.png)

## Funcionamiento

LLM Optimizer supervisa los hilos de Reddit citados por los sistemas de IA para buscar indicaciones en el conjunto de indicaciones del panel de control Presencia de marca. Cuando se detectan hilos citados, analiza esos hilos y sus comentarios en busca de menciones de marca, opinión, cuota de voz y citas de IA. Compara el rendimiento de su marca con el de la competencia del mercado, identifica los temas recurrentes que influyen en la opinión y ofrece recomendaciones para subsanar las diferencias de percepción.

Si no se citan los hilos de Reddit para las indicaciones del conjunto de indicaciones, esta oportunidad no aparecerá en el panel de control.

Los resultados se muestran en dos pestañas: **Sugerencias** y **Rendimiento**.

## Sugerencias

Esta pestaña muestra recomendaciones para mejorar la percepción de su marca en Reddit. Las sugerencias están organizadas en tres subpestañas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**.

![Pestaña Sugerencias](/help/dashboards/opportunities/assets/reddit-sentiment-suggestions.png)

La tabla de sugerencias incluye las siguientes columnas:

- **Sugerencia**: la mejora recomendada para subsanar una diferencia de percepción.
- **Prioridad**: nivel de urgencia (crítica, alta, media, baja).
- **Elementos de acción**: abre un panel con pasos específicos para implementar la recomendación, incluidos los equipos responsables (por ejemplo, relaciones públicas, administración de la comunidad o marketing de producto).
- **Evidencia**: abre una tabla de fuentes que muestra los hilos de Reddit que respaldan la sugerencia.

Al expandir una sugerencia, se muestra una sección **Análisis de IA** con lo siguiente:

- **Por qué esto necesita una mejora**: una explicación de la diferencia de percepción identificada, incluyendo el contexto competitivo y cómo se está manifestando el problema en los hilos de Reddit.
- **Cómo mejorar**: directrices específicas sobre qué contenido o acciones permitirían subsanar esta carencia.
- **Resultado esperado**: el resultado esperado de la implementación de la recomendación.

La tabla **Fuentes** muestra los hilos de Reddit que generan la sugerencia, con las siguientes columnas:

- **Hilo**: título y vínculo al hilo de Reddit.
- **Subreddit**: el subreddit donde se publicó el hilo.
- **Participación**: el nivel de participación (bajo, medio, alto).
- **Menciones de marca**: número de menciones de su marca en comparación con el total de menciones en el hilo.
- **Cuota de voz**: la proporción de menciones de su marca en comparación con todas las marcas mencionadas.
- **Cinco marcas principales**: las marcas más mencionadas en el hilo.
- **Opinión**: opinión general sobre su marca en el hilo.
- **Citas de IA**: número de respuestas de IA que citaron este hilo.

## Rendimiento

La pestaña **Rendimiento** proporciona un desglose detallado del rendimiento de su marca en el contenido de Reddit. Se organiza en cuatro secciones.

### Panorama del mercado

Compare el rendimiento de su marca con las marcas asociadas y la competencia del mercado en función de las menciones en los hilos.

![Panorama del mercado](/help/dashboards/opportunities/assets/reddit-sentiment-landscape.png)

Incluye lo siguiente:

- **Menciones de marca en hilos**: su cuota de voz frente a las marcas asociadas y la competencia del mercado.
- **Seguimiento del mercado**: un gráfico filtrable donde puede seleccionar hasta cinco marcas de la competencia para comparar la cuota de voz en los hilos.

### Análisis de opinión

Registra la percepción de la marca en los hilos analizados con un gráfico de **Distribución de opiniones** que muestra el desglose porcentual de la opinión favorable, neutra y desfavorable en los hilos.

![Análisis de opinión](/help/dashboards/opportunities/assets/reddit-sentiment-distribution.png)

### Hilos

Una tabla detallada de los hilos de Reddit analizados con las siguientes columnas:

- **Hilo**: título y vínculo al hilo de Reddit.
- **Subreddit**: el subreddit donde se publicó el hilo.
- **Participación**: el nivel de participación (bajo, medio, alto).
- **Menciones de marca**: número de menciones de su marca en comparación con el total de menciones en el hilo.
- **Cuota de voz**: la proporción de menciones de su marca en comparación con todas las marcas mencionadas.
- **Cinco marcas principales**: las marcas más mencionadas en el hilo.
- **Opinión**: opinión general sobre su marca en el hilo.
- **Citas de IA**: número de respuestas de IA que citaron este hilo.

### Temas

Una tabla de temas recurrentes identificados en los hilos analizados que muestra lo siguiente:

- **Tema**: tema o asunto recurrente identificado.
- **Menciones de marca**: número de menciones de la marca asociadas a tema.
- **Opinión**: opinión general asociada al tema.

Al hacer clic en **Detalles** en cualquier tema, se abre un panel desplegable con dos pestañas:

- **Análisis**: un resumen de cómo se habla de su marca en los hilos de Reddit asociados a ese tema.
- **Fuentes**: los hilos de Reddit específicos que contribuyen a la señal de opinión sobre el tema.

## Probar en la demostración

Vea la oportunidad de Análisis de opinión de Reddit en acción usando el entorno de demostración de Frescopa.

[Ver Análisis de opinión de Reddit en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/reddit-analysis/b7e4d9a0-3c1f-4e2b-9d5a-8f2c1e0a7b4d?siteId=frescopa-demo)

## Preguntas frecuentes

**¿Por qué Reddit es importante para la búsqueda por IA?**

Reddit es una de las fuentes con mayor preso en los datos de capacitación de LLM y la recuperación en tiempo real. Cuando los sistemas de IA generan respuestas sobre marcas, productos y temas, los debates de Reddit informan con frecuencia sobre el tono, el contexto y las afirmaciones objetivas de dichas respuestas. Una marca sobre la que se habla de forma desfavorable o incorrecta en Reddit es más probable que se represente de esa manera en las respuestas generadas por IA.

**¿Por qué no se muestra esta oportunidad en mi panel de control?**

Esta oportunidad solo aparece cuando los hilos de Reddit se detectan como citas para las indicaciones en el conjunto de indicaciones del panel de control Presencia de marca. Si no se citan los hilos de Reddit para esas indicaciones, no se mostrará la oportunidad. A medida que su marca vaya ganando más cobertura en Reddit y los sistemas de IA citen esos hilos para su conjunto de indicaciones, la oportunidad estará disponible.

**¿Qué significa Opinión general?**

La opinión general refleja el tono agregado de los hilos donde se menciona su marca: favorable, neutro o desfavorable calculada en todos los hilos analizados.

**¿Qué es la Cuota de voz?**

La cuota de voz es el porcentaje que representa su marca respecto al total de menciones de marcas en un hilo determinado o en todo los hilos analizados, en comparación con todas las demás marcas mencionadas.

**¿Qué son las citas de IA?**

Las citas de IA muestran cuántas respuestas de IA citaron un hilo determinado. Un mayor número de citas de IA indica que los sistemas de IA utilizan activamente el hilo a la hora de generar respuestas sobre temas relacionados, lo que hace que la opinión de esos hilos sea especialmente importante para la representación de IA de su marca.

**¿Cómo se identifican los competidores del mercado?**

Los competidores se identifican automáticamente en función del sector de su marca y de las marcas que se mencionan conjuntamente con más frecuencia en los hilos analizados. También puede seleccionar manualmente hasta cinco marcas para comparar en el gráfico Seguimiento del mercado.

**¿Con qué frecuencia se actualiza el análisis?**

El análisis de Reddit refleja el contenido analizado hasta la fecha que se muestra en el encabezado del panel de control. Vuelva a visitar la oportunidad, después de implementar las recomendaciones, para efectuar el seguimiento de los cambios en la opinión y la cuota de voz.
