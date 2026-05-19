---
title: Errores del tráfico agéntico
description: Descubra cómo LLM Optimizer detecta los errores HTTP que encuentran los agentes de IA al rastrear su sitio y cómo corregirlos para mejorar la accesibilidad del contenido y la visibilidad de la IA.
feature: Opportunities
autotag-review: '2026-05-15T17:32:31.900Z'
TQID: 'https://experienceleague.adobe.com/9Gbva-14SNt8A0G0B2Qu26OOp34L5NaM0z6lCv4yrTg'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1045
ht-degree: 100%

---


# Errores del tráfico agéntico

Los agentes de IA que rastrean su sitio se encuentran con los mismos errores HTTP que los exploradores humanos, pero las consecuencias son diferentes. Cuando un agente de IA detecta un error 404, 403 o 5xx, no puede acceder a ese contenido ni citarlo, lo que reduce directamente la visibilidad de su marca en las respuestas generadas por IA.

La oportunidad de Errores del tráfico agéntico monitoriza los registros de CDN en busca de errores HTTP devueltos a los agentes de IA y muestra las direcciones URL afectadas junto con sus volúmenes de visitas y sugerencias de correcciones. Incluye tres tipos de error, cada uno con su propia oportunidad en el panel de control:

- **404 No encontrado**: vínculos rotos que impiden que los agentes de IA tengan acceso al contenido que ya no existe en la dirección URL prevista.
- **403 Prohibido**: restricciones de acceso que bloquean el acceso de los rastreadores de IA a contenidos a los que deberían poder acceder.
- **Errores del servidor 5xx**: inestabilidad del lado del servidor que impide que el contenido esté disponible de forma temporal o permanente para los agentes de IA.

Cada tipo de error puede aparecer como una oportunidad independiente en el panel de control, según los errores que se detecten en el sitio.

La oportunidad también presenta dos métricas clave para cada tipo de error:

- **Total de URL**: número de URL únicas que devuelven errores a los agentes de IA.
- **Total de visitas**: número total de respuestas de error registradas en todas las solicitudes del agente de IA.

![Panel de control Errores del tráfico agéntico que muestra las métricas de resumen y los detalles del error](/help/dashboards/opportunities/assets/agentic-traffic-errors-overview.png)

## Funcionamiento

LLM Optimizer consulta los registros de CDN a través de Athena para identificar las direcciones URL que devuelven códigos de estado 404, 403 o 5xx a los agentes de usuario del agente de IA. Los agentes de usuario incluyen ChatGPT, Claude, Perplexity y Gemini. Se analizan y clasifican hasta 500 direcciones URL por auditoría según el volumen de tráfico. La auditoría se ejecuta semanalmente de forma predeterminada.

Las direcciones URL se validan antes de mostrarse para filtrar los falsos positivos y los datos obsoletos. LLM Optimizer vuelve a probar cada URL para confirmar su estado actual y compara las respuestas del agente de IA con las respuestas del explorador humano para identificar problemas específicos del rastreador.

Para los **errores 404**, las sugerencias funcionan con tecnología de IA. Como tal, LLM Optimizer analiza la estructura y el contenido de la URL dañada para recomendar URL alternativas que preserven la intención del usuario, junto con una puntuación de confianza y un motivo que explique la recomendación.

Para los errores **403 y 5xx**, las sugerencias se basan en plantillas y ofrecen directrices específicas para cada tipo de error.

## Tabla Detalles del error

La tabla de detalles del error enumera todas las direcciones URL afectadas, filtradas por **Agente de usuario**, **Código de país** y **Categoría**. Para cada URL se muestra lo siguiente:

- **URL**: la página afectada.
- **Total**: número total de visitas de error de los agentes de IA.
- Las visitas semanales de las últimas semanas, para que pueda realizar un seguimiento si el problema persiste o mejora.

![Tabla de detalles del error con filtros y columnas de visitas semanales](/help/dashboards/opportunities/assets/agentic-traffic-errors-table.png)

## Detalles de sugerencias

Al hacer clic en cualquier sugerencia, se abre el panel **Detalles de sugerencias**, que muestra lo siguiente:

