---
title: Oportunidades de optimización
description: Aprenda a utilizar el panel de control de oportunidades para detectar automáticamente cómo se puede mejorar el sitio a fin de aumentar la visibilidad de la marca.
feature: Opportunities
autotag-review: '2026-05-15T17:53:48.623Z'
TQID: 'https://experienceleague.adobe.com/FAbQhzuyT-kIitIaoVQ47dam-TpN-deU5Vbo1nmK5CA'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1227
ht-degree: 31%

---


# Oportunidades de optimización

Las oportunidades de optimización consisten en información detectada automáticamente que muestra dónde se puede mejorar su sitio y su presencia externa para aumentar la visibilidad de la marca en la búsqueda por IA.

Estas optimizaciones incluyen correcciones en la página (añadir contenido estructurado, canónicos o resúmenes), ajustes técnicos (desbloquear rastreadores de IA o resolver errores) e influir en el contenido en sitios de terceros con autoridad. Aprovechar estas oportunidades de optimización ayuda a que su marca se represente con precisión y tenga más probabilidades de citarse en respuestas generativas.

![Oportunidades de optimización](/help/dashboards/assets/oport.png)

## Panel de control Oportunidades

Las oportunidades de optimización que se presentan en el panel de control se priorizan en función de las deficiencias de los jugadores, los temas en tendencia y los datos de rendimiento, y se presentan como una lista. Puede buscar una oportunidad específica utilizando el campo de búsqueda. Además, las oportunidades se agrupan por etiquetas y puede hacer clic directamente en una etiqueta para mostrar todas las oportunidades agrupadas bajo dicha etiqueta.

Al hacer clic en **Detalles**, se abre una ventana independiente donde se ofrece más información y sugerencias adicionales.

## Oportunidades compatibles

A continuación se muestra una tabla de las oportunidades compatibles actualmente:

