---
title: Recuperar visibilidad del contenido
description: Aprenda cómo LLM Optimizer identifica las páginas donde el contenido crítico está oculto a los agentes de IA y cómo recuperar esa visibilidad mediante la optimización basada en el extremo.
feature: Opportunities
autotag-review: '2026-05-15T17:56:37.098Z'
TQID: 'https://experienceleague.adobe.com/rHqJL4RrJr1ghsy4fhXe-JLDrWruNSZgVhXQeRN-iyA'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 928
ht-degree: 100%

---


# Recuperar visibilidad del contenido

Los agentes de IA solo pueden citar contenido al que tienen acceso. Cuando el contenido clave de tus páginas está oculto tras la renderización del lado del cliente y las cargas dinámicas (como descripciones de productos, valoraciones de usuarios, recetas y comentarios), los agentes de IA lo pasan por alto por completo, dejando contenido valioso invisible para los sistemas que podrían citarlo.

La oportunidad Recuperar visibilidad del contenido identifica las páginas de su sitio donde existe esta brecha de visibilidad. Para cada página afectada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta los huecos de visibilidad y le permite aplicar correcciones sin necesidad de un CMS o desarrollador.

Se muestran tres métricas clave de un vistazo:

- **URL**: número de páginas identificadas con una brecha de visibilidad del contenido.
- **Ganancia de contenido estimada**: el multiplicador estimado de contenido que podría recuperarse aplicando la optimización.
- **Visibilidad media del contenido**: el porcentaje medio de contenido actualmente visible para los agentes de IA en las páginas afectadas.

![Panel Recuperar visibilidad del contenido](/help/dashboards/opportunities/assets/recover-content-visibility-overview.png)

Para obtener una descripción general en vídeo de esta oportunidad, puede ver[Recuperar la visibilidad del contenido](https://www.youtube.com/watch?v=BigPyJssFCw).

Esta oportunidad se puede optimizar utilizando[Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md). Las optimizaciones se envían exclusivamente a los agentes de IA, sin ningún impacto en los visitantes humanos (envío solo a través de bots). Posteriormente, las optimizaciones se aplican en la capa CDN sin necesidad de realizar cambios en el CMS y pueden surtir efecto en cuestión de minutos sin la intervención de un desarrollador, lo que la convierte en una implementación rápida y de bajo riesgo.

## Funcionamiento

LLM Optimizer analiza tus páginas comparando a qué tienen acceso los agentes de IA con lo que realmente está presente en la página. Las páginas que reciben mucho tráfico de agentes pero tienen poca visibilidad del contenido se muestran en la tabla **URL con sugerencias**, priorizadas por volumen de tráfico agéntico.

En cada URL afectada, LLM Optimizer proporciona:

- **Análisis de IA**: una descripción del contenido que falta y por qué es importante para la citabilidad del LLM, junto con una lista de referencias de contenido que podrían recuperarse
- **Visibilidad del contenido**: el porcentaje de contenido actualmente visible para los agentes de IA en dicha página
- **Coeficiente de ganancia de contenido**: el multiplicador estimado del contenido recuperable si se aplica la optimización
- **Vista previa**: una comparación en paralelo HTML que muestra cómo se ve la página ahora en comparación con después de la optimización, para que pueda validar el cambio antes de implementarlo

La solución se aplica mediante[Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md), la capacidad de implementación basada en el extremo de Adobe que proporciona una instantánea HTML totalmente prerenderizada y compatible con IA a los agentes de usuario de LLM en la capa CDN, recuperando contenido previamente oculto sin tocar su CMS.

<!-- [URLs with suggestions](/help/dashboards/opportunities/assets/recover-content-visibility-urls.png)-->

## URL con sugerencias

La tabla **URL con sugerencias** enumera todas las páginas afectadas y se puede filtrar por clasificación. En cada URL puede hacer lo siguiente:

- **Expanda la fila** para ver el análisis de IA, incluido el contenido que falta y por qué es importante.
- **Ver una vista previa** de la comparación HTML en paralelo de la página actual frente a la versión posterior a la optimización.
- **Marcar como solucionado** una vez que se haya resuelto el problema.
- **Ignorar** sugerencias que no sean relevantes.

Las sugerencias se organizan en tres vistas:**Sugerencias actuales**,**Sugerencias corregidas** y **Sugerencias ignoradas**. Una vez que se implementa una sugerencia, pasa a Sugerencias fijas con un estado de **Optimizado** y una acción **Ver en vivo** para verificar que la optimización esté activa para el tráfico agéntico. Las sugerencias fijas también se pueden revertir en cualquier momento.

![Sugerencias corregidas con estado Optimizado](/help/dashboards/opportunities/assets/recover-content-visibility-fixed.png)

## Implementar la optimización

Una vez que haya revisado las sugerencias y seleccionado las URL que desea optimizar, haga clic en **Implementar optimizaciones** para publicar la solución en el extremo de la CDN. Un cuadro de diálogo de confirmación **Implementar en Edge** muestra las URL seleccionadas, su tipo (Prerenderizado) y la sugerencia que se está aplicando. Tras la implementación, una pantalla de confirmación indica qué URL se optimizaron correctamente.

>[!NOTE]
>
>Para implementar las optimizaciones, es necesario completar el proceso de incorporación de Optimizar en Edge. Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

Cuadro de diálogo ![Implementar en Edge](/help/dashboards/opportunities/assets/recover-content-visibility-deploy.png)

## Probar en la demostración

Vea en acción la oportunidad Recuperar visibilidad del contenido utilizando el entorno de demostración de Frescopa.

[Vea Recuperar visibilidad del contenido en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/prerender/75729489-756a-4c2b-9905-155b1715da5c)

## Preguntas frecuentes

**¿Por qué el contenido de mi página no es visible para los agentes de IA?**

La mayoría de los sitios web modernos utilizan JavaScript para cargar el contenido de forma dinámica después de la solicitud inicial de la página. Por lo general, los agentes de IA no ejecutan JavaScript, por lo que el agente de IA nunca ve el contenido representado en el lado del cliente (listados de productos, reseñas de usuarios, vínculos a artículos de blog y elementos similares), incluso si es totalmente visible para los visitantes humanos.

**¿Esta optimización afectará a mis visitantes humanos o a los bots de SEO?**

No. Optimizar en Edge está pensado únicamente para los agentes de usuario de IA. Los visitantes humanos y los bots de SEO reciben la página original exactamente como antes, sin cambios en su experiencia ni en el rendimiento.

**¿Necesito cambiar mi CMS o involucrar a los desarrolladores?**

No. La optimización se aplica en el perímetro de la CDN y no requiere cambios de creación, despliegues de código ni la participación de desarrolladores. Una vez que se haya incorporado a Optimizar en Edge, podrá implementar y restablecer cambios en cuestión de minutos directamente desde la interfaz de LLM Optimizer.

**¿Qué sucede si el contenido de mi página cambia después de la implementación?**

Para recuperar la visibilidad del contenido de recuperación, LLM Optimizer utiliza una configuración de TTL de la caché bajo para que cualquier actualización del contenido en el sitio desencadene una actualización en cuestión de minutos. Los agentes de IA siempre recibirán la versión más actualizada de su contenido.

**¿Cómo empiezo a utilizar Optimizar en Edge?**

Consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para ver el proceso de incorporación completo, las guías de configuración de CDN y los requisitos previos.
