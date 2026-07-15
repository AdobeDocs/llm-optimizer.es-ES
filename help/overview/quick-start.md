---
title: Inicio rápido
description: Aprenda a incorporar su nombre de marca y dominio, a activar la versión de prueba desde Experience Hub o Experience Cloud y a completar la configuración de Adobe LLM Optimizer.
feature: Quickstart, Onboarding
autotag-review: '2026-05-15T17:56:15.005Z'
TQID: 'https://experienceleague.adobe.com/ShjpvskyOoHqz88gorfhqbIdP5SWT9FJ9SfmjBgEm8E'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: b70f186a-2ef9-43ce-b452-25fa1d91bcda
source-git-commit: a5bfae0a2fecc48f8deb80394817002cfb7c1a32
workflow-type: tm+mt
source-wordcount: 1201
ht-degree: 87%

---


# Inicio rápido

Para empezar a usar LLM Optimizer, complete el proceso de incorporación. A continuación, personalice las categorías, los temas y las indicaciones, configure el reenvío de registros de CDN y abra los [paneles de control](/help/dashboards/dashboards-overview.md) para obtener información más detallada.

<!--Where steps differ by layout, use **Customer Configuration (classic experience)** or **Brands Management** / **Prompts Management**, whichever matches your current interface.-->

## Experiencia centrada en la marca {#brand-centric-experience}

De forma predeterminada, los clientes empiezan en una interfaz centrada en la marca con una configuración basada en la incorporación. En esta interfaz, cada organización comienza con una marca activa y marcas sugeridas adicionales para elegir. <!--Existing LLM Optimizer customers will shift to this Brand Centric experience gradually.-->

## Información general sobre la incorporación

El proceso de incorporación comienza con la incorporación de su dominio y su nombre de marca. Cada parte del recorrido de incorporación se detalla a continuación junto con sugerencias útiles sobre cómo empezar a utilizar LLM Optimizer lo antes posible.

### Permitir que Adobe LLM Optimizer acceda a las páginas públicas

Para ofrecer contenido preciso y recomendaciones técnicas, Adobe LLM Optimizer requiere acceso a sus páginas públicas. Esto se logra mediante un rastreador interno seguro (agente de usuario Spacecat/1.0).

Requisitos de configuración:

* Añada el agente de usuario Spacecat/1.0 a la lista de permitidos en el archivo robots.txt del sitio o las reglas de administración de tráfico de bots
* Asegúrese de que las páginas no estén bloqueadas a nivel de dominio o de CDN. Las páginas bloqueadas no se pueden indexar, lo que significa que no se pueden generar tareas de optimización ni información sobre ellas.

Si la visibilidad del contenido aparece baja en el panel de control, compruebe que el rastreador tenga acceso a sus dominios. El acceso restringido es una causa frecuente de una indexación incompleta.

## Paso 1: Añadir el nombre de marca y dominio {#step-1-onboard-your-domain}

Para empezar a utilizar LLM Optimizer, primero active la versión de prueba (si cumple los requisitos) e incorpore su nombre de marca y dominio.

### Active la versión de prueba

El flujo de activación es diferente según el producto de Adobe.

#### Clientes de AEM Cloud

Para activar la versión de prueba, como cliente de AEM Cloud, puede realizar las siguientes acciones:

* Vaya a [Experience Hub](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) y utilice la tarjeta Anuncio del producto para activar LLM Optimizer. Después de seleccionar **Probar LLM Optimizer**, se le redirigirá a [https://llmo.now](https://llmo.now). Inicie sesión a través de IMS y, a continuación, introduzca un dominio y un nombre de marca para iniciar el proceso de incorporación.
* O vaya directamente a [https://llmo.now](https://llmo.now) e inicie sesión.

![Versión de prueba de LLM Optimizer](/help/overview/assets/llm-trial.png)

#### ADOBE ANALYTICS y ADOBE CUSTOMER JOURNEY ANALYTICS

Para los clientes de Adobe Analytics y Adobe Customer Journey Analytics, verá un banner en la página de inicio de Experience Cloud.

![Página principal de Experience Cloud con el banner Iniciar la versión de prueba de Adobe LLM Optimizer](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

Puede activar la versión de prueba de una de las siguientes maneras:

* Seleccione **Iniciar la versión de prueba de Adobe LLM Optimizer** en el banner.
* Vaya directamente a [https://llmo.now](https://llmo.now) e inicie sesión.

Cuando la versión de prueba esté activa, prosiga con la incorporación del nombre de marca y el dominio.

>[!NOTE]
>
> * **Prueba gratuita:** Los clientes de AEM Cloud y Adobe Analytics/Customer Journey Analytics pueden usar la versión de prueba gratuita de LLM Optimizer.
> * **Los clientes que activen la versión de prueba a partir del 1 de abril de 2026** pueden utilizar hasta 100 indicaciones, un dominio y pueden implementar optimizaciones en un máximo de 10 direcciones URL para un único tipo de oportunidad.
> * **Los clientes que activaron la versión de prueba antes del 1 de abril de 2026** continuarán teniendo acceso a hasta 200 indicaciones de acuerdo con los términos existentes.
>
>El uso más allá de los límites incluidos requiere un acuerdo de licencia independiente. El acceso se proporciona “tal cual” y “según disponibilidad”, y Adobe puede modificarlo, limitarlo o eliminarlo en cualquier momento. Póngase en contacto con el representante de su cuenta para obtener más información.

#### Incorporar el nombre de marca y dominio

Incorpore su nombre de marca y dominio para empezar a utilizar LLM Optimizer.

1. Introduzca su nombre de marca y el dominio asociado.

   * Debe ser el dominio principal en el que desea analizar y optimizar el contenido.

1. Complete la incorporación.

   * Cuando lo haya enviado, LLM Optimizer empezará a analizar su dominio y a generar perspectivas.

![Dominio de LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>Las indicaciones añadidas recientemente no aparecerán en el [panel de control Presencia de marca](/help/dashboards/brand-presence.md) hasta que se complete el procesamiento.

>[!NOTE]
>El dominio que proporcionó será utilizado por todas las personas de su organización y no se podrá cambiar.

Se generará un pequeño conjunto de categorías, temas e indicaciones durante la fase de incorporación. El análisis de la presencia de marca de esas indicaciones estará disponible poco después de que se haya incorporado el sitio.

La posibilidad de implementar optimizaciones en el perímetro también está disponible. Más información en [Optimizar en Edge: preguntas frecuentes](https://experienceleague.adobe.com/es/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Asimismo, configure el [reenvío de registros de CDN](#step-4) para el análisis de tráfico. LLM Optimizer requiere datos sobre la Presencia de marca e información del tráfico agéntico y de referencia para identificar las oportunidades y ofrecer recomendaciones específicas que mejoren la visibilidad basada en la IA.

### Clientes que no son de AEM Cloud

Cuando la organización haya concluido el acuerdo empresarial, se le incorporará a LLM Optimizer con el dominio seleccionado por la organización. Cuando finalice la incorporación, inicie sesión en [https://llmo.now](https://llmo.now).

## Paso 2: Personalizar categorías, temas e indicaciones {#step-2-customize-categories-topics-and-prompts}

Una vez incorporado el sitio, podrá ver el análisis de Presencia de marca en función del pequeño conjunto de indicaciones que se generaron automáticamente durante la fase de incorporación. A partir de ahora, podrá personalizar las categorías, los temas y las indicaciones de su marca.

### Categorías, temas e indicaciones de la experiencia centrada en la marca

Puede agregar categorías, temas y peticiones de datos de la siguiente manera:

* **Categorías**: vaya a **Administración de marcas** y haga clic en **Categorías**. Las categorías se definen a nivel global y se aplican a todas las marcas en Administración de marcas.

  ![Administración de marcas con categorías en la navegación](/help/assets/brand-centric-experience/llmo-app-shell.png)

* **Temas e indicaciones**: vaya a **Administración de indicaciones** para crear temas e indicaciones, incluidas las indicaciones para una marca específica.

  ![Administración de indicaciones](/help/assets/brand-centric-experience/prompts-management.png)

>[!NOTE]
>Las indicaciones exactas que solicite a los LLM no están disponibles porque los LLM no las revelan.

>[!NOTE]
>
> Para obtener información detallada sobre cómo configurar las categorías, temas e indicaciones, consulte la página [Prácticas recomendadas para configurar categorías, temas e indicaciones](/help/overview/best-practices-topics-prompts.md).

## Paso 3: Información sobre la Presencia de marca

Una vez incorporado el dominio, obtendrá información inicial en la vista Presencia de marca en función de las indicaciones que se generaron automáticamente durante la incorporación. Una vez que haya personalizado sus propias categorías, temas e indicaciones, LLM Optimizer activará automáticamente el análisis de Presencia de marca en función de las indicaciones que haya proporcionado, y los resultados estarán disponibles al cabo de 24 horas.

Vaya a **Presencia de marca** y seleccione una marca de la cual quiera ver la Presencia de marca mediante la lista desplegable de marcas. También puede ver la visibilidad de la marca a un nivel de **Todas las marcas** con esta experiencia.

## Paso 4: Proporcionar información para el reenvío de registros de CDN {#step-4}

Para obtener información sobre el tráfico agéntico y el tráfico de referencia, registre el reenvío de registros de CDN para que LLM Optimizer pueda leer sus registros de acceso.

### Reenvío de registros de CDN

Puede agregar información de reenvío de registros de CDN desde **Brands Management** de la siguiente manera: abra **Brands Management** y haga clic en la etiqueta **CDN**.

![Administración de marcas: reenvío de registros de CDN](/help/assets/brand-centric-experience/brands-management-cdn.png)

>[!NOTE]
>Para obtener más información sobre el reenvío de registros al utilizar una CDN administrada por el cliente (BYOCDN), consulte [Información general sobre el reenvío de registros BYOCDN](/help/overview/log-forwarding/log-forwarding-overview.md)


## Paso 5: Explorar paneles de control y realizar acciones

Después de proporcionar información para el Reenvío de registros de CDN, puede acceder al panel deseado desde la sección de navegación a la izquierda.

* Ver el panel de control [Presencia de marca](/help/dashboards/brand-presence.md), ver su puntuación de visibilidad y realizar un seguimiento de su rendimiento en relación con otras marcas.
* Explore los paneles de control [Tráfico agéntico](/help/dashboards/agentic-traffic.md) y [Tráfico de referencia](/help/dashboards/referral-traffic.md), si se ha configurado el reenvío de registros de CDN.
* Usar [Oportunidades](/help/dashboards/opportunities-overview.md) para identificar contenido y mejoras técnicas.
* Exportar datos y colaborar con su equipo o invitar a su compañero de trabajo para que utilice el producto.

Por último, para comprender completamente las capacidades de LLM Optimizer, debería explorar todos los [paneles de control](/help/dashboards/dashboards-overview.md) disponibles.
