---
title: Optimizar en Edge
description: Obtenga información sobre cómo entregar optimizaciones en LLM Optimizer en el perímetro de la CDN sin necesidad de realizar cambios en la creación.
feature: Opportunities
autotag-review: '2026-05-15T17:55:41.072Z'
TQID: 'https://experienceleague.adobe.com/kMxoKtrfyzxIpLJP9nt-rq6GP37ICCNe4XienUKqDZE'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: d1956731-2adb-4bb7-8301-2b239254ac72id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 3108
ht-degree: 57%

---


# Optimizar en Edge

Esta página proporciona información general detallada sobre cómo entregar optimizaciones en el perímetro de CDN sin ningún cambio en la creación. Abarca el proceso de incorporación, las oportunidades de optimización disponibles y cómo optimizar automáticamente en Edge.

## ¿Qué es Optimizar en Edge?

Optimizar en Edge es una capacidad de implementación basada en Edge en LLM Optimizer que proporciona cambios compatibles con la IA a los agentes de usuario de LLM. En el contexto actual, “Edge” significa que la optimización se aplica en la capa de CDN. Dado que ofrece optimizaciones en la capa de CDN, no se requieren cambios de creación en el sistema de administración de contenido (CMS), por lo que el CMS de origen permanece sin cambios. Esta separación le permite mejorar la visibilidad de LLM sin alterar los flujos de trabajo de publicación existentes. Se dirige únicamente al tráfico agéntico y no afecta ni a los usuarios humanos ni a los bots de SEO. Cuando LLM Optimizer detecta oportunidades para optimizar una página, los usuarios pueden implementar correcciones directamente en el perímetro de la CDN.

Optimizar en Edge es una alternativa más rápida y sencilla que las correcciones tradicionales que requieren esfuerzos de ingeniería complejos. Como se ha mencionado, una vez que complete una configuración única, no se requieren cambios de plataforma ni ciclos de desarrollo largos para aplicar los cambios. Puede publicar mejoras en minutos sin necesidad de participación del desarrollador. Es una forma sin código de optimizar el sitio web para los agentes de IA.

Optimizar en Edge está concebido para usuarios empresariales en equipos de marketing, SEO, contenido y estrategia digital. Permite a los usuarios empresariales completar el recorrido completo en LLM Optimizer como identificar oportunidades, comprender sugerencias e implementar fácilmente las correcciones. Con Optimizar en Edge, los usuarios obtienen una vista previa de los cambios que se implementan rápidamente en CDN, también validan que las optimizaciones estén activas. Se puede realizar un seguimiento del rendimiento en el ecosistema de LLM Optimizer.

### Ventajas principales

* **Envío solo de IA:** sirve HTML optimizado solo a agentes de IA sin afectar a los visitantes humanos ni a los bots de SEO.
* **Ciclos más rápidos:** publique cambios en minutos, no en semanas. No se requieren cambios de plataforma ni ciclos de ingeniería largos.
* **Reversible:** compatibilidad con una capacidad de reversión en un clic para revertir la página en minutos.
* **Sin impacto en el rendimiento:** las optimizaciones y el almacenamiento en caché basados en Edge no afectan la latencia del sitio.
* **No depende de CDN ni de CMS:** funciona con cualquier configuración de CDN y configuración de front-end, independientemente del sistema de administración de contenido.

### ¿Qué oportunidades se admiten con Optimizar en Edge?

Las oportunidades que pueden mejorar la experiencia web auténtica se admiten con Optimizar en Edge. Obtenga más información acerca de cada oportunidad en la página [Panel de control de oportunidades](/help/dashboards/opportunities-overview.md) y en la sección de oportunidades de la página actual.

## Incorporación

<!--You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.-->

Inicie el proceso de incorporación en su cuenta de LLM Optimizer:

1. En el panel **Configuración del cliente**, seleccione la pestaña **Configuración de CDN**.
1. Haga clic en **CDN integrada**.
   ![Ficha Configuración de CDN](/help/overview/assets/cc-cdn.png)
1. Para los clientes de Fastly administrados por AEM Cloud Service, la configuración de enrutamiento es de autoservicio y se puede completar directamente en la interfaz de usuario de LLM Optimizer. Para los clientes que utilizan otros proveedores de CDN, su equipo de TI/CDN debe completar la configuración y los requisitos previos necesarios. También puede consultar las guías de CDN de ejemplo que se proporcionan a continuación para obtener más instrucciones.

