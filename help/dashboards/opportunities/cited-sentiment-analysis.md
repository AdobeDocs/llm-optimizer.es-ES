---
title: Análisis de Opinión citado
description: Descubra cómo LLM Optimizer analiza las URL más citadas para ofrecer recomendaciones que mejoren la percepción y visibilidad de su marca en los resultados de Búsqueda por IA.
feature: Opportunities
autotag-review: '2026-05-15T17:39:50.086Z'
TQID: 'https://experienceleague.adobe.com/ZqgWup29QoQ-j0fDM6DqhGpzRqscg1f-fdXHTMN9fIk'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1030
ht-degree: 1%

---


# Análisis de Opinión citado

Cuando los sistemas de IA responden preguntas sobre su marca, dependen de un conjunto de URL citadas anteriormente: páginas web de terceros a las que se hace referencia con frecuencia en las respuestas generadas por IA. La forma en que se representa su marca en esas páginas determina directamente cómo los sistemas de IA la representan a los usuarios.

La oportunidad de Análisis de Opinión citada analiza las direcciones URL más citadas detectadas para buscar mensajes en el conjunto de mensajes del panel de Presencia de marca. Evalúa menciones de la marca, opinión, cuota de voz y temas recurrentes en esas páginas. Después, aparecen recomendaciones priorizadas para mejorar la forma en que se percibe su marca en los sistemas de IA de contenido en los que más se basan.

Se muestran cuatro métricas clave:

- **Páginas analizadas**: número de páginas web citadas examinadas para detectar menciones de la marca y opinión.
- **Páginas omitidas**: número de páginas que no se pudieron analizar (por ejemplo, debido a restricciones de acceso).
- **Menciones de la marca (páginas)**: la frecuencia con la que se menciona su marca en las páginas analizadas.
- **opinión general (páginas)**: opinión agregada hacia su marca en las páginas analizadas.

>[!NOTE]
>El análisis de Opinión citado está actualmente en fase beta. Las funciones y la disponibilidad pueden cambiar a medida que la capacidad sigue desarrollándose.

![Panel de análisis de Opinión citado](/help/dashboards/opportunities/assets/cited-sentiment-overview.png)

## Funcionamiento

LLM Optimizer identifica las direcciones URL más citadas que aparecen en las respuestas generadas por IA para las peticiones de datos del conjunto de peticiones de datos del panel de Presencia de marca. Analiza esas páginas en busca de menciones de la marca, opinión, cuota de voz y citas de IA. Compara el rendimiento de su marca con los competidores del mercado, identifica temas recurrentes y genera recomendaciones para abordar las brechas de percepción en las páginas más importantes para los sistemas de IA.

Si no se detectan direcciones URL citadas para los indicadores del conjunto de mensajes, esta oportunidad no aparecerá en el panel.

Los resultados se muestran en dos fichas: **Sugerencias** y **Rendimiento**.

## Sugerencias

Esta pestaña muestra recomendaciones para mejorar la percepción de su marca en las direcciones URL más citadas. Las sugerencias están organizadas en tres subpestañas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**.

![Ficha Sugerencias](/help/dashboards/opportunities/assets/cited-sentiment-suggestions.png)

La tabla de sugerencias incluye las siguientes columnas:

- **Sugerencia**: La mejora recomendada para resolver una brecha de percepción.
- **Prioridad**: nivel de urgencia (crítico, alto, Medium, bajo).
- **Elementos de acción**: abre un panel con pasos específicos para implementar la recomendación, incluidos los equipos responsables.

Al expandir una sugerencia, se muestra una sección **Análisis de IA** con:

- **Por qué esto necesita mejorarse**: Una explicación de la brecha de percepción identificada, incluidas las URL citadas que no representan suficientemente su marca y contexto competitivo.
- **Cómo mejorar**: directrices específicas sobre acciones de alcance, creación de contenido o asociación para resolver la brecha.
- **Resultado esperado**: El resultado esperado de implementar la recomendación.

## Rendimiento

La ficha **Rendimiento** proporciona un desglose detallado del rendimiento de su marca en las páginas más citadas. Está organizado en cuatro secciones.

### Panorama del mercado

Compara el rendimiento de su marca con las marcas asociadas y con los competidores del mercado en función de las menciones de las páginas citadas.

![Mercado horizontal](/help/dashboards/opportunities/assets/cited-sentiment-landscape.png)

