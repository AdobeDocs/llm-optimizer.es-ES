---
title: Agregar resúmenes de transcripciones multimedia
description: Descubra cómo LLM Optimizer identifica las páginas en las que la información clave está incrustada en vídeo sin texto legible por máquina, y cómo revisar e implementar los resúmenes de transcripciones generados por IA con Optimizar en Edge.
feature: Opportunities
source-git-commit: 36a6836f86b6d31cc4bf4682e881bd127edf66e4
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# Agregar resúmenes de transcripciones multimedia

>[!NOTE]
>
> **Acceso anticipado** — Agregar resúmenes de transcripciones multimedia está disponible en Acceso anticipado. La disponibilidad, la idoneidad y las partes del flujo de trabajo pueden cambiar a medida que la capacidad madura. Póngase en contacto con el equipo de su cuenta de Adobe si tiene alguna pregunta sobre el acceso.

La oportunidad de añadir resúmenes de transcripciones multimedia identifica las páginas en las que vive información importante en vídeo u otros medios sin transcripciones ni resúmenes de texto cortos que los agentes de inteligencia artificial puedan leer. Presenta **resúmenes de transcripciones generados por IA** basados en los medios y el contexto de la página adyacente. Ayuda a recuperar información clave de marca que, de lo contrario, se perdería si los agentes de IA comprendieran el contenido multimedia.

Para cada URL afectada, puede revisar los detalles propuestos de **Parche de contenido**, **Implementación** (por ejemplo, el selector y la operación de CSS de destino) y **Motivación**, y luego implementarlos con [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico auténtico reciba la HTML enriquecida sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Enriquece la página con el texto de resumen de la transcripción en la HTML que recuperan (por ejemplo, cerca del vídeo en línea relevante).
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer marca páginas de alto tráfico en las que falta texto legible por el equipo para los medios incrustados, según la configuración y la estructura de la página. Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la pestaña **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada **parche de contenido**, cómo se aplicará y por qué se recomienda.

Para cada página, tiene:

**Resumen multimedia**: resúmenes estructurados derivados del contenido de vídeo.
**Vista previa** - Antes y después de la comparación de páginas.

![URL con sugerencias sobre sugerencias actuales, fila expandida con parche de contenido, detalles de implementación y justificación](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-expand.png)

La tabla **URL con sugerencias** enumera páginas donde el texto de transcripción o resumen ayudaría a realizar un descubrimiento auténtico. Las sugerencias están organizadas en **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**. Para cada URL puede:

- **Expanda la fila** para ver el texto de **Parche de contenido**, los detalles de **Implementación** (incluida la operación DOM y el selector CSS planeados) y **Motivo** para el cambio.
- **Vista previa** de la comparación antes y después para el tráfico auténtico.
- **Marcar como fijo** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Puede editar el texto del parche desde la fila cuando sea compatible (control de lápiz) y, a continuación, utilizar las casillas de verificación de fila para seleccionar lo que desea implementar. El pie de página muestra cuántos están seleccionados y proporciona **Marcar como fijos**, **Ignorar sugerencias** y **Implementar optimizaciones**.

### Implementación de la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL, los selectores y las operaciones que está a punto de ejecutar. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

![Implementar en el cuadro de diálogo de Edge para parches de contenido de resumen de transcripciones multimedia](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-dialog.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron. Cierre el cuadro de diálogo y abra **Sugerencias fijas** para comprobar el estado.

![Confirmación de implementación completa](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-confirm.png)

>[!NOTE]
>
> La implementación de optimizaciones requiere completar el proceso de incorporación de Optimizar en Edge. Si aún no se ha incorporado, al hacer clic en **Implementar optimizaciones**, se le dirigirá al proceso de incorporación. Para obtener información detallada sobre cómo funciona Optimizar en Edge, los proveedores de CDN admitidos y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias fijas y Ver en directo

En **Sugerencias fijas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar el **parche de contenido** activo, los detalles de la **implementación** y la **justificación** . Además, puedes usar **Detalles** para análisis o **Ver en vivo** donde esté disponible para confirmar qué tráfico auténtico recibe.

![Sugerencias fijas con estado optimizado, parche de contenido expandido y reversión](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-fixed.png)

Para revertir de forma masiva, selecciona las filas optimizadas mediante las casillas de verificación y, a continuación, usa **Reversión** en el encabezado.

![Sugerencias fijas con filas seleccionadas antes de la reversión](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-select-in-fixed.png)

## Reversión

Si cambia de opinión, puede revertir una optimización implementada. En **Sugerencias fijas**, seleccione las filas que desea revertir y haga clic en **Deshacer**.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán y advierte que las optimizaciones implementadas se eliminarán de la ruta de acceso activa para el tráfico auténtico. Confirme y luego haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-dialog.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-confirm.png)

## Probar en la demostración

Explore el flujo de trabajo Agregar resúmenes de transcripciones multimedia en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
