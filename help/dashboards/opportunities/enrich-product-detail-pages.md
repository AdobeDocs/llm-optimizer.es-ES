---
title: Enriquecimiento de página de detalles del producto
description: Descubra cómo LLM Optimizer identifica las páginas de productos en las que los datos del catálogo se ocultan a los agentes de IA y cómo recuperar esa visibilidad mediante la optimización basada en Edge y las perspectivas del catálogo de productos con tecnología de Adobe Commerce.
feature: Opportunities
autotag-review: '2026-07-15T17:50:18.330Z'
TQID: 'https://experienceleague.adobe.com/UINqU57uqqbNJE3cV6zK56hxCcAmRrMMv-esNEfxqKI'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2:
  - id: a6256a78-8814-462c-9627-86699b39cee1
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 1210
ht-degree: 7%

---


# Enriquecimiento de páginas de detalles del producto

Los agentes de IA solo pueden recomendar productos que puedan comprender completamente. En la mayoría de las tiendas de comercio, las páginas de productos están diseñadas para compradores humanos. Como tal, estos productos dependen de pestañas procesadas por JavaScript, paneles expandibles, asistentes de compras, modelos interactivos y vínculos a variantes, especificaciones y características de productos de superficie. Los agentes de IA no analizan las profundidades de la página de detalles del producto, lo que significa que los rastreadores de LLM que impulsan la detección impulsada por IA nunca ven estos datos de producto enriquecidos, incluso cuando son totalmente visibles para los visitantes humanos.

La oportunidad Enriquecimiento de las páginas de detalles del producto identifica las páginas de producto en el catálogo de Adobe Commerce donde existe este hueco de visibilidad. Con la tecnología del catálogo de Adobe Commerce, compara los agentes de IA que pueden acceder a la tienda con los datos de producto completos disponibles en el catálogo y muestra todos los atributos, variantes y la profundidad de las características del producto que faltan en la vista del agente de IA.

De un vistazo, muestra las siguientes métricas clave:

- **Páginas de producto**: la lista de todas las páginas de detalles de producto identificadas con un intervalo de visibilidad de datos del catálogo.
- **Tráfico agéntico**: El total de visitas e interacciones en un sitio que inician e impulsan agentes de IA autónomos (como asistentes o bots con tecnología LLM) que actúan en nombre de usuarios para descubrir contenido, recuperarlo o interactuar con él.

![Enriquecer panel de páginas de detalles del producto](/help/dashboards/opportunities/assets/enrich-product-detail-pages-overview.png)

