---
title: Añadir preguntas frecuentes relevantes
description: Descubra cómo LLM Optimizer identifica las páginas de alto tráfico que carecen de contenido de preguntas y respuestas estructurado para los agentes de IA y cómo revisar e implementar las preguntas frecuentes generadas por IA con Optimizar en Edge.
feature: Opportunities
autotag-review: '2026-07-15T16:47:24.291Z'
TQID: 'https://experienceleague.adobe.com/ObmJKEvR9-ovzugCtAsRkcUBemcsMw6cNwizkuKYPcc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2:
  - id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 742
ht-degree: 10%

---


# Añadir preguntas frecuentes relevantes

La oportunidad Añadir preguntas más frecuentes relevantes identifica páginas de alto tráfico que carecen de contenido estructurado de preguntas y respuestas, en el que los agentes de inteligencia artificial suelen confiar al generar respuestas. Presenta contenido relevante **alineado por intención de preguntas frecuentes** basado en el material de la página existente. Esto ayuda a los agentes a relacionar las preguntas del usuario con el contenido de forma más directa.

Para cada URL afectada, puede revisar las sugerencias de preguntas frecuentes generadas por IA e implementarlas con [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico auténtico reciba un contexto de preguntas y respuestas más claro sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Enriquece la página con contenido de preguntas más frecuentes en la HTML que recuperan.
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer identifica páginas de alto tráfico en las que el contenido de preguntas y respuestas falta o es delgado, según el conjunto de mensajes de su marca. Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la ficha **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada recomendación.

![URL con sugerencias sobre sugerencias actuales, fila expandida con preguntas frecuentes y respuestas generadas por IA](/help/dashboards/opportunities/assets/add-relevant-faqs-expand.png)

La tabla **URL con sugerencias** enumera páginas donde las preguntas frecuentes ayudarían a realizar descubrimientos controlados por IA. Las sugerencias están organizadas en **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**. En cada URL puede hacer lo siguiente:

- **Expanda la fila** para ver el contenido de preguntas más frecuentes propuesto para esa página.
- **Vista previa** de la comparación antes y después para el tráfico auténtico.
- **Marcar como fijo** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Cada entrada expandida enumera las preguntas frecuentes **prompt**, **respuestas sugeridas generadas por IA**, **razonamiento** y **fuentes** ligadas a la página. La tabla también muestra cuántas preguntas frecuentes se sugieren por URL y **tráfico de agente (4 semanas)** para ayudarle a priorizar.

Haga clic en **Vista previa** en una fila para abrir la vista previa de optimización. Compara el aspecto actual de tu página en cuanto a tráfico real con la vista posterior a la optimización (por ejemplo, el nuevo bloque **FAQs**).

![Vista previa de optimizaciones que comparan la vista del agente actual con la vista posterior a la optimización con las preguntas frecuentes](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-01.png)

Seleccione las sugerencias de preguntas frecuentes que desee enviar mediante las casillas de verificación de fila. El pie de página muestra cuántos están seleccionados y proporciona **Marcar como fijos**, **Ignorar sugerencias** y **Implementar optimizaciones**.

![Sugerencias de preguntas frecuentes seleccionadas sobre sugerencias actuales con la implementación de optimizaciones](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-02.png)

### Implementar la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL, preguntas y respuestas que está a punto de insertar. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

Cuadro de diálogo ![Implementar en Edge](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-03.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron. Cierre el cuadro de diálogo y abra **Sugerencias fijas** para comprobar el estado.

![Confirmación de implementación completa](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-04.png)

>[!NOTE]
>
>Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias fijas y Ver en directo

En **Sugerencias fijas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar el contenido de las preguntas más frecuentes en directo, use **Detalles** para análisis o haga clic en **Ver en directo** para abrir una vista de solo lectura del **contenido de la página actual** que se ha servido para la verificación (incluida la sección **Preguntas más frecuentes** insertada).

![Sugerencias fijas con estado optimizado, Ver activo y Revertir](/help/dashboards/opportunities/assets/add-relevant-faqs-fixed.png)

La ventana **Ver en vivo** muestra la estructura de la página y la copia de las preguntas frecuentes tal como se presentan en esa comprobación.

![Ver en directo: contenido de la página actual, incluidas las preguntas frecuentes](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-05.png)

## Reversión

Si cambia de opinión, puede revertir cualquier optimización implementada. En la vista **Sugerencias fijas**, puede seleccionar las filas optimizadas que desea revertir y, a continuación, hacer clic en **Deshacer** en el encabezado.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán, con una breve advertencia de que se revertirán las optimizaciones implementadas. Confirme la lista y haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-07.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-08.png)

## Probar en la demostración

Explore el flujo de trabajo Agregar preguntas más frecuentes relevantes en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
