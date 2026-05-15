---
title: Agregar resúmenes compatibles con LLM
description: Descubra cómo LLM Optimizer identifica las páginas de alto tráfico que carecen de resúmenes concisos y puntos clave para los agentes de IA, y cómo revisarlas e implementarlas con Optimizar en Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:27:51.631Z'
TQID: 'https://experienceleague.adobe.com/QpBdx3B-qg41ZWtPU2R4CNq-POrSs31UIb0kms1H3GU'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 793
ht-degree: 0%

---


# Agregar resúmenes compatibles con LLM

La oportunidad de Agregar resúmenes favorables para LLM identifica páginas de alto tráfico que carecen de resúmenes estructurados concisos, lo que dificulta que los agentes de IA entiendan rápidamente la información clave de la página. Presenta resúmenes claros y puntos clave basados en el contenido de la página existente. Esto ayuda a los agentes a interpretar y capturar las reclamaciones de marcas importantes de forma más eficiente y aumenta la probabilidad de que el contenido se incluya con precisión en las respuestas de IA.

Para cada URL afectada, puede revisar las sugerencias generadas por IA e implementarlas con [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico auténtico sea más claro y pueda analizarse en el contexto sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Enriquece la página con resúmenes o puntos clave en la HTML que recuperan.
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer identifica páginas de alto tráfico donde los **resúmenes** y **puntos clave** de nivel de sección o página ayudarían a la comprensión de IA. Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la ficha **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada recomendación.

![URL con sugerencias sobre sugerencias actuales, fila expandida con sugerencias de resumen de página y sección](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

La tabla **URL con sugerencias** enumera páginas donde los resúmenes podrían ayudar a realizar un descubrimiento auténtico. Las sugerencias están organizadas en **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**. Para cada URL puede:

- **Expanda la fila** para ver el análisis y el texto de resumen propuesto (y los puntos clave cuando se incluyan).
- **Vista previa** de la comparación antes y después para el tráfico auténtico.
- **Marcar como fijo** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Cada entrada expandida muestra instrucciones de resumen a nivel de página y de sección, **copia generada por IA**, controles de edición y contexto asociados a la página activa.

Haga clic en **Vista previa** en la columna **Acciones** para abrir la vista previa de optimización. Compara el aspecto actual de la página en cuanto a tráfico real con la vista posterior a la optimización (por ejemplo, el contenido insertado de **resumen** y **punto clave** alineado con las ubicaciones sugeridas). Puede abrir o cerrar esa vista previa en cualquier momento antes de realizar la implementación.

Cuando esté listo para publicar, seleccione el resumen y los elementos de línea de puntos clave mediante las casillas de verificación. El pie de página muestra cuántos están seleccionados y proporciona **Marcar como fijos**, **Ignorar sugerencias** y **Implementar optimizaciones**.

![Sugerencias actuales con elementos de línea de resumen seleccionados e Implementar optimizaciones en el pie de página](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

### Implementación de la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL y los detalles de optimización seleccionados. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

![Implementar en el cuadro de diálogo de Edge](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron y observa que los agentes de IA pueden tardar algún tiempo en indexar la actualización. Cierre el cuadro de diálogo y abra **Sugerencias fijas** para comprobar el estado.

![Confirmación de implementación completa](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>La implementación de optimizaciones requiere completar el proceso de incorporación de Optimizar en Edge. Si aún no se ha incorporado, al hacer clic en **Implementar optimizaciones**, se le dirigirá al proceso de incorporación. Para obtener información detallada sobre cómo funciona Optimizar en Edge, los proveedores de CDN admitidos y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias fijas y Ver en directo

En **Sugerencias fijas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar la copia de resumen implementada y las instrucciones.

![Se corrigió la ficha Sugerencias con estado Optimizado, resúmenes implementados expandidos, Ver activo y Detalles](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

Haga clic en **Ver en directo** en la fila para abrir una vista de solo lectura del **contenido de la página actual** que se ha servido para la verificación (incluidos los bloques de **resumen** y **punto clave** insertados donde se aplican). Use **Detalles** para el análisis. Cuando necesite revertir los cambios de borde de forma masiva, seleccione las filas optimizadas mediante las casillas de verificación y, a continuación, utilice **Rollback** en el encabezado.

![Sugerencias fijas con casillas de verificación para la selección masiva antes de la reversión](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Reversión

Si cambia de opinión, puede revertir cualquier optimización implementada. En la vista **Sugerencias fijas**, seleccione las filas optimizadas que desee revertir y, a continuación, haga clic en **Deshacer** en el encabezado.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán, con una breve advertencia de que se revertirán las optimizaciones implementadas. Confirme la lista y haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## Probar en la demostración

Explore el flujo de trabajo Agregar resúmenes aptos para LLM en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
