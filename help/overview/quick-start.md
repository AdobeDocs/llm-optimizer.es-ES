---
title: Inicio rápido
description: 'Empiece a utilizar Adobe LLM Optimizer: incorpore su marca, obtenga información sobre la visibilidad basada en la IA y explore los paneles de control para mejorar el rendimiento de las búsquedas.'
feature: Quickstart, Onboarding
source-git-commit: 82830e66d43ddd9741617cdf6daab63cd259554b
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 93%

---


# Inicio rápido

Para comenzar con LLM Optimizer, debe completar el proceso de incorporación como se detalla en los pasos que se presentan a continuación. Una vez que complete el proceso, tendrá acceso completo a [los paneles de control de LLM Optimizer](/help/dashboards/dashboards-overview.md) y a otras funcionalidades.

## Información general sobre la incorporación

El proceso de incorporación comienza con la incorporación de su dominio. El proceso es diferente en función de si es cliente de AEM Cloud o no. Una vez completado el proceso, deberá proporcionar información para el reenvío de registros de CDN y, finalmente, personalizar categorías, temas e indicaciones. A continuación, se detalla cada parte del proceso junto con sugerencias útiles sobre cómo empezar a usar LLM Optimizer lo antes posible.

### Permitir que Adobe LLM Optimizer acceda a las páginas públicas

Para ofrecer contenido preciso y recomendaciones técnicas, Adobe LLM Optimizer requiere acceso a sus páginas públicas. Esto se logra mediante un rastreador interno seguro (agente de usuario Spacecat/1.0).

Requisitos de configuración:

* Añada el agente de usuario Spacecat/1.0 a la lista de permitidos en el archivo robots.txt del sitio o las reglas de administración de tráfico de bots
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o de CDN. Las páginas bloqueadas no se pueden indexar, lo que significa que no se pueden generar tareas de optimización ni información sobre ellas.

Si la visibilidad del contenido aparece baja en el panel de control, compruebe que el rastreador tenga acceso a sus dominios. El acceso restringido es una causa frecuente de una indexación incompleta.

## Paso 1: Incorporar su dominio

### Probar antes de comprar

Los clientes de AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) tienen la opción de usar la oferta **Probar antes de comprar**. Es una versión de prueba gratuita de LLM Optimizer con hasta 200 indicaciones gratuitas. El uso de más de 200 indicaciones requiere un contrato de licencia independiente. El acceso se proporciona “tal cual” y “según disponibilidad”, y Adobe puede modificarlo, limitarlo o eliminarlo en cualquier momento.

Hay algunas funcionalidades del producto que no están disponibles en la versión gratuita:

