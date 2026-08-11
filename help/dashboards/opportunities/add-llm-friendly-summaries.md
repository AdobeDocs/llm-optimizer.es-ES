---
title: Añadir resúmenes compatibles con LLM
description: Descubra cómo LLM Optimizer identifica las páginas de alto tráfico que carecen de resúmenes concisos y puntos clave para los agentes de IA, y cómo revisarlas e implementarlas con Optimize en Edge.
feature: Opportunities
autotag-review: '2026-07-15T16:47:03.003Z'
TQID: 'https://experienceleague.adobe.com/InOzeT7WlDaACpB-WT0F-JqI1nopOJewihCP9eUQnNY'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2: id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: ht
source-wordcount: 793
ht-degree: 100%

---


# Añadir resúmenes compatibles con LLM

La oportunidad de Añadir resúmenes favorables para LLM identifica páginas de alto tráfico que carecen de resúmenes estructurados concisos, lo que dificulta que los agentes de IA entiendan rápidamente la información clave de la página.Presenta resúmenes claros y puntos clave basados en el contenido de la página existente.Esto ayuda a los agentes a interpretar y capturar las reclamaciones de marcas importantes de forma más eficiente y aumenta la probabilidad de que el contenido se incluya con precisión en las respuestas de IA.

Para cada URL afectada, puede revisar las sugerencias generadas por IA e implementarlas con [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico agéntico sea más claro y pueda analizarse en el contexto sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Enriquece la página con resúmenes o puntos clave en la HTML que recuperan.
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer identifica páginas de alto tráfico donde los **resúmenes** y **puntos clave** de nivel de sección o página ayudarían a la comprensión de IA. Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la ficha **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada recomendación.

![URL con sugerencias sobre sugerencias actuales, fila expandida con sugerencias de resumen de página y sección](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

La tabla **URL con sugerencias** enumera páginas donde los resúmenes podrían ayudar a realizar un descubrimiento agéntico. Las sugerencias se organizan en **Sugerencias actuales**,**Sugerencias corregidas** y **Sugerencias ignoradas**. En cada URL puede hacer lo siguiente:

- **Expanda la fila** para ver el análisis y el texto de resumen propuesto (y los puntos clave cuando se incluyan).
- **Vista previa** de la comparación antes y después del tráfico agéntico.
- **Marcar como corregido** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Cada entrada expandida muestra instrucciones de resumen a nivel de página y de sección, **copia generada por IA**, controles de edición y contexto asociados a la página activa.

Haga clic en **Vista previa** en la columna **Acciones** para abrir la vista previa de optimización. Compara el aspecto actual de la página en cuanto a tráfico agéntico con la vista posterior a la optimización (por ejemplo, el contenido insertado de **resumen** y **punto clave** alineado con las ubicaciones sugeridas). Puede abrir o cerrar esa vista previa en cualquier momento antes de realizar la implementación.

Cuando esté listo para publicar, seleccione el resumen y los elementos de línea de puntos clave mediante las casillas de verificación. El pie de página muestra cuántos están seleccionados y permite **Marcar como corregido**, **Ignorar sugerencias** e **Implementar optimizaciones**.

![Sugerencias actuales con elementos de línea de resumen seleccionados e Implementar optimizaciones en el pie de página](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

### Implementar la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL y los detalles de optimización seleccionados. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

![Cuadro de diálogo Implementar en Edge](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron y observa que los agentes de IA pueden tardar algún tiempo en indexar la actualización. Cierre el cuadro de diálogo y abra **Sugerencias corregidas** para comprobar el estado.

![Confirmación de implementación completada](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias corregidas y Ver en vivo

En **Sugerencias corregidas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar la copia de resumen implementada y las instrucciones.

![Se corrigió la ficha Sugerencias con estado Optimizado, resúmenes implementados expandidos, Ver en vivo y Detalles](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

Haga clic en **Ver en vivo** en la fila para abrir una vista de solo lectura del **contenido de la página actual** que se ha usado para la verificación (incluidos los bloques de **resumen** y **punto clave** insertados donde se aplican). Use **Detalles** para el análisis. Cuando necesite revertir los cambios de extremo de forma masiva, seleccione las filas optimizadas mediante las casillas de verificación y, a continuación, utilice **Reversión** en el encabezado.

![Sugerencias corregidas con casillas de verificación para la selección masiva antes de la reversión](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Reversión

Si cambia de opinión, puede revertir cualquier optimización implementada. En la vista **Sugerencias corregidas**, seleccione las filas optimizadas que desee revertir y, a continuación, haga clic en **Reversión** en el encabezado.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán, con una breve advertencia de que se revertirán las optimizaciones implementadas. Confirme la lista y haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## Probar en la demostración

Explore el flujo de trabajo Añadir resúmenes aptos para LLM en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