>[!NOTE]
>Consulte las guías paso a paso a continuación que abarcan todo el flujo de incorporación. Para problemas no resueltos por las guías, puede comunicarse con `llmo-at-edge@adobe.com`.

Requisitos para su equipo de TI/CDN:

* Añada el agente de usuario `*AdobeEdgeOptimize/1.0*` a la lista de permitidos del archivo robots.txt del sitio o a las reglas de administración del tráfico de bots.
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o de CDN.
* Añadir las reglas de enrutamiento de Optimizar en Edge en la CDN.
* Si su CDN tiene reglas de WAF o Bot Manager, lista de permitidos el agente de usuario `*AdobeEdgeOptimize/1.0*`. Si se requiere una verificación adicional, configure el encabezado `x-edgeoptimize-fetcher-key`. Cada guía de BYOCDN a continuación incluye los pasos.
* Confirmar Optimizar en Edge en la interfaz de LLM Optimizer.

El diagrama siguiente ilustra cómo fluyen las solicitudes a través de una configuración de BYOCDN con Optimizar en Edge:

![Flujo de solicitud BYOCDN](/help/assets/optimize-at-edge/byocdn-request-flow.png)

>[!IMPORTANT]
>El enrutamiento debe configurarse en la CDN externa (la CDN más cercana al cliente). Si tiene varias CDN, el enrutamiento solo se puede realizar en la CDN externa.

Para guiarle en el proceso de configuración, seleccione a continuación su proveedor de CDN y siga la guía de configuración correspondiente. Tenga en cuenta que estos ejemplos deben adaptarse a la configuración real en directo. Se recomienda aplicar primero los cambios en los entornos inferiores.

### Guías de configuración de la CDN