| Oportunidad | Tipo | Problemas identificados | Sugerencias de correcciones |
|---------|----------|----------|----------|
| [Agregar resúmenes compatibles con LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | Contenido (en el sitio) | Identifica páginas de alto tráfico que carecen de resúmenes concisos y puntos clave estructurados a nivel de página o sección, lo que dificulta que los agentes de IA analicen e interpreten las afirmaciones de marca. Muestra las direcciones URL afectadas y donde se recomiendan los resúmenes. | Revise los resúmenes generados por IA y los puntos clave basados en el contenido existente, luego implemente en el perímetro de CDN con Optimizar en Edge para que los agentes reciban un contexto más claro y analizable. |
| [Agregar preguntas más frecuentes](/help/dashboards/opportunities/add-relevant-faqs.md) | Contenido (en el sitio) | Identifica páginas de alto tráfico que carecen de contenido de preguntas y respuestas estructurado y que están alineadas con el conjunto de mensajes, lo que dificulta que los agentes de inteligencia artificial relacionen las preguntas del usuario con su página. Muestra las direcciones URL afectadas y donde se recomiendan las preguntas frecuentes. | Revise el contenido de preguntas más frecuentes generado por IA y alineado por intención basado en el material de página existente e impleméntelo en el perímetro de CDN con Optimizar en Edge para que los agentes reciban un contexto de preguntas y respuestas más claro. |
| [Agregar resúmenes de transcripciones multimedia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | Contenido (en el sitio) | Identifica las páginas en las que la información clave está incrustada en vídeo u otros medios sin transcripciones o resúmenes legibles por el equipo, lo que dificulta el uso del contenido para los agentes de IA. Muestra las direcciones URL afectadas y el texto recomendado. | Revise los resúmenes de transcripción generados por IA basados en los medios y en la página y, a continuación, implemente en el perímetro de CDN con Optimizar en Edge para que los agentes reciban texto legible por el equipo (por ejemplo, cerca del vídeo correspondiente). |
| [Tráfico bloqueado por robots.txt](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | Optimización técnica del motor generativo | Analiza el archivo robots.txt en busca de reglas que bloqueen selectivamente a los agentes de IA de contenido que, de lo contrario, sería accesible públicamente. Informa de las direcciones URL afectadas y los agentes bloqueados. | Actualice el archivo robots.txt para permitir el acceso a los rastreadores de IA admitidos donde corresponda. |
| [Errores de tráfico de agente](/help/dashboards/opportunities/agentic-traffic-errors.md) | Optimización técnica del motor generativo | Supervisa los registros de CDN para las respuestas de error 404, 403 y 5xx devueltas a los agentes de IA. Informa de las direcciones URL afectadas y el total de visitas perdidas. | Corrija los vínculos rotos, actualice los permisos y resuelva los problemas del lado del servidor para que el contenido clave devuelva 200 respuestas. |
| [Simplificar contenido complejo](/help/dashboards/opportunities/simplify-complex-content.md) | Contenido (en el sitio) | Identifica páginas de alto tráfico en las que una copia densa o compleja se encuentra por debajo de los umbrales de legibilidad, lo que dificulta a los agentes de inteligencia artificial la interpretación de la información clave. Muestra las direcciones URL afectadas y donde se recomienda utilizar texto simplificado. | Revise el texto mejorado generado por IA basado en el contenido de la página existente e impleméntelo en el extremo de la CDN con Optimización en Edge para que los agentes reciban pasajes más claros y fáciles de analizar. |
| [Recuperar Visibilidad del contenido](/help/dashboards/opportunities/recover-content-visibility.md) | Optimización técnica del motor generativo | Indica las páginas donde se oculta contenido crítico para los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Preprocese las páginas en la capa de CDN mediante Optimizar en Edge para que los agentes de IA puedan acceder a más contenido sin ejecutar JavaScript. |
| [Agregar tabla de contenido](/help/dashboards/opportunities/add-table-of-contents.md) | Optimización técnica del motor generativo | Detecta páginas que carecen de encabezados de navegación u organización estructural claros, lo que dificulta que los agentes de IA analicen y asignen contenido a consultas de usuarios. Muestra las direcciones URL afectadas y donde se recomienda una tabla de contenido estructurada. | Revise la tabla de contenido estructurada sugerida con encabezados enlazados con anclaje que reflejen las secciones principales de la página y luego implemente en el extremo CDN con Optimizar en Edge para que se inserte una tabla de contenido en HTML, lo que mejora la estructura de la página para que los modelos puedan extraer, asignar y citar más fácilmente secciones relevantes. |
| [Análisis de Wikipedia](/help/dashboards/opportunities/wikipedia-analysis.md) | Fuera del sitio | Analiza la página de Wikipedia de su empresa en relación con los competidores del sector en cuanto a referencias, secciones, duración del contenido, imágenes e integridad del cuadro de información. Identifica lagunas específicas en las que la página no alcanza los valores de referencia del sector. | Revise las recomendaciones estratégicas generadas por IA para mejorar su presencia en Wikipedia, incluyendo la adición de referencias, el enriquecimiento de su infobox, la expansión de secciones y la mejora de la calidad del artículo. |
| [Análisis de Opinión de YouTube (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza los vídeos de YouTube citados para el conjunto de mensajes de Presencia de marca en menciones de la marca, opinión, cuota de voz y temas recurrentes. Solo aparece cuando los vídeos de YouTube se detectan como citas para el conjunto de mensajes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en todo el contenido de YouTube, incluidas las acciones sugeridas y los equipos responsables de implementarlas. |
| [Análisis de Opinión de Reddit (Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza los hilos de Reddit citados para el conjunto de mensajes de Presencia de marca para menciones de la marca, opinión, cuota de voz y temas recurrentes. Solo aparece cuando los hilos de Reddit se detectan como citas para el conjunto de mensajes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en todo el contenido de Reddit, incluidas las acciones sugeridas y los equipos responsables de implementarlas. |
| [Análisis de Opinión citado (Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza las direcciones URL más citadas detectadas para los mensajes de Presencia de marca establecidos para menciones de la marca, opinión, cuota de voz y temas recurrentes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en las páginas que más citan los sistemas de IA al responder a las preguntas sobre su marca. |
| [Enriquecer catálogo de productos (Beta)](/help/dashboards/opportunities/enrich-product-catalog.md) | Contenido (in situ), Adobe Commerce | Identifica los productos del catálogo de Commerce cuyos nombres o descripciones son demasiado genéricos, técnicamente densos o ambiguos para que los LLM los interpreten. Muestra los PDP evaluados, el contexto de tráfico auténtico y los enriquecimientos narrativos generados por IA. | Revise y edite los nombres y las descripciones de los productos propuestos y, a continuación, implemente optimizaciones para publicar actualizaciones directamente en el catálogo de Adobe Commerce (con la reversión de Sugerencias fijas). |
| [Enriquecer páginas de detalles del producto](/help/dashboards/opportunities/enrich-product-detail-pages.md) | Información geográfica técnica, Adobe Commerce | En el caso de las tiendas Adobe Commerce, compara los datos de catálogo completos con los datos a los que los agentes de IA pueden acceder en cada página de detalles del producto; muestra los PDP en los que faltan variantes, especificaciones, atributos y campos de catálogo relacionados en el HTML visible del agente, priorizados por el tráfico auténtico. | Destaca la información de catálogo recuperable que falta en la vista del agente y por qué importa para la detección de productos basada en LLM; implemente con Optimizar en Edge para ofrecer una instantánea de HTML totalmente procesada previamente y compatible con IA al tráfico auténtico en el perímetro de CDN, de modo que los agentes reciban un contexto de producto enriquecido de su catálogo sin CMS ni cambios de catálogo. |

## Optimización automática {#auto-optimization}

La optimización automática implementa las optimizaciones recomendadas con un solo clic, esto reduce el esfuerzo manual y el tiempo necesario para obtener los valores. Las optimizaciones se pueden aplicar en la fuente de contenido o en el perímetro de CDN. La optimización automática basada en Edge está disponible actualmente en Acceso anticipado para las oportunidades seleccionadas. Para obtener más información, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

<!--
### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.
-->

### Herramientas adicionales

El [comprobador de visibilidad LLM](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) es una extensión de Chrome que le permite ver exactamente a qué parte del contenido de su página web pueden acceder los LLM y también lo que permanece oculto. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración. Con un solo clic, los usuarios pueden evaluar la legibilidad automática de cualquier sitio y ver una comparación en paralelo de lo que ven los agentes de IA frente a lo que ven los usuarios humanos. Además, calcula cuánto contenido se puede recuperar mediante LLM Optimizer.

<!--
| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |
-->