Muestra lo siguiente:

- **Menciones de la marca en páginas**: su cuota de voz frente a marcas asociadas y competidores del mercado.
- **Seguimiento del mercado**: Un gráfico filtrable donde puedes seleccionar hasta cinco marcas de la competencia para comparar la cuota de voz en las páginas analizadas.

### Análisis de opinión

Registra la percepción de la marca en las páginas analizadas con un gráfico de **Distribución de la Opinión** que muestra el desglose porcentual de la opinión favorable, neutral y desfavorable en todas las páginas.

![Análisis de Opinión](/help/dashboards/opportunities/assets/cited-sentiment-distribution.png)

### Páginas

Una tabla detallada de páginas web citadas analizadas con las siguientes columnas:

- **Página** — URL de la página analizada.
- **Menciones de la marca**: recuento de menciones de la marca frente al total de menciones en la página.
- **Cuota de voz**: la cuota de menciones de tu marca en relación con todas las marcas mencionadas.
- **Principales 5 marcas**: las marcas más mencionadas en la página.
- **Opinión**: opinión general hacia su marca en la página.
- **Citas de IA** — Cantidad de respuestas de IA que citaron esta página.

### Temas

Una tabla de temas recurrentes identificados en las páginas analizadas que muestra lo siguiente:

- **Tema**: tema o asunto recurrente identificado.
- **Menciones de la marca**: número de menciones de la marca asociadas con el tema.
- **Opinión**: opinión general asociada al tema.

Al hacer clic en **Detalles** en cualquier tema, se abre un desglose con un resumen de análisis y las páginas de origen que aportan datos.

## Probar en la demostración

Vea la oportunidad de Análisis de Opinión Citado en acción usando el entorno de demostración de Frescopa - [Ver Análisis de Opinión Citado en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/cited-analysis/d3a8b217-9f4c-4e88-a612-6b7f91e5c044?siteId=frescopa-demo).

## Preguntas frecuentes

**¿Por qué importan las direcciones URL más citadas para la Búsqueda por IA?**

Las direcciones URL más citadas son las páginas de terceros a las que los sistemas de IA hacen referencia con mayor frecuencia al generar respuestas acerca de su marca. La opinión y el encuadre de esas páginas influyen de manera directa y desmesurada en la forma en que la IA representa su marca, más que las páginas que rara vez se citan. Mejorar la forma en que se representa su marca en esas páginas específicas es una de las acciones de mayor aprovechamiento que puede realizar para aumentar la visibilidad de la IA.

**¿Por qué no se muestra esta oportunidad en mi panel?**

Esta oportunidad solo aparece cuando se detectan direcciones URL citadas para mensajes en el conjunto de mensajes del panel de Presencia de marca. Si no se han identificado direcciones URL citadas para esas indicaciones, no se mostrará la oportunidad.

**¿Qué significa Páginas omitidas?**

Las páginas omitidas son direcciones URL citadas que no se han podido analizar, normalmente porque la página está detrás de un Paywall, requiere autenticación o bloquea acceso automatizado. Estas páginas se cuentan, pero se excluyen del análisis de opinión y mención de la marca.

**¿Qué es la Cuota de voz?**

La cuota de voz es el porcentaje de menciones de la marca totales de su marca en una página determinada o en todas las páginas analizadas, en relación con todas las demás marcas mencionadas.

**¿Qué son las citas de IA?**

Las citas de IA muestran cuántas respuestas de IA citaron una página determinada. Los recuentos más altos de citas de IA indican que los sistemas de IA están utilizando activamente la página al generar respuestas sobre temas relacionados, lo que hace que la opinión en esas páginas sea especialmente importante para la representación de IA de su marca.

**¿Cómo se identifican los competidores del mercado?**

Los competidores se identifican automáticamente en función del sector de su marca y de las marcas que se mencionan conjuntamente con más frecuencia en las páginas analizadas. También puede seleccionar manualmente hasta cinco marcas para comparar en el gráfico de seguimiento de mercado.

**¿Con qué frecuencia se actualiza el análisis?**

El análisis refleja las direcciones URL citadas detectadas hasta la fecha que se muestra en el encabezado del panel. Vuelva a visitar la oportunidad, después de implementar las recomendaciones, para rastrear los cambios en la opinión y la cuota de voz.
