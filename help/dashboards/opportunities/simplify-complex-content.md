---
title: Simplificar contenido complejo
description: Descubra cómo LLM Optimizer identifica las páginas de alto tráfico con copia densa que es difícil de interpretar para los agentes de IA, y cómo revisar e implementar texto simplificado con Optimizar en Edge.
feature: Opportunities
autotag-review: '2026-07-15T18:04:55.581Z'
TQID: 'https://experienceleague.adobe.com/uMK9qeAGMNrtvR0TYbeg8SIOKlwKf4L5NIE9ZgsJaUw'
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
workflow-type: ht
source-wordcount: 776
ht-degree: 100%

---


# Simplificar contenido complejo

La oportunidad de Simplificar contenido complejo identifica páginas de alto tráfico donde el texto es denso o complejo, lo que dificulta que los agentes de IA interpreten la información clave.Introduce versiones más claras y fáciles de escanear de la copia existente preservando al mismo tiempo el significado original.Esto ayuda a los agentes a analizar, resumir y extraer información importante y de forma más fiable.

Para cada URL afectada, puede revisar **sugerencias de texto mejorado**, compararlas con **vista previa** e implementarlas con [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico agéntico reciba una HTML más clara sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Actualiza la página visible del agente para que los pasajes complejos se reemplacen o aumenten con **Texto mejorado** alineado con la página activa.
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer identifica las páginas que reciben un tráfico agéntico alto y cuyo contenido se clasifica por debajo de los umbrales de legibilidad y sugiere que se vuelva a escribir la copia. Para cada página tiene:

**Texto mejorado**: contenido simplificado basado en lo que ya está en la página.
**Vista previa**: un antes y un después de la comparación para el tráfico agéntico.

Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la ficha **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada recomendación.

![URL con sugerencias sobre sugerencias actuales, fila expandida con texto mejorado y vista previa](/help/dashboards/opportunities/assets/simplify-complex-content-expand.png)

La tabla **URL con sugerencias** enumera páginas donde el contenido simplificado ayudaría a una comprensión agéntica. Las sugerencias se organizan en: **Sugerencias actuales**, **Sugerencias corregidas** y **Sugerencias ignoradas**. En cada URL puede hacer lo siguiente:

- **Expanda la fila** para ver **sugerencias de texto mejorado** para esa página.
- **Vista previa** de la comparación antes y después del tráfico agéntico.
- **Marcar como fijo** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Las **vistas** incluyen **Sugerencias actuales**,**Sugerencias corregidas** (estado **Optimizado** al implementarse) y **Sugerencias ignoradas**. Puede verificar la implementación en vivo usando **Ver en vivo** en **Sugerencias fijas** y revertir en cualquier momento.

Seleccione las direcciones URL o los elementos de línea con **texto mejorado** que desee enviar mediante las casillas de verificación y, a continuación, utilice **Marcar como corregido**, **Ignorar sugerencias** o **Implementar optimizaciones** en el encabezado de **Plan de oportunidades**. La IU de demostración también muestra un recuento de selección y acciones relacionadas con la lista.

![Plan de oportunidades, Sugerencias actuales, fila expandida y Optimizaciones de implementación en el encabezado del plan](/help/dashboards/opportunities/assets/simplify-complex-content-select.png)

### Implementar la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL y los detalles de optimización seleccionados. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

![Cuadro de diálogo Implementar en Edge](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-dialog.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron y observa que los agentes de IA pueden tardar algún tiempo en indexar la actualización. Cierre el cuadro de diálogo y abra **Sugerencias corregidas** para comprobar el estado.

![Confirmación de implementación completada](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-confirm.png)

>[!NOTE]
>
>Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias corregidas y Ver en vivo

En **Sugerencias corregidas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar **Texto mejorado** e instrucciones implementadas.

![Pestaña Sugerencias fijas con estado optimizado, copia simplificada expandida, Ver en vivo y Detalles](/help/dashboards/opportunities/assets/simplify-complex-content-fixed.png)

Haga clic en **Ver en vivo** en la fila para abrir una vista de solo lectura del **contenido de la página actual** que se ha usado para la verificación (incluidos los pasajes simplificados donde se aplicaron). Use **Detalles** para el análisis.

![Ver en vivo: contenido de la página actual que incluye texto simplificado para los agentes](/help/dashboards/opportunities/assets/simplify-complex-content-view-live.png)

Cuando necesite revertir los cambios en el borde de forma masiva, seleccione las filas optimizadas mediante las casillas de verificación y, a continuación, utilice **Reversión** en el encabezado.

![Sugerencias corregidas con la fila implementada expandida, Estado optimizado y Reversión en el encabezado](/help/dashboards/opportunities/assets/simplify-complex-content-rollback.png)

## Reversión

Si cambia de opinión, puede revertir cualquier optimización implementada. En la vista **Sugerencias corregidas**, seleccione las filas optimizadas que desee revertir y, a continuación, haga clic en **Deshacer** en el encabezado.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán, con una breve advertencia de que se revertirán las optimizaciones implementadas. Confirme la lista y haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-dialog.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-confirm.png)

## Probar en la demostración

Explore el flujo de trabajo Simplificar contenido complejo en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