| Proveedor de CDN | Tipo | Guía |
|---|---|---|
| CDN administrada por AEM Cloud Service (Fastly) | Administrado por Adobe | [Ver guía de configuración](/help/dashboards/optimize-at-edge/aemcs-managed-cdn.md) |
| Fastly (BYOCDN) | Traer su propia CDN | [Ver la guía de configuración](/help/dashboards/optimize-at-edge/fastly-byocdn.md) |
| Akamai (BYOCDN) | Traer su propia CDN | [Ver la guía de configuración](/help/dashboards/optimize-at-edge/akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Traer su propia CDN | [Ver la guía de configuración](/help/dashboards/optimize-at-edge/cloudflare-byocdn.md) |
| CloudFront (BYOCDN) | Traer su propia CDN | [Ver la guía de configuración](/help/dashboards/optimize-at-edge/cloudfront-byocdn.md) |

>[!NOTE]
>
>Si su proveedor de CDN no aparece en la lista anterior o si no encuentra su dominio o correo electrónico en la IU de LLM Optimizer, póngase en contacto con `llmo-at-edge@adobe.com` para obtener ayuda sobre la incorporación. Una vez completadas las configuraciones, puede implementar sugerencias para las oportunidades de Optimizar en Edge en LLM Optimizer.

Cada guía anterior de configuración de la CDN incluye pasos de verificación detallados al final para confirmar que el tráfico agéntico se enruta correctamente y que el tráfico humano no se ve afectado.

## Oportunidades

En la tabla siguiente se presentan las oportunidades que pueden mejorar la experiencia web agéntica y que son compatibles con Optimizar en Edge.

| Oportunidad | Tipo | Identificación automática | Sugerencia automática | Optimización automática |
|---------|----------|----------|----------|----------|
| [Recuperar Visibilidad del contenido](/help/dashboards/opportunities/recover-content-visibility.md) | Optimización técnica del motor generativo | Detecta páginas donde se oculta contenido crítico a los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Resalta el contenido que puede estar disponible para los agentes de IA y recomienda habilitar el procesamiento previo para esas páginas. | Proporciona una instantánea de HTML totalmente procesada y compatible con IA al tráfico agéntico que recupera el contenido oculto anteriormente. |
| [Enriquecer páginas de detalles del producto](/help/dashboards/opportunities/enrich-product-detail-pages.md) | Optimización técnica del motor generativo | En el caso de las tiendas Adobe Commerce, compara los datos de catálogo completos con los datos a los que los agentes de IA pueden acceder en cada página de detalles del producto; muestra los PDP en los que faltan variantes, especificaciones, atributos y campos de catálogo relacionados en el HTML visible del agente, priorizados por el tráfico auténtico. | Resalta la información de catálogo recuperable que falta en la vista del agente y por qué importa para el descubrimiento de productos impulsados por LLM. | Proporciona una instantánea de HTML totalmente procesada previamente y compatible con IA al tráfico auténtico en el perímetro de la CDN para que los agentes reciban un contexto de producto enriquecido de su catálogo sin CMS ni cambios de catálogo. |
| [Agregar resúmenes compatibles con LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | Optimización de contenido | Identifica páginas de alto tráfico que carecen de resúmenes concisos y puntos clave estructurados en el nivel de página o sección, lo que dificulta que los agentes de IA las analicen e interpreten. | Recomienda resúmenes breves generados por IA y puntos clave basados en contenido existente. | Inserta resúmenes y puntos clave en las secciones relevantes de HTML, lo que mejora la forma en que los modelos interpretan y describen el contenido de la página. |
| [Agregar preguntas más frecuentes](/help/dashboards/opportunities/add-relevant-faqs.md) | Optimización de contenido | Identifica páginas de alto tráfico que carecen de contenido de preguntas y respuestas estructurado y que están alineadas con el conjunto de mensajes, lo que dificulta que los agentes de inteligencia artificial relacionen las preguntas del usuario con su página. | Sugiere contenido de preguntas más frecuentes generado por IA y alineado con la intención del usuario y los temas de la página existentes. | Inserta contenido de preguntas frecuentes en el HTML, lo que hace que las páginas sean más detectables y relevantes en las respuestas basadas en IA. |
| [Simplificar contenido complejo](/help/dashboards/opportunities/simplify-complex-content.md) | Optimización de contenido | Indica las páginas con texto complejo que puede dificultar la comprensión de la IA. | Proporciona versiones simplificadas de texto complejo generadas por IA preservando al mismo tiempo el significado original. | Reescribe secciones complejas en la página, lo que mejora la legibilidad de la IA. |
| [Agregar tabla de contenido](/help/dashboards/opportunities/add-table-of-contents.md) | Optimización técnica del motor generativo | Detecta páginas que carecen de encabezados de navegación u organización estructural claros, lo que dificulta que los agentes de IA analicen y asignen contenido a consultas de usuarios. | Sugiere una tabla de contenido estructurada con encabezados vinculados por anclajes que reflejen las secciones principales de la página. | Inserta una tabla de contenido en HTML, lo que mejora la estructura de la página para que los modelos de IA puedan extraer, asignar y citar más fácilmente secciones relevantes. |
| [Agregar resúmenes de transcripciones multimedia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | Optimización de contenido | Identifica las páginas en las que la información clave está incrustada en vídeo u otros medios sin transcripciones o resúmenes legibles por el equipo, lo que dificulta el uso del contenido para los agentes de IA. Muestra las direcciones URL afectadas y el texto recomendado. | Recomienda resúmenes de transcripciones generados por IA basados en los medios y en la página. | Inserta resúmenes de transcripción en HTML para que el tráfico auténtico reciba texto legible por máquina (por ejemplo, cerca del vídeo correspondiente). |

### Herramientas adicionales

La extensión del explorador [Comprobador de Visibilidades del contenido de IA](https://chromewebstore.google.com/detail/ai-content-visibility-che/jbjngahjjdgonbeinjlepfamjdmdcbcc) muestra la cantidad de contenido de la página web a la que pueden acceder los LLM y lo que permanece oculto. Diseñado como una herramienta de diagnóstico gratuita e independiente, no requiere licencia de producto ni configuración.

Con un solo clic, puede evaluar la legibilidad automática de cualquier sitio. Puede ver una comparación en paralelo de lo que ven los agentes de IA frente a lo que ven las personas y realizar un cálculo estimado de cuánto contenido se puede recuperar mediante LLM Optimizer. Consulte la página [¿Puede la IA leer su sitio web?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obtener más información.

## Oportunidades detalladas

En las secciones siguientes, puede ver detalles adicionales de cada oportunidad compatible con Optimizar en Edge.

### Recuperar visibilidad del contenido

Esta oportunidad indica las páginas donde el contenido clave está oculto para los agentes de IA debido al procesamiento en el lado del cliente. Para cada página identificada, muestra exactamente qué contenido falta en la vista del agente de IA, resalta los huecos de visibilidad y le permite aplicar cambios directamente para recuperar el contenido oculto. Al implementar esta oportunidad con Optimizar en Edge, se proporciona una versión de la página procesada previamente y optimizada con IA para los agentes de usuario de LLM para que puedan acceder al contexto completo sin ejecutar JavaScript.
Esto garantiza que la página sea primero totalmente visible para los agentes de IA. Además de ese HTML preprocesado, se aplican mejoras adicionales.

>[!IMPORTANT]
>Esta funcionalidad de procesamiento previo se aplica automáticamente a todas las oportunidades que se presentan a continuación cuando se implementa con Optimizar en Edge para garantizar que la página sea totalmente visible para los agentes de IA.

Consulte [Recuperar Visibilidad del contenido](/help/dashboards/opportunities/recover-content-visibility.md) para ver una guía de panel, los pasos de implementación y las preguntas más frecuentes.

### Enriquecimiento de páginas de detalles del producto

Esta oportunidad se dirige a páginas de detalles de productos de Adobe Commerce donde los compradores ven un contexto de producto completo a través de experiencias de tienda interactivas, pero los agentes de IA solo reciben una instantánea de HTML superficial. El agente de catálogo compara el catálogo de Commerce autorizado con el PDP visible del agente, enumera todas las lagunas significativas (por ejemplo, variantes o especificaciones que nunca aparecen en HTML estático) y le permite implementar una respuesta perimetral solo de bots que restaura la paridad para los rastreadores LLM sin alterar los registros del catálogo ni la IU humana.

Consulte [Enriquecimiento de las páginas de detalles del producto](/help/dashboards/opportunities/enrich-product-detail-pages.md) para ver una guía de panel, los pasos de implementación y las preguntas más frecuentes.

### Añadir resúmenes compatibles con LLM

Esta oportunidad identifica páginas de alto tráfico que pueden beneficiarse de resúmenes concisos y puntos clave estructurados para que los LLM puedan entender rápidamente las reclamaciones en la página. Para cada página, detecta dónde más se necesita un resumen y propone resúmenes generados por IA (y puntos clave cuando son relevantes) a nivel de página o sección, basados en contenido existente. Al implementar con Optimizar en Edge, ese contenido se inserta en HTML que recuperan los agentes de IA, lo que mejora la precisión con que la marca se representa en las respuestas de IA.

Consulte [Agregar resúmenes aptos para LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) para obtener más información sobre esta oportunidad.

### Añadir preguntas frecuentes relevantes

Esta oportunidad indica páginas de alto tráfico en las que el contenido adicional de preguntas y respuestas podría coincidir mejor con la intención del usuario y las indicaciones en el descubrimiento controlado por IA. Para cada página, propone bloques de preguntas más frecuentes generados por IA vinculados a su conjunto de mensajes y al contenido de la página. Con Optimizar en Edge, estas preguntas frecuentes se insertan en HTML, lo que hace que su página sea más compatible con IA y aumenta la probabilidad de que las respuestas de IA reflejen directamente sus directrices.

Consulte [Agregar preguntas más frecuentes](/help/dashboards/opportunities/add-relevant-faqs.md) relevantes para ver una guía de panel, los pasos de implementación y las preguntas más frecuentes.

### Simplificar contenido complejo

Esta oportunidad encuentra páginas con párrafos largos y complejos que pueden reducir la comprensión de la IA. Para cada página que supera los umbrales de legibilidad, crea contenido generado por IA que es más sencillo y fácil de analizar, conservando al mismo tiempo el significado original. Cuando se implementa en el perímetro, el contenido simplificado que se entrega al tráfico agéntico ayuda a los LLM a interpretar y resumir el contenido con mayor fiabilidad.

Consulte [Simplificar contenido complejo](/help/dashboards/opportunities/simplify-complex-content.md) para ver una guía de panel, los pasos de implementación y las preguntas más frecuentes.

### Agregar tabla de contenido

Esta oportunidad detecta las páginas que son difíciles de navegar para los agentes de IA porque los encabezados y la estructura de sección no están claros o no están presentes. Para cada página afectada, propone una tabla de contenido estructurada con entradas enlazadas con anclaje alineadas con las secciones principales. Al implementar con Optimizar en Edge, esa tabla de contenido se inserta en HTML para que los modelos puedan asignar de forma más fiable las consultas de usuario a las partes correctas de la página y citarlas.

Consulte [Agregar tabla de contenido](/help/dashboards/opportunities/add-table-of-contents.md) para ver una guía de panel, los pasos de implementación y las instrucciones de acceso anticipado.

### Agregar resúmenes de transcripciones multimedia

Esta oportunidad se dirige a páginas donde la información importante solo se encuentra dentro de la reproducción de vídeo, sin transcripciones ni resúmenes de texto que los agentes de IA puedan leer. Para cada página, recomienda transcripciones generadas por IA y breves resúmenes de los puntos clave de los medios. Con Optimizar en Edge, estos resúmenes se añaden a HTML como texto legible por máquina, de modo que los agentes pueden utilizar el mismo contenido que obtienen los visitantes humanos al ver el vídeo.

Consulte [Agregar resúmenes de transcripciones multimedia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) para ver una guía de panel, los pasos de implementación y las preguntas más frecuentes.

## Optimización automática en Edge

Para cada oportunidad, puede obtener una vista previa, editar, implementar, ver en directo y restablecer las optimizaciones en el perímetro.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Vista previa

La **Vista previa** le permite ver el impacto de una sugerencia antes de que se ponga en marcha. Muestra una comparación en paralelo entre la página actual y la versión optimizada por IA que se espera después de aplicar la sugerencia. Esta vista utiliza la misma lógica de Optimizar en Edge que activará el tráfico en directo, pero en un modo de vista previa aislado. Esto no afecta al tráfico en directo, ya que es una simulación de solo lectura para la revisión.

![Vista previa](/help/assets/optimize-at-edge/preview.png)

### Editar

**Editar** le permite perfeccionar o reescribir por completo la sugerencia generada automáticamente antes de implementarla. En lugar de aceptar la sugerencia, mantiene un control total a través del flujo de trabajo de edición. La vista muestra los cambios propuestos en un editor estructurado, donde puede modificar el texto para que se ajuste mejor a la intención original. A continuación, la versión editada se proporcionará a los agentes de IA una vez implementada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implementar

**Implementar** publica las sugerencias seleccionadas para que las experiencias optimizadas se puedan ofrecer desde el perímetro a los agentes de IA. Si la CDN está completamente enrutada, todas las páginas del dominio suelen estar disponibles con los nuevos cambios en cuestión de minutos. Si el enrutamiento solo se ha configurado para rutas seleccionadas, solo las páginas incluidas en la lista de permitidos se publicarán con las optimizaciones.

![Implementar](/help/assets/optimize-at-edge/deploy.png)

### Ver en directo

**Ver en directo** le permite verificar que la optimización está activa y que se comporta según lo esperado para el tráfico agéntico, una vista a la que de otra manera sería difícil acceder. Puede ver la página activa en Sugerencias fijas, que procesa la página tal como se muestra a los agentes de IA.

![Ver en directo](/help/assets/optimize-at-edge/view-live.png)

### Reversión

Una reversión de forma segura revierte una optimización implementada anteriormente. La versión de solo IA de la página suele volver a su estado anterior en cuestión de minutos, lo que permite experimentar con optimizaciones cuando es necesario.

![Reversión](/help/assets/optimize-at-edge/rollback.png)

## Recursos adicionales

Para obtener más información sobre la capacidad Optimizar en Edge, consulte la siguiente lista de reproducción [LLM Optimizer — Optimizar en Edge](https://www.youtube.com/playlist?list=PLzbVcr6JHocVSMWBCaCw4xxjQ_VFVvFh0).

## Preguntas frecuentes

P: ¿Pueden los clientes de prueba probar Optimize en Edge?

Sí, los clientes de prueba pueden acceder a una oportunidad de optimización e implementarla para un máximo de 10 páginas. De forma predeterminada, la oportunidad es Recuperar Visibilidad del contenido, que permite a los agentes de IA acceder a la versión completa del contenido de la página.

P. ¿A qué tipos de LLM se dirige con Optimizar en Edge?

Usted es quien define la lista de agentes de usuario a los que dirigirse durante el proceso de incorporación.

<!--
Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.
-->

P. ¿Qué sucede si todavía no me he incorporado a Optimizar en Edge?

Si hace clic en **Implementar optimizaciones** antes de completar la configuración necesaria, no se aplicará nada al sitio. En su lugar, un cuadro de diálogo emergente le solicitará que se ponga en contacto con nuestro equipo en `llmo-at-edge@adobe.com` para obtener ayuda sobre la incorporación. Hasta que se complete la incorporación, aún puede explorar las oportunidades y sugerencias detectadas, pero el flujo de trabajo de implementación con un solo clic permanecerá inactivo.

P: ¿Qué sucede cuando el contenido se actualiza en la fuente?

Servimos la versión optimizada de su página desde la caché siempre y cuando la página fuente subyacente no haya cambiado. Sin embargo, cuando la fuente cambia en **Recuperar la visibilidad del contenido**, nuestro sistema se actualiza automáticamente para que los agentes de IA siempre reciban el contenido más actualizado. Esto se debe a que utilizamos una configuración de tiempo de vida (TTL) de la caché baja (del orden de minutos) de modo que cualquier actualización de contenido en su sitio activa una nueva optimización dentro de ese intervalo. Para oportunidades de contenido como **Añadir resúmenes compatibles con LLM**, LLM Optimizer supervisa la página de origen en busca de cambios. Si se detecta un cambio, pausamos la optimización y la marcamos para que sea analizada por humanos a fin de evitar que el contenido se desplace entre la página visible del agente y la página visible por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. ¿Optimize at Edge solo es para sitios que utilizan Adobe Edge Delivery Service (EDS)?

No. Optimizar en Edge no depende de la red de distribución de contenido (CDN) y funciona con cualquier arquitectura front-end, no solo con las implementadas en la pila EDS de Adobe.

P. ¿En qué se diferencia el procesamiento previo de Optimizar en Edge del procesamiento tradicional del lado del servidor (SSR)?

Ambos resuelven diferentes problemas y pueden trabajar juntos. El SSR tradicional procesa contenido del lado del servidor, pero no incluye contenido cargado posteriormente en el explorador. El procesamiento previo de Optimizar en Edge captura la página después de que JavaScript y los datos del lado del cliente se hayan cargado, lo que produce la versión completamente ensamblada en el perímetro de CDN. SSR se centra en mejorar la experiencia humana y Optimizar en Edge mejora la experiencia web para los LLM.

P. ¿Recuperar Visibilidad del contenido (es decir, preprocesamiento) es un encubrimiento? Parece que se está ofreciendo una versión diferente de la página a los agentes de inteligencia artificial.

No. El procesamiento previo garantiza que los agentes de IA puedan ver el mismo contenido que los visitantes humanos y los bots de SEO ya ven. Muchos sitios cargan contenido significativo con JavaScript, que los agentes de IA típicos no ejecutan, de modo que los agentes pueden perder grandes partes de la página. El procesamiento previo produce una instantánea estática que captura el texto completo, de modo que los agentes reciben la misma información que los seres humanos y los motores de búsqueda. **restaura** la paridad de contenido para los LLM; no agrega ni cambia contenido factual.

P. ¿Qué sucede con otras oportunidades de contenido, como Agregar resúmenes descriptivos de LLM, en los que aparece una copia nueva en la página ofrecida a los agentes? ¿Eso es encubrimiento?

No. Optimizar en Edge no presenta información a la que los usuarios humanos y los rastreadores en optimización de los motores de búsqueda no puedan acceder. El servicio reorganiza o resume el contenido que ya existe en la página para que los agentes de inteligencia artificial puedan interpretarlo más fácilmente. Cuando alguien sigue un vínculo de una respuesta de IA a su sitio, puede encontrar la misma información subyacente en la página activa.

P. ¿Qué sucede si implemento optimizaciones para algunas URL de mi dominio, pero no para todas?

Solo se modifican las URL que se hayan optimizado explícitamente. Para las URL con oportunidades implementadas, los agentes de IA reciben la versión optimizada. Para las URL sin oportunidades implementadas, nuestro servicio simplemente envía la página original tal cual sin aplicar cambios ni almacenarla en nuestra capa de caché de optimización. Esto garantiza que pueda implementar las optimizaciones de forma selectiva sin afectar al resto del sitio.