* La prueba está limitada a un dominio. No podrá cambiar el dominio que ha proporcionado después de completar la configuración.
* La capacidad de implementar optimizaciones está disponible en Acceso anticipado. Más información en [Optimizar en las preguntas más frecuentes de Edge](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Consulte la sección siguiente para obtener información detallada sobre cómo activar la versión de prueba gratuita e incorporar su dominio.

### Clientes de AEM Cloud

Si es cliente de AEM Cloud, tiene la opción de probar LLM Optimizer usando la tarjeta de anuncio del producto en [Experience Hub](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Las indicaciones añadidas recientemente no aparecerán en el [panel de control Presencia de marca](/help/dashboards/brand-presence.md) hasta que se complete el procesamiento. Los clientes de AEM Cloud pueden utilizar la versión de prueba gratuita de LLM Optimizer. El uso de más de 200 indicaciones requiere un contrato de licencia independiente. El acceso se proporciona “tal cual” y “según disponibilidad”, y Adobe puede modificarlo, limitarlo o eliminarlo en cualquier momento. Póngase en contacto con el representante de su cuenta para obtener más información.

![Versión de prueba de LLM Optimizer](/help/overview/assets/llm-trial.png)

Cuando haga clic en el botón **Probar LLM Optimizer**, se le redirigirá a [https://llmo.now](https://llmo.now). A continuación, se le solicitará que inicie sesión mediante IMS. Cuando haya iniciado la sesión, iniciará el proceso de incorporación proporcionando un dominio y el nombre de la marca.

![Dominio de LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>El dominio que proporcionó será utilizado por todas las personas de su organización y no se podrá cambiar.

Se generará un pequeño conjunto de categorías, temas e indicaciones durante la fase de incorporación. El análisis de la presencia de marca de esas indicaciones estará disponible poco después de que se haya incorporado el sitio.

<!--![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)-->

Además, deberá configurar el [reenvío de registros de CDN](#step-4) para el análisis del tráfico. LLM Optimizer requiere datos de presencia de marca e información del tráfico agéntico y el tráfico de referencia para identificar las oportunidades y ofrecer recomendaciones prescriptivas para mejorar la visibilidad basada en la IA.

### Clientes que no son de AEM Cloud

Una vez finalizado el acuerdo empresarial, se incorporará con el dominio que desee incorporar en LLM Optimizer. Una vez completada esta incorporación, podrá iniciar sesión en LLM Optimizer en [https://llmo.now](https://llmo.now).

## Paso 2: Personalizar categorías, temas e indicaciones

Una vez incorporado el sitio, podrá ver el análisis de Presencia de marca en función del pequeño conjunto de indicaciones que se generaron automáticamente durante la fase de incorporación. A partir de ahora, podrá personalizar las categorías, los temas y las indicaciones de su marca. Esta configuración se crea en el [panel de control Configuración del cliente](/help/dashboards/customer-configuration.md).

![Panel de control Configuración del cliente](/help/overview/assets/prompt-creation.png)

Desde este panel de control, puede realizar lo siguiente:

* Añadir **nuevas categorías** que se ajusten a las prioridades de su empresa Las categorías pueden ser amplias áreas de contenido relevantes para su dominio.
* Escribir **temas personalizados** o subtemas de los que quiera realizar un seguimiento. Los temas pueden ser temas específicos vinculados a palabras clave sin marca de gran volumen asociadas con su dominio.
* Crear **sus indicaciones** para supervisar la visibilidad en consultas específicas. Las indicaciones son consultas (con y sin marca) que proporcionan una visibilidad de línea de base. Solo se generará automáticamente un número limitado de indicaciones en función de las categorías y los temas que haya proporcionado.
* Definir la mención de los **alias** para asegurarse de que se capturen y se contabilicen todas las menciones de una marca.
* Definir los **otros alias** para realizar un seguimiento preciso de otras marcas.

>[!NOTE]
>Las indicaciones exactas que solicite a los LLM no están disponibles porque los LLM no las revelan.

>[!NOTE]
>
> Para obtener información detallada sobre cómo configurar las categorías, temas e indicaciones, consulte la página [Prácticas recomendadas para configurar categorías, temas e indicaciones](/help/overview/best-practices-topics-prompts.md).

## Paso 3: Información sobre la Presencia de marca

Una vez incorporado el dominio, obtendrá información inicial en la vista Presencia de marca en función de las indicaciones que se generaron automáticamente durante la incorporación. Una vez que haya personalizado sus propias categorías, temas e indicaciones, LLM Optimizer activará automáticamente el análisis de Presencia de marca en función de las indicaciones que haya proporcionado, y los resultados estarán disponibles al cabo de 24 horas.

## Paso 4: Proporcionar información para el reenvío de registros de CDN {#step-4}

Para obtener información sobre el tráfico agéntico y el tráfico de referencia, deberá proporcionar información para el reenvío de registros de CDN. La puede añadir desde el [panel de control Configuración del cliente](/help/dashboards/customer-configuration.md#cdn-configuration) navegando hasta la pestaña **Configuración de CDN** y haciendo clic en **Incorporar CDN**.

![CDN de configuración del cliente](/help/overview/assets/cc-cdn.png)

O bien, si no se ha añadido ningún proveedor de CDN previamente (tal como se ha descrito anteriormente), se le pedirá que añada el reenvío de registros de CDN al acceder a los paneles de control Tráfico de agéntico y Tráfico de referencia por primera vez. Para obtener más información, consulte lo siguiente:

* [Tráfico agéntico](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfico de referencia](/help/dashboards/referral-traffic.md#setup#setup)

## Paso 5: Explorar paneles de control y realizar acciones

Después de proporcionar información para el reenvío de registros de CDN, podrá hacer lo siguiente:

* Ver el panel de control [Presencia de marca](/help/dashboards/brand-presence.md), ver su puntuación de visibilidad y realizar un seguimiento de su rendimiento en relación con otras marcas.
* Explorar los paneles de control [Tráfico agéntico](/help/dashboards/agentic-traffic.md) y [Tráfico de referencia](/help/dashboards/referral-traffic.md), si se ha configurado el reenvío de registros de CDN.
* Usar [Oportunidades](/help/dashboards/opportunities.md) para identificar contenido y mejoras técnicas.
* Exportar datos y colaborar con su equipo o invitar a su compañero de trabajo para que utilice el producto.

Por último, para comprender completamente las capacidades de LLM Optimizer, debería explorar todos los [paneles de control](/help/dashboards/dashboards-overview.md) disponibles.
