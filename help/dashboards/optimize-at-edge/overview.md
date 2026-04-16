---
title: Optimizar en Edge
description: Obtenga información sobre cómo entregar optimizaciones en LLM Optimizer en el perímetro de la CDN sin necesidad de realizar cambios en la creación.
feature: Opportunities
source-git-commit: 050a4eaa510df7195c5208978ba56d4413916808
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 74%

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

Las oportunidades que pueden mejorar la experiencia web auténtica se admiten con Optimizar en Edge. Obtenga más información acerca de cada oportunidad en la página [Panel de control de oportunidades](/help/dashboards/opportunities.md) y en la sección de oportunidades de la página actual.

## Incorporación

<!--You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.-->

Inicie el proceso de incorporación en su cuenta de LLM Optimizer:

1. En el panel **Configuración del cliente**, seleccione la pestaña **Configuración de CDN**.
1. Haga clic en **CDN integrada**.
   ![Ficha Configuración de CDN](/help/overview/assets/cc-cdn.png)
1. Para los clientes de Fastly administrados por AEM Cloud Service, la configuración de enrutamiento es de autoservicio y se puede completar directamente en la interfaz de usuario de LLM Optimizer. Para los clientes que utilizan otros proveedores de CDN, su equipo de TI/CDN debe completar la configuración y los requisitos previos necesarios. También puede consultar las guías de CDN de ejemplo que se proporcionan a continuación para obtener más instrucciones.

>[!NOTE]
>Consulte las guías paso a paso a continuación que abarcan todo el flujo de incorporación. Para problemas no resueltos por las guías, puede comunicarse con `llmo-at-edge@adobe.com`.

Requisitos previos para la incorporación a Optimizar en Edge:

* Complete el proceso de incorporación a LLM Optimizer.
* Complete el proceso de reenvío de registros para los registros de CDN.

Requisitos para su equipo de TI/CDN:

* Agregue `*AdobeEdgeOptimize/1.0*` user-agent a la Lista de permitidos del archivo robots.txt del sitio o a las reglas de administración del tráfico de bots.
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o de CDN.
* Añadir las reglas de enrutamiento de Optimizar en Edge en la CDN.
* Si su CDN tiene reglas de WAF o Bot Manager, lista de permitidos el agente de usuario `*AdobeEdgeOptimize/1.0*`. Si se requiere una verificación adicional, configure el encabezado `x-edgeoptimize-fetcher-key`. Cada guía de BYOCDN a continuación incluye los pasos.
* Confirmar Optimizar en Edge en la interfaz de LLM Optimizer.

>[!IMPORTANT]
>El enrutamiento debe configurarse en la CDN externa (la CDN más cercana al cliente). Si tiene varias CDN, el enrutamiento solo se puede realizar en la CDN externa.

Para guiar el proceso de configuración, seleccione su proveedor de CDN a continuación y siga la guía de configuración correspondiente. Tenga en cuenta que estos ejemplos deben adaptarse a la configuración real en directo. Se recomienda aplicar primero los cambios en los entornos inferiores. **Traer su propia CDN** guías incluyen pruebas opcionales de nombres de host de ensayo al final de cada página.

### Guías de configuración de CDN