- La URL afectada y la acción recomendada: por ejemplo, “Debe ser una URL válida o redireccionar a una URL alternativa”.
- Un gráfico de **estadísticas** que muestra el total de visitas por semana realizadas por el agente de usuario del agente de IA, para que pueda comprender el impacto del tráfico y si el problema persiste o mejora.
- Acciones **Compartir** y **Descartar** para administrar la sugerencia.

![Panel de detalles de sugerencias para un 404 con gráfico de estadísticas](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion.png)

En algunos casos **5xx** (y similares), el panel puede anotar cuándo no hay direcciones URL alternativas del mismo dominio disponibles y explicar cómo las recomendaciones siguen las reglas de dominios y listas. Por ejemplo, sugerir la URL del dominio base para conservar el valor SEO cuando no se pueda ofrecer una coincidencia más cercana.

![Panel Detalles de sugerencias para un error del servidor con mensajes explicativos](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion-503.png)

## Cómo solucionarlo

La corrección depende del tipo de error:

**Errores 404**: la sugerencia incluye una o más direcciones URL alternativas recomendadas por la IA, basadas en la estructura y el contenido de la dirección URL dañada, junto con una puntuación de confianza y un motivo. Implemente una redirección del lado del servidor de la URL dañada a la alternativa sugerida para restaurar el acceso del agente de IA y preservar la capacidad de detección del contenido.

**Errores 403**: revise los permisos de acceso para asegurarse de que no se bloquee el acceso de los rastreadores de IA al contenido al que deberían poder acceder En concreto, las siguientes:
- Revise los permisos de acceso: rastreador de IA bloqueado.
- Compruebe que la configuración de seguridad no bloquea los rastreadores legítimos.

**Errores 5xx**: investigue los problemas del lado del servidor que afectan a las páginas marcadas. En concreto, las siguientes:
- Investigue la estabilidad del servidor en las páginas con mucho tráfico.
- Compruebe los registros de la aplicación para ver si hay errores recurrentes.
- Monitorice el estado y la capacidad de la infraestructura.

## Probar en la demostración

Vea la oportunidad Errores de tráfico agéntico en acción usando el entorno de demostración de Frescopa.

- [Ver errores 404 en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-4xxs)
- [Ver errores 5xx en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-5xxs)

## Preguntas frecuentes

**¿Por qué los errores HTTP son importantes para la visibilidad de IA?**

En los sistemas de generación aumentada por recuperación, los rastreadores de IA descubren vínculos e intentan recuperar el contenido de la página para incluirlo en sus respuestas. Si falta una página, devuelve un error o no se puede acceder a ella, su contenido no se puede recuperar ni citar. La corrección de estos errores técnicos mejora directamente la probabilidad de que los sistemas de IA indexen y citen correctamente el contenido.

**¿Cuál es la diferencia entre un error 404 y un error 403?**

Un error 404 significa que la página no existe en la dirección URL solicitada: se ha eliminado o trasladado sin redireccionamiento. Un error 403 significa que la página existe, pero se está denegando el acceso a todas las rastreadores o, específicamente, a los agentes de IA. Ambos impiden que los agentes de IA accedan al contenido, pero la corrección es diferente para cada uno.

**¿Por qué un error 403 podría afectar solamente a los agentes de IA y no a los visitantes humanos?**

Algunas configuraciones de seguridad o de control de acceso pueden bloquear el acceso al contenido de los agentes de usuario del agente de IA al que los visitantes humanos pueden acceder normalmente. LLM Optimizer marca específicamente estos casos comparando las respuestas del agente de IA con las respuestas del explorador humano.

**¿Cómo se filtran los falsos positivos?**

LLM Optimizer vuelve a probar las direcciones URL para confirmar su estado actual antes de mostrarlas como sugerencias y compara las respuestas del agente de IA con las respuestas del explorador humano para identificar problemas específicos del rastreador. No se muestran las direcciones URL que ya no devuelven errores.

**¿Con qué frecuencia se actualiza el análisis?**

La auditoría se ejecuta semanalmente de forma predeterminada, extrayendo datos de error de los registros de CDN de la semana anterior. En la tabla de detalles del error se muestran todas las visitas semanales para que pueda rastrear las tendencias a lo largo del tiempo.

**¿Qué agentes de IA se monitorizan?**

LLM Optimizer monitoriza las respuestas de error de todos los patrones de agente de usuario del agente de IA detectados, incluidos los rastreadores ChatGPT, Claude, Perplexity y Gemini.
