---
title: Agregar tabla de contenido
description: Descubra cómo LLM Optimizer identifica las páginas de alto tráfico que carecen de una estructura de navegación clara para los agentes de IA y cómo revisar e implementar una tabla de contenido con Optimizar en Edge.
feature: Opportunities
autotag-review: '2026-07-15T16:47:42.882Z'
TQID: 'https://experienceleague.adobe.com/x-7FiZKCLMmEfm1x2lQNtfOd4su1MyGLrcAtLnjpaqw'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2: id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 655
ht-degree: 9%

---


# Agregar tabla de contenido

>[!NOTE]
>
> **Acceso anticipado** — Esta capacidad está disponible en Acceso anticipado. La disponibilidad, la idoneidad y las partes del flujo de trabajo pueden cambiar a medida que la capacidad madura. Póngase en contacto con el equipo de su cuenta de Adobe si tiene alguna pregunta sobre el acceso.

La oportunidad Agregar tabla de contenido identifica páginas de alto tráfico que carecen de una **tabla de contenido** y una guía estructural claras, lo que dificulta que los agentes de IA analicen la página y asignen las consultas de usuario a las secciones correctas. Presenta una tabla de contenido estructurada con **encabezados vinculados por anclajes** que reflejan las secciones principales de la página. Esta estructura ayuda a los agentes a extraer, asignar y citar pasajes relevantes de forma más fiable.

Para cada URL afectada, puede revisar las entradas sugeridas de la Tabla de contenido e implementarlas con [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico real reciba un contexto de navegación más claro sin que se requieran cambios en el Sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Agrega una tabla de contenido a la página.
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer identifica páginas de alto tráfico donde una **Tabla de contenido** mejoraría la forma en que los agentes de IA navegan por encabezados y secciones. Para cada página, las sugerencias se basan en encabezados que ya se encuentran en la página, de modo que la Tabla de contenido refleje la estructura de la página.

Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la ficha **Sugerencias actuales**.

En **Sugerencias actuales**, para cada URL puede:

- **Expanda la fila** para inspeccionar la tabla de contenido propuesta (analizada a partir de encabezados de página y presentada como entradas con vínculos de anclaje).
- **Vista previa** a antes y después de la comparación.
- **Marcar como fijo** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Las sugerencias están organizadas en **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**, lo que concuerda con otras oportunidades de Optimizar en Edge.

### Implementar la optimización

Cuando esté listo para publicar en el perímetro de, seleccione las sugerencias de la tabla de contenido que desee implementar. El pie de página resume cuántos elementos se han seleccionado y, por lo general, ofrece **Marcar como fijos**, **Ignorar sugerencias** y **Implementar optimizaciones**.

Haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL y los detalles de optimización seleccionados. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron. Cierre el cuadro de diálogo y abra **Sugerencias fijas** para comprobar el estado.

>[!NOTE]
>
>Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias fijas y Ver en directo

En **Sugerencias fijas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar la tabla de contenido implementada, use **Detalles** para análisis donde esté disponible o haga clic en **Ver en directo** para abrir una vista de solo lectura del **contenido de la página actual** que se ha servido para la verificación (incluida la **tabla de contenido insertada**).

Cuando necesite revertir los cambios de borde de forma masiva, seleccione las filas optimizadas mediante las casillas de verificación y, a continuación, utilice **Rollback** en el encabezado.

## Reversión

Si cambia de opinión, puede revertir una optimización implementada. En la vista **Sugerencias fijas**, seleccione las filas optimizadas que desee revertir y, a continuación, haga clic en **Deshacer** en el encabezado.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán, con una breve advertencia de que se revertirán las optimizaciones implementadas. Confirme la lista y haga clic en **Reversión** o **Cancelar**.

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.