Esta oportunidad se puede optimizar utilizando[Optimizar en Edge](https://experienceleague.adobe.com/es/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge). Las optimizaciones se entregan exclusivamente a agentes de IA sin impacto en los visitantes humanos (entrega solo de bots), se aplican en el nivel de CDN sin necesidad de cambios de CMS o catálogo y pueden entrar en vigor en minutos sin participación del desarrollador, lo que lo convierte en una ruta de implementación rápida y de bajo riesgo para catálogos de productos grandes.

## Funcionamiento

El agente de catálogo de Adobe Commerce lee todos los datos de su catálogo de productos, incluidas las variantes, las relaciones de producto más profundas, los atributos, las facetas, los metadatos de categoría y todas las características del producto. A continuación, compara los datos con lo que realmente pueden acceder los agentes de IA en la PDP de la tienda correspondiente. Las páginas en las que se ocultan los datos del catálogo de los rastreadores de IA aparecen en la tabla **URL con sugerencias**, priorizadas por el volumen de tráfico auténtico.

Para cada página de producto afectada, LLM Optimizer proporciona:

- **Vista previa del análisis de IA**: una lista completa de la información de catálogo que falta en la vista del agente de IA y por qué es importante para el descubrimiento de productos impulsados por LLM, incluida una lista de puntos de datos recuperables como variantes de productos, opciones de tamaño, especificaciones de materiales y detalles de compatibilidad, entre otros.

La corrección se aplica usando [Optimizar en Edge](https://experienceleague.adobe.com/es/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge): la capacidad de implementación basada en Edge de Adobe que ofrece una instantánea de HTML totalmente procesada previamente y compatible con IA a los agentes de usuario de LLM en el nivel de CDN. Esto recupera todos los datos de catálogo previamente ocultos (incluidas las variantes de producto, las especificaciones técnicas y los detalles de características) sin tocar el catálogo de Commerce ni la interfaz de usuario de tienda visible humana.

![URL con tabla de sugerencias](/help/dashboards/opportunities/assets/enrich-product-detail-pages-suggestions.png)

## URL con sugerencias

La tabla **URL con sugerencias** enumera todas las páginas de productos identificadas que se benefician de una optimización. Para cada URL de producto puede:

- **Vista previa** para ver el análisis de IA, incluida la información de catálogo que falta y por qué son importantes para la detección controlada por IA
- **Marcar como fijo** una vez que se haya implementado y validado la optimización
- **Ignorar** sugerencias que no sean relevantes para su estrategia de comercialización

Las sugerencias se organizan en tres vistas:**Sugerencias actuales**,**Sugerencias corregidas** y **Sugerencias ignoradas**. Una vez implementada una sugerencia, pasa a Fixed Suggestions con un estado de **Optimized** y una acción de **View Live** para verificar que el enriquecimiento esté activo para el tráfico auténtico. Las sugerencias fijas se pueden revertir en cualquier momento.

## Implementar la optimización

Una vez que haya revisado las sugerencias y seleccionado las páginas de productos que desea optimizar, haga clic en **Implementar optimizaciones** para publicar el enriquecimiento en el perímetro de CDN. Un cuadro de diálogo de confirmación de **Implementar en Edge** muestra las direcciones URL del producto seleccionado, el tipo de optimización y el enriquecimiento que se está aplicando. Después de la implementación, una pantalla de confirmación confirma qué páginas de productos se optimizaron correctamente.

La optimización se entrega exclusivamente a los agentes de usuario de IA a través de la capa perimetral de CDN. Los visitantes humanos siguen viendo la experiencia existente de la tienda exactamente como antes sin cambios en el diseño de la PDP, el rendimiento de la página o la experiencia de la marca.

>[!NOTE]
>
>La implementación de optimizaciones requiere (1) conectar LLM Optimizer a Adobe Commerce y (2) completar el proceso de incorporación de Optimize at Edge.

Si la instancia de Commerce aún no está conectada a LLM Optimizer, se le dirigirá a la configuración de conexión antes de que se puedan aplicar los enriquecimientos.

Si aún no ha completado el proceso de incorporación, al hacer clic en **Implementar optimizaciones** se le dirigirá al proceso de incorporación. Para obtener información completa sobre cómo funciona Optimizar en Edge, los proveedores de CDN compatibles y el proceso de incorporación, consulte la página [Optimizar en Edge](https://experienceleague.adobe.com/es/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge).

Cuadro de diálogo ![Implementar en Edge](/help/dashboards/opportunities/assets/enrich-product-detail-pages-deploy.png)

## Probar en la demostración

Vea la oportunidad de Enriquecer las páginas de detalles del producto en acción usando el entorno de demostración de Frescopa.

[Ver páginas de detalles de producto enriquecidos en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Preguntas frecuentes

**¿Por qué se ocultan los datos de mi catálogo de productos a los agentes de IA?**

Los escaparates de Commerce están diseñados para compradores humanos. A menudo, las características del producto, las variantes, las opciones de tamaño, los detalles del material y otras especificaciones técnicas aparecen a través de interacciones impulsadas por JavaScript, como pestañas, paneles contraíbles, modelos emergentes, vínculos y asistentes de compras. Los agentes de IA no analizan las profundidades de la página de detalles del producto, por lo que todos estos datos son invisibles para los rastreadores de LM incluso cuando están completamente presentes en el catálogo de productos. El resultado es que los agentes de IA hacen recomendaciones de productos basadas en una fracción de la información real del producto disponible.

**¿Qué tipos de datos de productos recupera esta optimización?**

El agente de catálogo recupera toda la información de producto disponible en su catálogo de Adobe Commerce a la que los agentes de IA no pueden acceder actualmente en la tienda. Esto incluye caracteres de producto, relaciones, variantes (tamaños, colores, configuraciones), especificaciones y atributos técnicos, detalles de compatibilidad, metadatos de categoría y valores de faceta.

**¿Afectará esta optimización a mis visitantes humanos, bots SEO o rendimiento de tienda?**

No. Optimizar en Edge está pensado únicamente para los agentes de usuario de IA. Los visitantes humanos y los bots de optimización de los motores de búsqueda reciben la página de producto original exactamente como antes, sin cambios en su experiencia, rendimiento de carga de página ni diseño de tienda.

**¿Debo cambiar mi catálogo de Commerce, CMS, o involucrar a desarrolladores?**

No. La optimización se aplica en la capa perimetral de la CDN y no requiere cambios en el catálogo de Adobe Commerce, implementaciones de código ni participación del desarrollador. Una vez incorporado para optimizar en Edge, puede implementar y revertir los enriquecimientos en minutos directamente desde la interfaz de LLM Optimizer.

**¿Qué sucede si los datos de mis productos cambian después de la implementación?**

Para la oportunidad Enriquecimiento de las páginas de detalles del producto, LLM Optimizer utiliza la configuración de TTL de caché baja para que cualquier actualización de producto en el catálogo de Commerce déclencheur una actualización en cuestión de minutos. Los agentes de IA siempre recibirán los datos de producto más actualizados disponibles.
