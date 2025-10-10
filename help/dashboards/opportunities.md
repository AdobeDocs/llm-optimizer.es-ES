---
title: Oportunidades de optimización
description: Esta es la descripción general del artículo.
source-git-commit: 77bddfa7351d573c20a0f68a08b69000bc06beb8
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Oportunidades de optimización

Las oportunidades de optimización se detectan automáticamente con perspectivas que muestran dónde se puede mejorar el sitio y la presencia externa para aumentar la visibilidad de la marca en la búsqueda de IA. Estas optimizaciones incluyen correcciones en la página (adición de contenido estructurado, canónicos o resúmenes), ajustes técnicos (desbloqueo de rastreadores de IA o resolución de errores) e influencia en el contenido en sitios autoritativos de terceros. Abordar estas oportunidades de optimización ayuda a que su marca se represente con precisión y tenga más probabilidades de citarse en respuestas generativas.

![Oportunidades de optimización](/help/dashboards/assets/oport.png)

## Tablero de oportunidades

Las oportunidades de optimización presentadas en el tablero se priorizan en función de las brechas del reproductor, los temas de tendencia y los datos de rendimiento, y se presentan como una lista. Puede buscar una oportunidad específica utilizando el campo de búsqueda. Además, las oportunidades se agrupan por etiquetas y puede hacer clic directamente en una etiqueta para mostrar todas las oportunidades agrupadas bajo esa etiqueta.

Al hacer clic en **Detalles**, se abrirá una ventana independiente donde se proporciona más información y sugerencias adicionales.

## Oportunidades compatibles

A continuación se muestra una tabla de las oportunidades que admite actualmente:

| Oportunidad | Tipo | Problemas identificados | Corrección de sugerencias |
|---------|----------|----------|----------|
| Resumir párrafos largos | Contenido (in situ) | Detecta párrafos que exceden los umbrales de longitud recomendados. Muestra las direcciones URL afectadas y los fragmentos de texto de gran tamaño. | Cree resúmenes o divida texto largo en secciones más cortas y analizables. |
| Recomendar contenido estructurado (preguntas frecuentes) | Contenido (in situ) | Detecta mensajes de alta popularidad sin entradas de preguntas más frecuentes coincidentes. Muestra avisos relacionados, categorías y direcciones URL afectadas. | Añada bloques de esquema de preguntas frecuentes con respuestas concisas para hacer coincidir consultas comunes. |
| Detectar Hreflang Que Falta | Contenido (in situ) | Indica las páginas que carecen de atributos hreflang. Proporciona las direcciones URL afectadas y la cobertura esperada por idioma o región. | Implemente etiquetas hreflang para indicar las versiones localizadas correctas. |
| Detectar canónicos faltantes | Contenido (in situ) | Detecta párrafos que exceden los umbrales de longitud recomendados. Muestra las direcciones URL afectadas y los fragmentos de texto de gran tamaño. | Cree resúmenes o divida texto largo en secciones más cortas y analizables. |
| Detectar encabezados vacíos | Contenido (in situ) | Indica las páginas donde existen etiquetas de encabezado pero que no contienen texto. Muestra la dirección URL y la ubicación de las etiquetas vacías. | Agregue texto descriptivo a los encabezados que reflejen el contenido debajo de ellos. |
| Detectar encabezados duplicados | Contenido (in situ) | Analiza las etiquetas de encabezados de HTML y marca los encabezados repetidos. Muestra las direcciones URL afectadas y los fragmentos de texto duplicados. | Modificar encabezados para que sean únicos y mantener la jerarquía (H1 → H2 → H3). Combinar o cambiar el nombre de las secciones duplicadas. |
| Detectar tráfico agéntico bloqueado | GEO técnico | Analiza los registros de CDN para las solicitudes bloqueadas de agentes de IA conocidos (por ejemplo, GPTBot, PerplexityBot). Informa de las direcciones URL y los agentes afectados. | Actualice robots.txt o las configuraciones del servidor para permitir el acceso a los rastreadores de IA admitidos cuando corresponda. |
| Detectar problemas de 404s / 403s / 5xx | GEO técnico | Supervisa los registros de CDN para ver si hay respuestas de error. Frecuencia de informes, direcciones URL afectadas y visitas estimadas perdidas. | Corrija los vínculos rotos, actualice los permisos y resuelva los problemas del lado del servidor para que el contenido clave devuelva 200 respuestas. |
