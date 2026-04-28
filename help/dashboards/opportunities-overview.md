---
title: Oportunidades de optimización
description: Aprenda a utilizar el panel de control de oportunidades para detectar automáticamente cómo se puede mejorar el sitio a fin de aumentar la visibilidad de la marca.
feature: Opportunities
source-git-commit: 34e90bc95aa1d2ffabe8fd06c2c548491dd5c5b7
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 58%

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
| Resumir párrafos largos | Contenido (en el sitio) | Detecta párrafos que exceden los umbrales de longitud recomendados. Muestra las direcciones URL afectadas y los fragmentos de texto de gran tamaño. | Cree resúmenes o divida texto largo en secciones más cortas y fáciles de escanear. |
| Recomendar contenido estructurado | Contenido (en el sitio) | Detecta indicaciones de alta popularidad sin entradas de preguntas frecuentes coincidentes. Muestra indicaciones relacionadas, categorías y direcciones URL afectadas. | Añada bloques de esquemas de preguntas frecuentes con respuestas concisas para que se ajusten a las consultas comunes. |
| [Tráfico bloqueado por robots.txt](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | Optimización técnica del motor generativo | Analiza el archivo robots.txt en busca de reglas que bloqueen selectivamente a los agentes de IA de contenido que, de lo contrario, sería accesible públicamente. Informa de las direcciones URL afectadas y los agentes bloqueados. | Actualice el archivo robots.txt para permitir el acceso a los rastreadores de IA admitidos donde corresponda. |
| [Errores de tráfico de agente](/help/dashboards/opportunities/agentic-traffic-errors.md) | Optimización técnica del motor generativo | Supervisa los registros de CDN para las respuestas de error 404, 403 y 5xx devueltas a los agentes de IA. Informa de las direcciones URL afectadas y el total de visitas perdidas. | Corrija los vínculos rotos, actualice los permisos y resuelva los problemas del lado del servidor para que el contenido clave devuelva 200 respuestas. |
| Simplificar contenido complejo | Contenido (en el sitio) | Identifica párrafos largos y complejos que superan los umbrales de legibilidad y que pueden reducir la comprensión de IA. | Preprocese las páginas para que los agentes de IA puedan disponer de más contenido sin ejecutar JavaScript. |
| [Recuperar Visibilidad del contenido](/help/dashboards/opportunities/recover-content-visibility.md) | Optimización técnica del motor generativo | Indica las páginas donde se oculta contenido crítico para los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Preprocese las páginas en la capa de CDN mediante Optimizar en Edge para que los agentes de IA puedan acceder a más contenido sin ejecutar JavaScript. |
| [Análisis de Wikipedia](/help/dashboards/opportunities/wikipedia-analysis.md) | Fuera del sitio | Analiza la página de Wikipedia de su empresa en relación con los competidores del sector en cuanto a referencias, secciones, duración del contenido, imágenes e integridad del cuadro de información. Identifica lagunas específicas en las que la página no alcanza los valores de referencia del sector. | Revise las recomendaciones estratégicas generadas por IA para mejorar su presencia en Wikipedia, incluyendo la adición de referencias, el enriquecimiento de su infobox, la expansión de secciones y la mejora de la calidad del artículo. |
| [Análisis de Opinión de YouTube (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza los vídeos de YouTube citados para el conjunto de mensajes de Presencia de marca en menciones de la marca, opinión, cuota de voz y temas recurrentes. Solo aparece cuando los vídeos de YouTube se detectan como citas para el conjunto de mensajes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en todo el contenido de YouTube, incluidas las acciones sugeridas y los equipos responsables de implementarlas. |
| [Análisis de Opinión de Reddit (Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza los hilos de Reddit citados para el conjunto de mensajes de Presencia de marca para menciones de la marca, opinión, cuota de voz y temas recurrentes. Solo aparece cuando los hilos de Reddit se detectan como citas para el conjunto de mensajes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en todo el contenido de Reddit, incluidas las acciones sugeridas y los equipos responsables de implementarlas. |
| [Análisis de Opinión citado (Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | Fuera del sitio, medios sociales y comunidad | Analiza las direcciones URL más citadas detectadas para los mensajes de Presencia de marca establecidos para menciones de la marca, opinión, cuota de voz y temas recurrentes. | Revise las recomendaciones priorizadas para mejorar la percepción de la marca en las páginas que más citan los sistemas de IA al responder a las preguntas sobre su marca. |

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
