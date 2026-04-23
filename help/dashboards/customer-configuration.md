---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se monitorizará y analizará su marca dentro de la plataforma del optimizador de LLM.
feature: Customer Configuration
source-git-commit: 625807b8905f741aa89d551483d89cca2ef91873
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 37%

---


# Configuración del cliente {#customer-configuration}

El panel de control Configuración del cliente es una potente herramienta que proporciona perspectivas sobre la visibilidad de su marca en los LLM. Al configurar correctamente categorías, temas e indicaciones, puede asegurarse de que la marca esté bien posicionada para aparecer en las respuestas generadas por LLM. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

The Customer Configuration Dashboard (shown below) applies when your organization still uses this navigation.

![Panel de control Configuración del cliente](/help/dashboards/assets/customer-config.png)

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Indicaciones](#prompts-brand)
* [Categorías](#categories)
* [Otras marcas](#other-brands)
* [Alias de marca](#brand-aliases)
* [Configuración de la CDN](#agentic-cdn)
* [Consola de búsqueda de Google](#google-console)

If you are on the [Brand Centric experience](/help/overview/quick-start.md#brand-centric-experience), navigate to **Brands Management** to setup and configure brands, brand aliases and define competitors to track against. **Brands Management** is also used to configure integrations such as Google Search Console, Adobe Analytics, and CDN log forwarding related to URLs associated with brands. You can do this by clicking on the corresponding tabs: GSC, CDN and so on.

![Brands Management — app navigation (Brand Centric experience)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Brands Management — configuration overview (Brand Centric experience)](/help/assets/brand-centric-experience/brands-management-configuration.png)

>[!IMPORTANT]
>
> Para obtener información detallada sobre cómo configurar las categorías, temas e indicaciones, consulte la página [Prácticas recomendadas para configurar categorías, temas e indicaciones](/help/overview/best-practices-topics-prompts.md).

## Indicaciones {#prompts-brand}

From the **Prompts** tab, you can review, manage and customize prompts. Puede cargar un archivo .csv de [análisis de Presencia de marca](/help/dashboards/brand-presence.md), y la lista se rellenará con indicaciones y temas de ese análisis, o [descargar una biblioteca de indicaciones](/help/overview/best-practices-topics-prompts.md) creada por Adobe. También puede eliminar, modificar y añadir temas y sus indicaciones asociadas según sea necesario.

Para importar un archivo .csv de data insights, primero debe exportar un archivo desde el panel de control Presencia de marca. Consulte la sección [data insights](/help/dashboards/brand-presence.md#data-insights) para obtener información sobre cómo hacerlo. Una vez que tenga el archivo, haga lo siguiente:

1. En el panel de control, haga clic en **Cargar CSV**.
2. En la ventana Importar Data Insights, arrastre y suelte o elija manualmente el archivo.
3. Haga clic en **Subir datos**.

También puede crear un nuevo archivo CSV descargando la plantilla desde la ventana **Importar Data Insights**. Una vez tenga la plantilla, ábrala e introduzca los temas junto con sus indicaciones, categorías y regiones asociadas, cada una en una nueva línea.

Para obtener información sobre cómo descargar y utilizar la biblioteca de indicadores del sector creada por Adobe, consulte la sección Biblioteca de indicadores del sector en [esta página](/help/overview/best-practices-topics-prompts.md)

Además, también puede añadir temas/indicaciones a la lista independientemente de un archivo CSV o de una biblioteca de indicaciones. Para conseguirlo, en el panel de control, debe hacer lo siguiente:

1. Haga clic en el botón **Añadir tema**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Introduzca el nombre del tema
4. Añada el texto de la indicación.
5. Seleccione la región.
6. Haga clic en **Añadir indicación** y el tema con la indicación aparece en la lista.

For customers that are on the [Brand Centric experience](/help/overview/quick-start.md#brand-centric-experience), to add Topics and Prompts, navigate to **Prompts Management**.

![Prompts Management (Brand Centric experience)](/help/assets/brand-centric-experience/prompts-management.png)

>[!NOTE]
>Las indicaciones añadidas recientemente no aparecen en la presencia de marca hasta que se complete el procesamiento.

En la lista, puede hacer clic en cada tema y aparecen las indicaciones asociadas. Para eliminar el tema y sus indicaciones asociadas, haga clic en el icono Eliminar de la lista.

## Categorías {#categories}

Desde la pestaña Categorías, puede definir las categorías de empresa o las líneas de producto que desea rastrear y asociarlas a regiones específicas. En general, la pestaña Categorías está relacionada con casi todas las demás personalizaciones de esta página, ya que las categorías aparecen en el campo Categoría para las demás personalizaciones (seguimiento de otros, alias, etc.). Para añadir una nueva categoría, haga lo siguiente:

1. Haga clic en el botón **Añadir**.
2. En la nueva ventana de configuración, añada **Nombre de categoría**.
3. Personalice la **región asociada** donde se supervisará la categoría.
4. Haga clic en **Guardar** y la nueva categoría aparecerá en la lista de categorías.

Añadir nuevas categorías no generará automáticamente temas ni indicaciones, estos deberán añadirse manualmente desde la pestaña [Data Insights](#data-insights).

Para eliminar una categoría, haga clic en el icono Eliminar en la lista de categorías. Tenga cuidado, porque **al eliminar una categoría también se eliminarán los elementos asociados**, como alias de marca vinculados a esa categoría específica.

## Otras marcas {#others-tracking}

Con esta pestaña, puede realizar un seguimiento de cómo se mencionan los demás en relación con su marca en diferentes categorías y regiones. Monitorice su presencia y rendimiento en sus segmentos de mercado. Para personalizar el seguimiento, haga lo siguiente:

1. Haga clic en el botón **Añadir**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Añada el nombre del otro.
4. Personalice los demás alias y dominios si es necesario.
5. Haga clic en **Guardar**.

Para eliminar una entrada de la lista, haga clic en el icono Eliminar.

## Alias de marca {#brand-aliases}

Al utilizar el alias de marca, puede configurar nombres alternativos y variaciones de su marca que deban rastrearse en diferentes categorías y regiones. Esto garantiza una monitorización completa de todas las menciones de la marca. Para añadir un alias de marca, haga lo siguiente:

1. Haga clic en el botón **Añadir**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Seleccione la **región** donde se monitorizará el alias.
4. Añada el alias de la marca.
5. Haga clic en **Guardar** y el alias de la marca aparecerá en la lista.

To delete a brand alias, click the **Delete** icon from the alias list.

## Configuración de la CDN {#cdn-configuration}

Desde esta pestaña, puede configurar los flujos de CDN para permitir que Adobe LLM Optimizer analice los datos de CDN. Estos datos se utilizarán para impulsar los paneles de control (como el tráfico agéntico), lo que proporcionará perspectivas sobre los patrones de tráfico, las métricas de rendimiento y las oportunidades de optimización. Para incorporar su proveedor de CDN, haga clic en **Incorporar CDN**.

![CDN de configuración de cliente](/help/overview/assets/cc-cdn.png)

En la ventana **Incorporar proveedor de CDN**, haga lo siguiente:

1. Seleccione su proveedor de CDN.
2. Haga clic en **Incorporar** para habilitar el reenvío de registros.

Si selecciona **Otro**, tendrá que ponerse en contacto con llmo-now@adobe.com para obtener ayuda.

## Consola de búsqueda de Google {#google-console}

Adobe LLM Optimizer allows you to integrate your Google Search Console account to bring real search queries directly into the interface. By surfacing real Google Search Console queries, you can build prompt sets that are grounded in actual search behavior and high-intent discovery patterns. This helps you prioritize prompts based on proven demand and aligns LLM optimization efforts with how users currently search. Additionally, you remain in full control because queries are never added automatically and must be explicitly selected before becoming active prompts.

### Funcionamiento {#how-it-works}

The main thing to remember about the integration between LLM Optimizer with Google Search Console is the following: instead of manually guessing what customers might ask an AI assistant, we look at what they **are already searching for** and transform those real queries into natural, conversational prompts. This process of moving from search queries to AI prompts is exemplified in the diagram below.

![Process Flow](/help/dashboards/assets/diagram-flow.png)

Generally speaking, the process has five steps:

#### Step 1 — Collect your real search data {#gsc-one}

The process starts with the keywords your audience is actually using when it finds your website via Google. This raw dataset (often thousands of unique queries) is the foundation for everything that follows.

#### Step 2 — Analyze meaning and filter for safety {#gsc-two}

Each query is analyzed for its semantic meaning (what the user is really asking about) and screened through a safety filter that removes inappropriate or off-brand content. This ensures only clean, relevant keywords move forward.

#### Step 3 — Group into categories and topics {#gsc-three}

Las consultas relacionadas se agrupan automáticamente en **categorías** (temas empresariales generales) y **temas** (subtemas centrados dentro de cada categoría). El sistema prioriza las categorías que ya están configuradas en la configuración de LLM Optimizer. Además, también pueden surgir nuevas categorías que los datos de búsqueda revelen, pero que aún no se estén monitoreando. El diagrama siguiente es un ejemplo de categorías y temas para una marca de muebles:

![Marca de muebles](/help/dashboards/assets/diagram-example.png)

#### Paso 4: Generar mensajes basados en palabras clave reales {#gsc-four}

Para cada tema, el sistema genera indicadores similares a cómo las personas reales hablan con los asistentes de IA. Cada mensaje se ve directamente influido por las palabras clave de búsqueda reales de la consola de búsqueda de Google, lo que transforma la intención de la palabra clave en preguntas conversacionales naturales.

Este enfoque (basado en palabras clave) significa:

* Los indicadores reflejan una demanda real, no preguntas hipotéticas.
* El lenguaje refleja cómo sus clientes realmente dicen las cosas.
* La cobertura abarca toda la amplitud de lo que las personas buscan en el sitio.

La generación rápida también tiene en cuenta el perfil de su marca, incluidos los productos, la competencia, el posicionamiento en el sector y la audiencia destinataria, para garantizar que las indicaciones sean contextualmente precisas.

#### Paso 5: Garantía de calidad y entrega {#gsc-five}

Antes de la entrega, cada mensaje pasa por varias comprobaciones de calidad automatizadas:

* Deduplicación: se eliminan las indicaciones casi idénticas.
* Equilibrio de proporción de marca: garantiza una combinación realista (aproximadamente 75% sin marca, ~25% con marca).
* Calidad del lenguaje: elimina la fraseología robótica para que suene natural.
* Comprobaciones de coherencia: valida, elimina las frases de relleno y garantiza una longitud concisa.

Además, cada mensaje está etiquetado con su categoría, tema, tipo de intención y clasificación con marca/sin marca, listo para que LLM Optimizer empiece a monitorizarlo.

#### Anatomía del indicador {#prompt-anatomy}

Una vez completado el proceso anterior, cada mensaje enviado a LLM Optimizer tiene los siguientes atributos:

| Campo | Descripción |
|---------|----------|
| Texto | El mensaje, similar a cómo lo escribiría un usuario en un asistente de IA |
| Categoría | Tema empresarial general asignado a este mensaje. |
| Tema | El subtema específico dentro de la categoría. |
| Región | The target market (for example, US, UK and so on). |
| Intención | The user mindset: informational, comparative, transactional, instructional, planning, or delegation. |
| Tipo | The type can be either branded (mentions the brand/products) or unbranded (generic industry question). |

### Usos {#how-to-use}

Follow the steps presented below to integrate and use the Google Search Console queries with LLM Optimizer.

#### Connect the Google Search Console {#connect-console}

Before using this feature you need to integrate your Google Search Console account with LLM optimizer.

1. Open the **Customer Configuration** dashboard (classic navigation) or **Brands Management** (Brand Centric experience), then go to the Google Search Console integration (GSC tag in the Brand Centric experience).
1. Navigate to the Google Search Console tab and click **Connect Account**.
   ![Google Search Console](/help/dashboards/assets/google-console.png)
1. Sign in with a Google account that has access to the desired Search Console property.
   ![Google Account](/help/dashboards/assets/google-account.png)
1. Choose the property you want to connect.
   ![Console Property](/help/dashboards/assets/console-property.png)
1. After the connection is complete, LLM Optimizer begins retrieving relevant search queries.
   ![Retrieving Data](/help/dashboards/assets/console-complete.png)

#### Review and search queries {#search-query}

After you integrate the Google Search Console account with LLM optimizer, you can review the list of topics and prompts sourced from the search console and add the prompts from the list.

1. On the Google Search Console tab, review the list of topics and prompts sourced from the Search Console.
   ![Prompts List](/help/dashboards/assets/prompts-list.png)
1. Click on the desired topic/prompt category to expand the list.
1. Use the **Add** button to add prompts from the list. You can also bulk add prompts and categories by using **Add all**.
   ![Add Prompts](/help/dashboards/assets/add-prompts.png)
1. Once you are satisfied with the selection, click **Save** on the notification message.

#### View added queries in the Prompts list {#prompts-list}

Después de agregar una consulta, aparece en la ficha [Indicadores](#prompts-brand) del panel de configuración del cliente (navegación clásica) o en **Administración de indicadores** (experiencia centrada en la marca). Las solicitudes procedentes de la consola de búsqueda de Google se marcan con un icono de consola de búsqueda de Google en la columna **Origen**. El icono le ayuda a distinguir entre los indicadores basados en el comportamiento de búsqueda real del usuario y los agregados manualmente o desde otras fuentes.

### Preguntas frecuentes {#gsc-faq}

P: ¿Con qué frecuencia se actualizan las preguntas en el panel de la consola de búsqueda de Google?

Las solicitudes procedentes de la consola de búsqueda de Google generalmente se actualizan una vez al mes. Cada actualización extrae los datos de consulta de búsqueda más recientes de la consola de búsqueda de Google, vuelve a ejecutar la canalización de generación y actualiza el conjunto de mensajes. Esto garantiza que los indicadores permanezcan alineados con las tendencias de búsqueda actuales y los cambios estacionales en el comportamiento del usuario.

P: ¿Cuántas peticiones de datos suelen proceder de la consola de búsqueda de Google?

El número depende del tamaño de la implementación y de la cantidad de categorías rastreadas. Por ejemplo:

| Categorías | Total de temas | Indicadores entregados |
|---------|----------|----------|
| 1-2 | 3-8 | ~65-180 |
| 4-5 | 12-20 | ~270-450 |
| 10 | 30-40 | ~675-900 |

Nuestro objetivo es ofrecer conjuntos de mensajes rápidos que cumplan los objetivos de calidad comunicados durante la prueba e incorporación: al menos 20 mensajes por tema, con 3-4 temas por categoría y un equilibrio entre marca y marca saludable.

P: ¿Con qué frecuencia veré las solicitudes procedentes de la consola de búsqueda de Google después de conectarme a la consola de búsqueda de Google?

Los indicadores suelen estar disponibles **en un plazo de pocas horas** después de que se haya establecido la conexión a la consola de búsqueda de Google. La canalización extrae automáticamente los datos de búsqueda, los procesa a través de los pasos de generación y garantía de calidad y envía el mensaje final definido a LLM Optimizer.

P: ¿Quién puede conectarse a la consola de búsqueda de Google?

Cualquier persona con **Propietario** o **Permiso completo** en la propiedad de la consola de búsqueda de Google puede autorizar la conexión. These are the permission levels that grant read access to search query data. If you are unsure about your permission level, you can check it under **Settings>Users** and permissions in your Google Search Console.

Q: Can I mark prompts as ignored or skipped so that I do not see them in the Google Search Console prompts list?

Yes, you can delete any prompt you do not want to monitor. Deleted prompts are removed from your active prompt list and will not appear in future reporting. If a deleted prompt is regenerated in a subsequent monthly refresh, you can remove it again.

Q: Once I add prompts from Google Search Console to my prompts list, how soon will I see Brand Presence data for those prompts?

Brand Presence data for newly added prompts will appear during the next scheduled data refresh, which typically runs at the beginning of each week. Depending on when you add the prompts, you may see results within a few days.
