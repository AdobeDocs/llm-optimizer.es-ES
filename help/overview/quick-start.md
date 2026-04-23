---
title: Inicio rápido
description: Aprenda a incorporar su nombre de marca y dominio, activar la versión de prueba desde Experience Hub o Experience Cloud y completar la configuración de Adobe LLM Optimizer.
feature: Quickstart, Onboarding
source-git-commit: d38cf066ca1e3785032b7beca1c257e3a42f532b
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 37%

---


# Inicio rápido

Para empezar a usar LLM Optimizer, complete la incorporación. A continuación, personalice las categorías, los temas y las indicaciones, configure el reenvío de registros de CDN y abra los [paneles](/help/dashboards/dashboards-overview.md) para obtener información más detallada.

**Experiencia centrada en la marca:** De manera predeterminada, los nuevos clientes comienzan en una interfaz enfocada y de primera categoría con una configuración basada en la incorporación. En esta nueva interfaz, cada organización comienza con una marca activa y marcas sugeridas adicionales para elegir. Los clientes existentes de LLM Optimizer cambiarán gradualmente a esta experiencia centrada en la marca.

<!--Where steps differ by layout, use **Customer Configuration (classic experience)** or **Brands Management** / **Prompts Management**, whichever matches your current interface.-->

## Información general sobre la incorporación

El proceso de incorporación comienza con la incorporación de su dominio y su nombre de marca. A continuación se detalla cada parte del recorrido de incorporación, junto con sugerencias útiles sobre cómo empezar a usar LLM Optimizer lo antes posible.

### Permitir que Adobe LLM Optimizer acceda a las páginas públicas

Para ofrecer contenido preciso y recomendaciones técnicas, Adobe LLM Optimizer requiere acceso a sus páginas públicas. Esto se logra mediante un rastreador interno seguro (agente de usuario Spacecat/1.0).

Requisitos de configuración:

* Añada el agente de usuario Spacecat/1.0 a la Lista de permitidos del archivo robots.txt del sitio o a las reglas de administración de tráfico de bots.
* Asegúrese de que las páginas no estén bloqueadas en el nivel de dominio o de CDN. Las páginas bloqueadas no se pueden indexar, lo que significa que no se pueden generar tareas de optimización ni información sobre ellas.

Si la visibilidad del contenido aparece baja en el panel de control, compruebe que el rastreador tenga acceso a sus dominios. El acceso restringido es una causa frecuente de una indexación incompleta.

## Paso 1: Incorporar su nombre de marca y dominio {#step-1-onboard-your-domain}

Para empezar a usar LLM Optimizer, primero active la versión de prueba (si cumple los requisitos) e incorpore su nombre de marca y dominio.

### Activar la versión de prueba

El flujo de activación difiere según el producto de Adobe.

#### Clientes de AEM Cloud

Para activar la versión de prueba, como cliente de AEM Cloud, puede:

* Vaya a [Experience Hub](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) y use la tarjeta Anuncio del producto para activar LLM Optimizer. Después de seleccionar **Probar LLM Optimizer**, se le redirigirá a [https://llmo.now](https://llmo.now). Inicie sesión a través de IMS y, a continuación, introduzca un dominio y un nombre de marca para iniciar el proceso de incorporación.
* O ve directamente a [https://llmo.now](https://llmo.now) e inicia sesión.

![Versión de prueba de LLM Optimizer](/help/overview/assets/llm-trial.png)

#### clientes de Adobe Analytics

Si es cliente de Adobe Analytics, verá un banner en la página de inicio de Experience Cloud.

![Página de inicio de Experience Cloud con el titular Iniciar la versión de prueba de Adobe LLM Optimizer](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

Puede activar la versión de prueba de una de las siguientes maneras:

* Select **Start your Adobe LLM Optimizer Trial** in the banner.
* Go directly to [https://llmo.now](https://llmo.now) and sign in.

Once the trial is active, proceed with onboarding your brand name and domain.

>[!NOTE]
>
> * **Free trial:** AEM Cloud and Adobe Analytics customers can use the free trial version of LLM Optimizer.
> * **Customers who activate the trial on or after April 1, 2026** can use up to 100 prompts, one domain, and can deploy optimizations across up to 10 URLs for a single opportunity type.
> * **Customers who activated the trial before April 1, 2026** continue to have access to up to 200 prompts under their existing terms.
>
>Use beyond the included limits requires a separate license agreement. Access is provided on an &quot;as-is&quot; and &quot;as-available&quot; basis, and may be modified, limited or removed at any time. Contact your account representative for more information.

#### Onboard your brand name and domain

Onboard your brand name and domain to begin using LLM Optimizer.

1. Enter your brand name and the associated domain.

   * This should be the main domain where you want to analyze and optimize content.

1. Complete onboarding.

   * Once submitted, LLM Optimizer begins analyzing your domain and generating insights.

![Dominio de LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>Las indicaciones añadidas recientemente no aparecerán en el [panel de control Presencia de marca](/help/dashboards/brand-presence.md) hasta que se complete el procesamiento.

>[!NOTE]
>El dominio que proporcionó será utilizado por todas las personas de su organización y no se podrá cambiar.

Se generará un pequeño conjunto de categorías, temas e indicaciones durante la fase de incorporación. El análisis de la presencia de marca de esas indicaciones estará disponible poco después de que se haya incorporado el sitio.

The ability to deploy optimizations at edge is also available. Learn more in [Optimize at Edge — Frequently asked questions](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Additionally, configure [CDN log forwarding](#step-4) for traffic analysis. LLM Optimizer requires Brand Presence data and insights from agentic and referral traffic to identify opportunities and provide prescriptive recommendations that boost AI visibility.

### Non-AEM Cloud customers

After your organization finalizes the business agreement, you are onboarded to LLM Optimizer with the domain your organization selected. When onboarding finishes, sign in at [https://llmo.now](https://llmo.now).

## Paso 2: Personalizar categorías, temas e indicaciones {#step-2-customize-categories-topics-and-prompts}

Una vez incorporado el sitio, podrá ver el análisis de Presencia de marca en función del pequeño conjunto de indicaciones que se generaron automáticamente durante la fase de incorporación. Moving forward, you can customize categories, topics, and prompts for your brand.

### Customer Configuration (classic navigation)

If you are using classic navigation (not the Brand Centric experience), you can customize categories, topics, and prompts for your brand from the [customer configuration dashboard](/help/dashboards/customer-configuration.md).

![Panel de control Configuración del cliente](/help/overview/assets/prompt-creation.png)

En el panel de configuración del cliente, puede:

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

### Experiencia centrada en la marca

Para los clientes que se encuentran en la experiencia centrada en la marca, puede agregar categorías, temas y preguntas de la siguiente manera:

* **Categorías** — Vaya a **Administración de marcas** y haga clic en **Categorías**. Las categorías se definen a nivel global y se aplican a todas las marcas en Administración de marcas.

  ![Administración de marcas con categorías en la navegación](/help/assets/brand-centric-experience/llmo-app-shell.png)

* **Temas e indicadores** — Vaya a **Administración de indicadores** para crear temas e indicadores, incluidos indicadores para una marca específica.

  ![Administración de indicadores](/help/assets/brand-centric-experience/prompts-management.png)

## Paso 3: Información sobre la Presencia de marca

Una vez incorporado el dominio, obtendrá información inicial en la vista Presencia de marca en función de las indicaciones que se generaron automáticamente durante la incorporación. Una vez que haya personalizado sus propias categorías, temas e indicaciones, LLM Optimizer activará automáticamente el análisis de Presencia de marca en función de las indicaciones que haya proporcionado, y los resultados estarán disponibles al cabo de 24 horas.

>[!NOTE]
>
> Para los clientes que están en la experiencia centrada en la marca, vaya a **Presencia de marca** y seleccione la marca para la que desee ver la Presencia de marca mediante el menú desplegable de marca. También puedes ver la visibilidad de la marca a un nivel de **Todas las marcas** con esta experiencia.

## Paso 4: Proporcionar información para el reenvío de registros de CDN {#step-4}

Para desbloquear las perspectivas de tráfico y Tráfico de referencia del agente, registre el reenvío de registros de CDN para que LLM Optimizer pueda leer sus registros de acceso.

### Configuración del cliente (navegación clásica)

Si utiliza la navegación clásica, puede agregar información de reenvío de registros de CDN desde el [panel de configuración del cliente](/help/dashboards/customer-configuration.md#cdn-configuration). Abra la pestaña **Configuración de CDN** y seleccione **CDN integrada**.

![CDN de configuración del cliente](/help/overview/assets/cc-cdn.png)

O bien, si no se ha añadido ningún proveedor de CDN previamente (tal como se ha descrito anteriormente), se le pedirá que añada el reenvío de registros de CDN al acceder a los paneles de control Tráfico de agéntico y Tráfico de referencia por primera vez. Para obtener más información, consulte lo siguiente:

* [Tráfico agéntico](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfico de referencia](/help/dashboards/referral-traffic.md#setup)

>[!NOTE]
>Para obtener más información sobre el reenvío de registros al usar una CDN administrada por el cliente (BYOCDN), consulte [Información general sobre el reenvío de registros BYOCDN](/help/overview/log-forwarding/log-forwarding-overview.md)

### Experiencia centrada en la marca

Para los clientes que están en la experiencia centrada en la marca, puede agregar la información de reenvío de registro de CDN de **Brands Management** de la siguiente manera: abra **Brands Management** y haga clic en la etiqueta **CDN**.

![Gestión de marcas — Reenvío de registros de CDN](/help/assets/brand-centric-experience/brands-management-cdn.png)

## Paso 5: Explorar paneles de control y realizar acciones

Después de proporcionar información para el reenvío de registros de CDN, podrá hacer lo siguiente:

* Ver el panel de control [Presencia de marca](/help/dashboards/brand-presence.md), ver su puntuación de visibilidad y realizar un seguimiento de su rendimiento en relación con otras marcas.
* Explore los paneles de [Agentic](/help/dashboards/agentic-traffic.md) y [Tráfico de referencia](/help/dashboards/referral-traffic.md), si se ha configurado el reenvío de registros de CDN.
* Usar [Oportunidades](/help/dashboards/opportunities.md) para identificar contenido y mejoras técnicas.
* Exportar datos y colaborar con su equipo o invitar a su compañero de trabajo para que utilice el producto.

>[!NOTE]
> En la experiencia de Brand Centric, acceda a la vista deseada desde la sección de navegación a la izquierda.

Por último, para comprender completamente las capacidades de LLM Optimizer, debería explorar todos los [paneles de control](/help/dashboards/dashboards-overview.md) disponibles.
