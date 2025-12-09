---
title: Inicio rápido
description: 'Empiece con Adobe LLM Optimizer: Incorpore su marca, desbloquee las perspectivas de visibilidad de la IA y explore los paneles para mejorar el rendimiento de la búsqueda.'
feature: Quickstart, Onboarding
source-git-commit: 24183fbe2577bb9402f8b6aaaf1e46c75403383d
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---


# Inicio rápido

Para comenzar con el optimizador LLM, debe completar el proceso de incorporación como se detalla en los pasos que se presentan a continuación. Una vez que complete el proceso, tendrá acceso completo a [los paneles de LLM Optimizer](/help/dashboards/dashboards-overview.md) y otras funcionalidades.

## Resumen de incorporación

El proceso de incorporación comienza con la incorporación de su dominio. El proceso es diferente en función de si es cliente de AEM Cloud o no. Una vez completado el proceso, deberá proporcionar información para el Reenvío de registros de CDN y, finalmente, personalizar categorías, temas y peticiones de datos. A continuación, se detalla cada parte del proceso junto con sugerencias útiles sobre cómo empezar a usar LLM Optimizer lo antes posible.

### Permitir que Adobe LLM Optimizer acceda a páginas públicas

Para ofrecer contenido preciso y recomendaciones técnicas, Adobe LLM Optimizer requiere acceso a sus páginas públicas. Esto se logra a través de un rastreador interno seguro (agente de usuario de Spacecat/1.0).

Requisitos de configuración:

* Añada el agente de usuario Spacecat/1.0 a la Lista de permitidos del archivo robots.txt del sitio o a las reglas de administración de tráfico de bots
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o CDN. Las páginas bloqueadas no se pueden indexar, lo que significa que no se pueden generar tareas de optimización y perspectivas para ellas.

Si la visibilidad del contenido aparece baja en el panel, compruebe que el rastreador tenga acceso a sus dominios. El acceso restringido es una causa frecuente de indexación incompleta.

## Paso 1: Incorporar su dominio

### Pruebe antes de comprar

Los clientes de AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) tienen la opción de usar la oferta **Probar antes de comprar**. Es una versión de prueba gratuita de LLM Optimizer con hasta 200 mensajes gratuitos. El uso de más de 200 peticiones de datos requiere un contrato de licencia independiente. El acceso se proporciona &quot;tal cual&quot; y &quot;según esté disponible&quot;, y Adobe puede modificarlo, limitarlo o eliminarlo en cualquier momento.

Hay algunas funciones del producto que no están disponibles en la versión gratuita:

* La prueba está limitada a un dominio. No podrá cambiar el dominio que ha proporcionado después de completar la configuración.
* La compatibilidad con la implementación de optimizaciones no estará disponible.

Consulte la sección siguiente para obtener detalles sobre cómo activar la versión de prueba gratuita e incorporar su dominio.

### Clientes de AEM Cloud

