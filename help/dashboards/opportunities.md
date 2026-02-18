---
title: Oportunidades de optimización
description: Aprenda a utilizar el panel de control de oportunidades para detectar automáticamente cómo se puede mejorar el sitio a fin de aumentar la visibilidad de la marca.
feature: Opportunities
source-git-commit: 1f665bd14349c15d92f8274742606abcf9b02000
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 100%

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
| Recomendar contenido estructurado (preguntas frecuentes) | Contenido (en el sitio) | Detecta indicaciones de alta popularidad sin entradas de preguntas frecuentes coincidentes. Muestra indicaciones relacionadas, categorías y direcciones URL afectadas. | Añada bloques de esquemas de preguntas frecuentes con respuestas concisas para que se ajusten a las consultas comunes. |
| Detectar atributos hreflang que faltan | Contenido (en el sitio) | Indica las páginas que carecen de atributos hreflang. Proporciona las direcciones URL afectadas y la cobertura prevista por idioma o región. | Implemente etiquetas hreflang para indicar las versiones localizadas correctas. |
| Detectar etiquetas canónicas que faltan | Contenido (en el sitio) | Busca páginas sin etiquetas canónicas o con etiquetas en conflicto. Muestra las direcciones URL afectadas y las duplicados. | Añada etiquetas canónicas que apunten a la versión preferida de cada página. Garantice un uso coherente entre las variantes. |
| Detectar tráfico agéntico bloqueado | Optimización técnica del motor generativo | Analiza los registros de CDN en busca de solicitudes bloqueadas de agentes de IA conocidos (por ejemplo, GPTBot, PerplexityBot). Informa de las direcciones URL y los agentes afectados. | Actualice robots.txt o las configuraciones del servidor para permitir el acceso a los rastreadores de IA admitidos, según corresponda. |
| Detectar problemas 404s / 403s / 5xx | Optimización técnica del motor generativo | Supervisa los registros de CDN para ver si hay respuestas de error. Frecuencia de informes, direcciones URL afectadas y visitas estimadas perdidas. | Corrija los vínculos rotos, actualice los permisos y resuelva los problemas del lado del servidor para que el contenido clave devuelva 200 respuestas. |
| Recuperar visibilidad del contenido (acceso anticipado) | Optimización técnica del motor generativo | Indica las páginas donde se oculta contenido crítico para los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Preprocese las páginas para que los agentes de IA puedan disponer de más contenido sin ejecutar JavaScript. |

## Optimización automática {#auto-optimization}

La optimización automática implementa las optimizaciones recomendadas con un solo clic, esto reduce el esfuerzo manual y el tiempo necesario para obtener los valores. Las optimizaciones se pueden aplicar en la fuente de contenido o en el perímetro de CDN. La optimización automática basada en Edge está disponible actualmente en Acceso anticipado para las oportunidades seleccionadas. Para obtener más información, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge.md).

<!--### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.-->

### Herramientas adicionales

El [comprobador de visibilidad LLM](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) es una extensión de Chrome que le permite ver exactamente a qué parte del contenido de su página web pueden acceder los LLM y también lo que permanece oculto. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración. Con un solo clic, los usuarios pueden evaluar la legibilidad automática de cualquier sitio y ver una comparación en paralelo de lo que ven los agentes de IA frente a lo que ven los usuarios humanos. Además, calcula cuánto contenido se puede recuperar mediante LLM Optimizer.
