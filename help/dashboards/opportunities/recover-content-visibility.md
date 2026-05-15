---
title: Recuperar visibilidad del contenido
description: Descubra cómo LLM Optimizer identifica las páginas en las que se oculta contenido crítico a los agentes de IA y cómo recuperar esa visibilidad mediante la optimización basada en Edge.
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
ht-degree: 1%

---


# Recuperar visibilidad del contenido

Los agentes de IA solo pueden citar contenido al que pueden acceder. Cuando el contenido clave de las páginas se oculta tras el procesamiento del lado del cliente y las cargas dinámicas (como descripciones de productos, clasificaciones de usuarios, recetas y comentarios), los agentes de IA lo omiten por completo, lo que deja el contenido valioso invisible para los sistemas que podrían citarlo.

La oportunidad Recuperar Visibilidad del contenido identifica las páginas del sitio donde existe esta brecha de visibilidad. Para cada página afectada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta el hueco y le permite aplicar correcciones sin ningún cambio de CMS ni participación del desarrollador.

De un vistazo, muestra tres métricas clave:

- **URL**: número de páginas identificadas con un intervalo de visibilidad del contenido.
- **Ganancia de contenido estimada**: El multiplicador estimado de contenido que se podría recuperar aplicando la optimización.
- **Visibilidad del contenido promedio**: el porcentaje promedio de contenido visible actualmente para los agentes de inteligencia artificial en todas las páginas afectadas.

![Recuperar tablero de Visibilidad del contenido](/help/dashboards/opportunities/assets/recover-content-visibility-overview.png)

Puedes ver [Recuperar Visibilidad del contenido](https://www.youtube.com/watch?v=BigPyJssFCw) para ver un vídeo de información general sobre esta oportunidad.

Esta oportunidad se puede optimizar usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md). Las optimizaciones se entregan exclusivamente a los agentes de IA sin impacto en los visitantes humanos (entrega solo de bots). Las optimizaciones se aplican entonces en la capa de CDN sin necesidad de cambios de CMS y pueden surtir efecto en minutos sin participación del desarrollador, lo que la convierte en una implementación rápida y de bajo riesgo.

## Funcionamiento

LLM Optimizer analiza las páginas comparando lo que los agentes de IA pueden acceder con lo que realmente está presente en la página. Las páginas que reciben un tráfico agéntico elevado pero que tienen una visibilidad del contenido baja aparecen en la tabla **URL con sugerencias**, priorizadas por el volumen de tráfico agéntico.

Para cada URL afectada, LLM Optimizer proporciona:

- **Análisis de IA**: una descripción del contenido que falta y de por qué es importante para la visibilidad de LLM, junto con una lista de referencias de contenido que se podrían recuperar
- **Visibilidad del contenido**: el porcentaje de contenido visible actualmente para los agentes de inteligencia artificial en esa página.
- **Proporción de ganancia de contenido**: multiplicador estimado de contenido recuperable si se aplica la optimización
- **Vista previa**: una comparación de HTML en paralelo que muestra el aspecto actual de la página en comparación con la optimización posterior, para que pueda validar el cambio antes de implementar

La corrección se aplica usando [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md): la capacidad de implementación basada en Edge de Adobe que ofrece una instantánea de HTML totalmente procesada previamente y compatible con IA a los agentes de usuario de LLM en el nivel de CDN, recuperando el contenido oculto anteriormente sin tocar el CMS.

<!-- [URLs with suggestions](/help/dashboards/opportunities/assets/recover-content-visibility-urls.png)-->

## URL con sugerencias

La tabla **URL con sugerencias** enumera todas las páginas afectadas y se pueden filtrar por clasificación. Para cada URL puede:

- **Expanda la fila** para ver el análisis de IA, incluido el contenido que falta y por qué importa.
- **Previsualizar** la comparación de HTML en paralelo de la página actual con la versión posterior a la optimización.
- **Marcar como corregido** una vez solucionado el problema.
- **Ignorar** sugerencias que no sean relevantes.

Las sugerencias están organizadas en tres vistas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**. Una vez implementada una sugerencia, pasa a Fixed Suggestions con un estado de **Optimized** y una acción de **View Live** para verificar que la optimización esté activa para el tráfico auténtico. Las sugerencias fijas también se pueden revertir en cualquier momento.

![Se han corregido sugerencias con el estado Optimizado](/help/dashboards/opportunities/assets/recover-content-visibility-fixed.png)

## Implementación de la optimización

Una vez que haya revisado las sugerencias y seleccionado las direcciones URL para optimizar, haga clic en **Implementar optimizaciones** para publicar la corrección en el perímetro de CDN. Un cuadro de diálogo de confirmación de **Implementar en Edge** muestra las direcciones URL seleccionadas, su tipo (procesamiento previo) y la sugerencia que se está aplicando. Después de la implementación, una pantalla de confirmación confirma qué direcciones URL se optimizaron correctamente.

>[!NOTE]
>
>La implementación de optimizaciones requiere completar el proceso de incorporación de Optimizar en Edge. Si aún no se ha incorporado, al hacer clic en **Implementar optimizaciones**, se le dirigirá al proceso de incorporación. Para obtener información detallada sobre cómo funciona Optimizar en Edge, los proveedores de CDN admitidos y el proceso de incorporación, consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md).

![Implementar en el cuadro de diálogo de Edge](/help/dashboards/opportunities/assets/recover-content-visibility-deploy.png)

## Probar en la demostración

Vea la oportunidad de Recuperar Visibilidad del contenido en acción usando el entorno de demostración de Frescopa.

[Ver Visibilidad del contenido de recuperación en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/prerender/75729489-756a-4c2b-9905-155b1715da5c)

## Preguntas frecuentes

**¿Por qué se oculta el contenido de mi página a los agentes de inteligencia artificial?**

La mayoría de los sitios web modernos dependen de JavaScript para cargar contenido de forma dinámica después de la solicitud de página inicial. Los agentes de IA no suelen ejecutar JavaScript, por lo que el contenido procesado del lado del cliente (listas de productos, críticas de usuarios, vínculos de artículos de blog y elementos similares) nunca se ve por el agente de IA, aunque sea totalmente visible para los visitantes humanos.

**¿Afectará esta optimización a mis visitantes humanos o bots SEO?**

No. Optimizar en Edge solo segmenta los agentes de usuario de IA. Los visitantes humanos y los bots de optimización de los motores de búsqueda reciben la página original exactamente como antes, sin cambios en su experiencia o rendimiento.

**¿Debo cambiar mi CMS o involucrar a los desarrolladores?**

No. La optimización se aplica en el perímetro de la CDN y no requiere cambios de creación, implementaciones de código ni participación del desarrollador. Una vez incorporado para optimizar en Edge, puede implementar y revertir los cambios en minutos directamente desde la interfaz de LLM Optimizer.

**¿Qué sucede si el contenido de mi página cambia después de implementar?**

Para la Visibilidad del contenido de recuperación, LLM Optimizer utiliza la configuración de TTL de caché baja para que cualquier actualización de contenido en el sitio déclencheur una actualización en cuestión de minutos. Los agentes de IA siempre recibirán la versión más actualizada de su contenido.

**¿Cómo empiezo con Optimizar en Edge?**

Consulte la página [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) para ver el proceso de incorporación completo, las guías de configuración de CDN y los requisitos previos.