| Proveedor de CDN | Tipo | Guía |
|---|---|---|
| CDN administrada por AEM Cloud Service (rápidamente) | Administrado por Adobe | [Ver guía de configuración](/help/dashboards/optimize-at-edge/aemcs-managed-cdn.md) |
| Rápido (BYOCDN) | Traer su propia CDN | [Ver guía de configuración](/help/dashboards/optimize-at-edge/fastly-byocdn.md) |
| Akamai (BYOCDN) | Traer su propia CDN | [Ver guía de configuración](/help/dashboards/optimize-at-edge/akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Traer su propia CDN | [Ver guía de configuración](/help/dashboards/optimize-at-edge/cloudflare-byocdn.md) |
| CloudFront (BYOCDN) | Traer su propia CDN | [Ver guía de configuración](/help/dashboards/optimize-at-edge/cloudfront-byocdn.md) |

>[!NOTE]
>
>Si su proveedor de CDN no aparece en la lista anterior o si no encuentra su dominio o correo electrónico en la interfaz de usuario de LLM Optimizer, póngase en contacto con `llmo-at-edge@adobe.com` para obtener ayuda sobre la incorporación. Una vez completadas las configuraciones, puede implementar sugerencias para las oportunidades de Optimizar en Edge en LLM Optimizer.

Cada guía de configuración de CDN anterior incluye pasos de verificación detallados al final para confirmar que el tráfico auténtico se enruta correctamente y que el tráfico humano no se ve afectado.

## Oportunidades

En la tabla siguiente se presentan las oportunidades que pueden mejorar la experiencia web agéntica y que son compatibles con Optimizar en Edge.

| Oportunidad | Tipo | Identificación automática | Sugerencia automática | Optimización automática |
|---------|----------|----------|----------|----------|
| Recuperar visibilidad del contenido | Optimización técnica del motor generativo | Detecta páginas donde se oculta contenido crítico a los agentes de IA. Muestra las direcciones URL afectadas y el contenido previsto que se puede recuperar. | Resalta el contenido que puede estar disponible para los agentes de IA y recomienda habilitar el procesamiento previo para esas páginas. | Proporciona una instantánea de HTML totalmente procesada y compatible con IA al tráfico agéntico que recupera el contenido oculto anteriormente. |
| Añadir resúmenes compatibles con LLM | Optimización de contenido | Identifica páginas largas o complejas que carecen de resúmenes concisos a nivel de página o sección, lo que dificulta que la inteligencia artificial las escanee y comprenda rápidamente. | Recomienda resúmenes cortos generados por IA a nivel de página y sección que capturan contenido clave. | Inserta los resúmenes en las secciones relevantes de HTML, lo que mejora la forma en que los modelos interpretan y describen el contenido de la página. |
| Añadir preguntas frecuentes relevantes | Optimización de contenido | Detecta lagunas de intención en el contenido de la página existente que podrían beneficiarse de las preguntas frecuentes. | Sugiere contenido de preguntas frecuentes generado por IA alineado con la intención del usuario y los temas existentes. | Inserta contenido de preguntas frecuentes en el HTML, lo que hace que las páginas sean más detectables y relevantes en las respuestas basadas en IA. |
| Simplificar contenido complejo | Optimización de contenido | Indica las páginas con texto complejo que puede dificultar la comprensión de la IA. | Proporciona versiones simplificadas de texto complejo generadas por IA preservando al mismo tiempo el significado original. | Reescribe secciones complejas en la página, lo que mejora la legibilidad de la IA. |

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

### Añadir resúmenes compatibles con LLM

Esta oportunidad identifica las páginas que pueden beneficiarse de resúmenes concisos para ayudar a los LLM a comprender rápidamente de qué trata el contenido de la página. Para cada página, la oportunidad detecta dónde más se necesita un resumen y crea resúmenes generados por IA a nivel de página o de sección. Cuando se implementa con Optimizar en Edge, estos resúmenes se insertan en el HTML que recuperan los agentes de IA, lo que mejora las posibilidades de que el contenido se describa con mayor precisión.

### Añadir preguntas frecuentes relevantes

Esta oportunidad indica las páginas en las que el contenido adicional de preguntas y respuestas podría ajustarse mejor a la intención del usuario y las indicaciones en la detección basada en la IA. Para cada página, propone bloques de preguntas frecuentes generados por IA vinculados a la intención del usuario y al contenido de la página. Con Optimizar en Edge, estas preguntas frecuentes se insertan en el HTML, lo que hace que su página sea más compatible con la IA y aumenta la probabilidad de que las respuestas con IA reflejen directamente sus indicaciones.

### Simplificar contenido complejo

Esta oportunidad encuentra páginas con párrafos largos y complejos que pueden reducir la comprensión de la IA. Para cada página que supera los umbrales de legibilidad, crea contenido generado por IA que es más sencillo y fácil de analizar, conservando al mismo tiempo el significado original. Cuando se implementa en el perímetro, el contenido simplificado que se entrega al tráfico agéntico ayuda a los LLM a interpretar y resumir el contenido con mayor fiabilidad.

## Optimización automática en Edge

Para cada oportunidad, puede obtener una vista previa, editar, implementar, ver en directo y restablecer las optimizaciones en el perímetro.

>[!VIDEO](https://video.tv.adobe.com/v/3477987/?captions=spa&learn=on&enablevpops)

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

Servimos la versión optimizada de su página desde la caché siempre y cuando la página de origen subyacente no haya cambiado. Sin embargo, cuando el origen cambia para **Recuperar Visibilidad del contenido**, nuestro sistema se actualiza automáticamente para que los agentes de IA siempre reciban el contenido más actualizado. Esto se debe a que utilizamos la configuración de tiempo de duración de caché (TTL) bajo (por orden de minutos) para que cualquier actualización de contenido en su sitio déclencheur una nueva optimización dentro de esa ventana. Para oportunidades de contenido como **Agregar resúmenes compatibles con LLM**, LLM Optimizer supervisa la página de origen en busca de cambios. Si se detecta un cambio, pausamos la optimización y la marcamos para que sea analizada por humanos a fin de evitar que el contenido se desplace entre la página visible del agente y la página visible por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. ¿Optimize at Edge solo es para sitios que utilizan Adobe Edge Delivery Service (EDS)?

No. Optimizar en Edge no depende de la red de distribución de contenido (CDN) y funciona con cualquier arquitectura front-end, no solo con las implementadas en la pila EDS de Adobe.

P. ¿En qué se diferencia el procesamiento previo de Optimizar en Edge del procesamiento tradicional del lado del servidor (SSR)?

Ambos resuelven diferentes problemas y pueden trabajar juntos. El SSR tradicional procesa contenido del lado del servidor, pero no incluye contenido cargado posteriormente en el explorador. El procesamiento previo de Optimizar en Edge captura la página después de que JavaScript y los datos del lado del cliente se hayan cargado, lo que produce la versión completamente ensamblada en el perímetro de CDN. SSR se centra en mejorar la experiencia humana y Optimizar en Edge mejora la experiencia web para los LLM.

P. ¿Qué sucede si implemento optimizaciones para algunas direcciones URL de mi dominio, pero no para todas?

Solo se modifican las direcciones URL que se hayan optimizado explícitamente. Para las direcciones URL con oportunidades implementadas, los agentes de IA reciben la versión optimizada. Para las URL sin oportunidades implementadas, nuestro servicio simplemente envía la página original tal cual sin aplicar cambios ni almacenarla en nuestra capa de caché de optimización. Esto garantiza que pueda implementar las optimizaciones de forma selectiva sin afectar al resto del sitio.