Si eres cliente de AEM Cloud, tienes la opción de probar LLM Optimizer usando la tarjeta Anuncio del producto en [Experience Hub](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Las solicitudes agregadas recientemente no aparecerán en el [Tablero de presencia de marca](/help/dashboards/brand-presence.md) hasta que se complete el procesamiento. Los clientes de AEM Cloud pueden utilizar la versión de prueba gratuita de LLM Optimizer. El uso de más de 200 peticiones de datos requiere un contrato de licencia independiente. El acceso se proporciona &quot;tal cual&quot; y &quot;según esté disponible&quot;, y Adobe puede modificarlo, limitarlo o eliminarlo en cualquier momento. Póngase en contacto con el representante de su cuenta para obtener más información.

![Prueba de LLM Optimizer](/help/overview/assets/llm-trial.png)

Una vez que hagas clic en el botón **Probar LLM Optimizer**, se te redirigirá a [https://llmo.now](https://llmo.now). A continuación, se le pedirá que inicie sesión mediante IMS. Una vez que inicie sesión, iniciará el proceso de incorporación proporcionando un dominio y el nombre de la marca.

![Dominio de LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>El dominio que ha proporcionado será utilizado por todos los miembros de su organización y no se puede cambiar.

Se generará un pequeño conjunto de categorías, temas y mensajes durante la fase de incorporación. El análisis de presencia de marca en esas indicaciones estará disponible poco después de que se haya incorporado el sitio.

<!--![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)-->

Además, también debe configurar el [reenvío de registros de CDN](#step-4) para el análisis del tráfico. LLM Optimizer requiere datos de presencia de marca y perspectivas del tráfico agéntico y de referencia para identificar oportunidades y proporcionar recomendaciones prescriptivas para impulsar la visibilidad de la IA.

### Clientes que no son de AEM Cloud

Una vez finalizado el acuerdo empresarial, se incorporará al dominio que desee incorporar en LLM Optimizer. Una vez completada esta incorporación, podrá iniciar sesión en LLM Optimizer a través de [https://llmo.now](https://llmo.now).

### Paso 2: Personalizar categorías, temas e indicadores

Una vez incorporado el sitio, puede ver el análisis de presencia de marca en función del pequeño conjunto de indicadores que se generaron automáticamente durante la fase de incorporación. Ahora puede personalizar las categorías, los temas y las peticiones de datos de su marca. Esta configuración se creó en el [panel de configuración del cliente](/help/dashboards/customer-configuration.md).

![Panel de configuración del cliente](/help/overview/assets/prompt-creation.png)

Desde este panel, puede:

* Agregue **nuevas categorías** que se ajusten a sus prioridades empresariales. Las categorías pueden ser áreas de contenido amplias relevantes para su dominio.
* Escriba **temas personalizados** o subtemas de los que quiera realizar un seguimiento. Los temas pueden ser temas específicos vinculados a palabras clave sin marca de gran volumen asociadas con su dominio.
* Cree **sus indicadores** para supervisar la visibilidad en consultas específicas. Los indicadores son consultas (con marca y sin marca) que proporcionan una visibilidad de línea de base. Solo se generará automáticamente un número limitado de mensajes en función de las categorías y los temas que haya proporcionado.
* Defina la mención **alias** para asegurarse de que todas las menciones de una marca se capturan y se contabilizan.
* Defina **otros alias** para rastrear otras marcas con precisión.

>[!NOTE]
>Los mensajes exactos que solicita a los LLM no están disponibles para el público porque no los revelan.

>[!NOTE]
>
> Para obtener más información sobre cómo configurar las categorías, temas y preguntas, consulte la página [Prácticas recomendadas para configurar categorías, temas y preguntas](/help/overview/best-practices-topics-prompts.md).

### Paso 3: Perspectivas de presencia de marca

Una vez incorporado el dominio, verá perspectivas iniciales en la vista Presencia de marca en función de los mensajes que se generaron automáticamente durante la incorporación. Una vez que haya personalizado sus propias categorías, temas y preguntas, LLM Optimizer almacenará automáticamente en déclencheur el análisis de presencia de marca en las preguntas que haya proporcionado y los resultados estarán disponibles en 24 horas.

### Paso 4: Proporcionar información para el reenvío de registros de CDN {#step-4}

Para desbloquear las perspectivas de tráfico agente y tráfico de referencia, debe proporcionar información para el reenvío de registros de CDN. Se puede agregar desde el [panel de configuración del cliente](/help/dashboards/customer-configuration.md#cdn-configuration) navegando a la pestaña **Configuración de CDN** y haciendo clic en **Incorporar CDN**.

![CDN de configuración de cliente](/help/overview/assets/cc-cdn.png)

Alternativamente, si no se ha agregado ningún proveedor de CDN previamente (como se ha descrito anteriormente), se le pedirá que agregue el reenvío de registros de CDN al acceder a los paneles de tráfico de agente y referencia por primera vez. Para obtener más información, consulte:

* [Tráfico de agente](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfico de referencia](/help/dashboards/referral-traffic.md#setup#setup)

### Paso 5: Explorar paneles y realizar acciones

Después de proporcionar información para el Reenvío de registros de CDN, puede:

* Vea el panel [Presencia de marca](/help/dashboards/brand-presence.md), vea su puntuación de visibilidad y realice un seguimiento de su rendimiento en relación con otras marcas.
* Explore los paneles de [Agente](/help/dashboards/agentic-traffic.md) y [Tráfico de referencia](/help/dashboards/referral-traffic.md), si se ha configurado el reenvío de registros de CDN.
* Use [Oportunidades](/help/dashboards/opportunities.md) para identificar contenido y mejoras técnicas.
* Exporte datos y colabore con su equipo o invite a su compañero a utilizar el producto.

Por último, para comprender completamente las capacidades de LLM Optimizer, debería explorar todos los [paneles](/help/dashboards/dashboards-overview.md) disponibles.
