---
title: Añadir resúmenes de transcripciones multimedia
description: Descubra cómo LLM Optimizer identifica las páginas en las que la información clave está incrustada en vídeo sin texto legible por máquina, y cómo revisar e implementar los resúmenes de transcripciones generados por IA con Optimize en Edge.
feature: Opportunities
autotag-review: '2026-07-15T16:47:13.112Z'
TQID: 'https://experienceleague.adobe.com/lsMTVS4cFaGnhZonULQE4MB31bMdkzxoKA62o4IBcz0'
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: ht
source-wordcount: 769
ht-degree: 100%

---


# Añadir resúmenes de transcripciones multimedia

>[!NOTE]
>
> **Acceso anticipado**: añadir resúmenes de transcripciones multimedia está disponible en Acceso anticipado.La disponibilidad, la idoneidad y las partes del flujo de trabajo pueden cambiar a medida que la capacidad va madurando.Póngase en contacto con su equipo de cuentas de Adobe si tiene alguna pregunta sobre el acceso.

La oportunidad de añadir resúmenes de transcripciones multimedia identifica las páginas en las que vive información importante en vídeo u otros medios sin transcripciones ni resúmenes de texto cortos que los agentes de inteligencia artificial puedan leer. Presenta **resúmenes de transcripciones generados por IA** basados en los medios y el contexto de la página adyacente. Ayuda a recuperar información clave de marca que, de lo contrario, se perdería si los agentes de IA comprendieran el contenido multimedia.

Para cada URL afectada, puede revisar los detalles propuestos de **Parche de contenido**, **Implementación** (por ejemplo, el selector y la operación de CSS de destino) y **Motivación**, y luego implementarlos con [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md) para que el tráfico agéntico reciba la HTML enriquecida sin que se requieran cambios en el sistema de administración de contenido (CMS).

## Cómo soluciona el problema

Las correcciones se aplican usando [Optimize en Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Ofrece una instantánea de HTML procesada previamente a los agentes de IA.
- Enriquece la página con el texto de resumen de la transcripción en la HTML que recuperan (por ejemplo, cerca del vídeo en línea relevante).
- Funciona en la capa CDN (sin cambios en CMS).
- Es solo IA, sin impacto en visitantes humanos ni bots SEO.
- Se implementa en minutos y es **totalmente reversible** desde la interfaz de LLM Optimizer.

## Funcionamiento

LLM Optimizer marca páginas de alto tráfico en las que falta texto legible por el equipo para los medios incrustados, según la configuración y la estructura de la página. Las direcciones URL afectadas aparecen en la tabla **direcciones URL con sugerencias** de la pestaña **Sugerencias actuales**, donde puede expandir una fila para inspeccionar cada **parche de contenido**, cómo se aplicará y por qué se recomienda.

En cada página, tiene:

**Resumen multimedia**: resúmenes estructurados derivados del contenido de vídeo.
**Vista previa** antes y después de la comparación de páginas.

![URL con sugerencias sobre sugerencias actuales, fila expandida con parche de contenido, detalles de implementación y motivación](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-expand.png)

La tabla **URL con sugerencias** enumera páginas donde el texto de transcripción o resumen ayudaría a realizar un descubrimiento agéntico. Las sugerencias se organizan en **Sugerencias actuales**,**Sugerencias corregidas** y **Sugerencias ignoradas**. En cada URL puede hacer lo siguiente:

- **Expanda la fila** para ver el texto de **Parche de contenido**, los detalles de **Implementación** (incluida la operación DOM y el selector CSS planeados) y la **Motivación** para el cambio.
- **Vista previa** de la comparación antes y después del tráfico agéntico.
- **Marcar como corregido** si se dirigió a la oportunidad fuera de LLM Optimizer.
- **Ignorar** sugerencias que no sean relevantes.

Puede editar el texto del parche desde la fila cuando sea compatible (control de lápiz) y, a continuación, utilizar las casillas de verificación de fila para seleccionar lo que desea implementar. El pie de página muestra cuántos están seleccionados y permite **Marcar como corregido**, **Ignorar sugerencias** e **Implementar optimizaciones**.

### Implementar la optimización

Cuando esté listo para publicar en Edge, haga clic en **Implementar optimizaciones**. Un cuadro de diálogo **Implementar en Edge** enumera las direcciones URL, los selectores y las operaciones que está a punto de ejecutar. Revise la lista y, a continuación, elija **Implementar** o **Cancelar**.

![Implementar en el cuadro de diálogo de Edge para parches de contenido de resumen de transcripciones multimedia](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-dialog.png)

Después de una implementación correcta, **Implementación completada** confirma cuántas optimizaciones se activaron. Cierre el cuadro de diálogo y abra **Sugerencias corregidas** para comprobar el estado.

![Confirmación de implementación completada](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-confirm.png)

>[!NOTE]
>
> Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugerencias corregidas y Ver en vivo

En **Sugerencias corregidas**, las direcciones URL implementadas muestran **Optimizado** en la columna de estado. Expanda una fila para revisar el **parche de contenido** en vivo, los detalles de la **implementación** y la **motivación** . Además, puede usar **Detalles** para análisis o **Ver en vivo** donde esté disponible para confirmar qué tráfico agéntico recibe.

![Sugerencias corregidas con estado optimizado, parche de contenido expandido y reversión](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-fixed.png)

Para revertir de forma masiva, seleccione las filas optimizadas mediante las casillas de verificación y, a continuación, use **Reversión** en el encabezado.

![Sugerencias corregidas con filas seleccionadas antes de la reversión](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-select-in-fixed.png)

## Reversión

Si cambia de opinión, puede revertir una optimización implementada. En **Sugerencias corregidas**, seleccione las filas que desea revertir y haga clic en **Deshacer**.

El cuadro de diálogo **Reversión** enumera las sugerencias que se revertirán y advierte que las optimizaciones implementadas se eliminarán de la ruta de acceso activa del tráfico agéntico. Confirme y luego haga clic en **Reversión** o **Cancelar**.

![Sugerencias de cuadro de diálogo de reversión para revertir](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-dialog.png)

Cuando finalice la operación, aparecerá un resumen de **Se ha revertido correctamente**; ciérrelo para volver al panel.

![Reversión completada: revertida correctamente](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-confirm.png)

## Probar en la demostración

Explore el flujo de trabajo Añadir resúmenes de transcripciones multimedia en la [demostración de Frescopa](https://play.llmo.now/org/demo-org).
