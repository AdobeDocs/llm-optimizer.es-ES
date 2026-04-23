---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se monitorizará y analizará su marca dentro de la plataforma del optimizador de LLM.
feature: Customer Configuration
source-git-commit: ef6b4ec9dcb3b5234add6e82cbc54ab29d363509
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 37%

---


# Configuración del cliente {#customer-configuration}

El panel de control Configuración del cliente es una potente herramienta que proporciona perspectivas sobre la visibilidad de su marca en los LLM. Al configurar correctamente categorías, temas e indicaciones, puede asegurarse de que la marca esté bien posicionada para aparecer en las respuestas generadas por LLM. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

El panel de configuración del cliente (que se muestra a continuación) se aplica cuando su organización sigue utilizando este sistema de navegación.

![Panel de control Configuración del cliente](/help/dashboards/assets/customer-config.png)

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Indicaciones](#prompts-brand)
* [Categorías](#categories)
* [Otras marcas](#other-brands)
* [Alias de marca](#brand-aliases)
* [Configuración de la CDN](#agentic-cdn)
* [Consola de búsqueda de Google](#google-console)

Si está en la experiencia centrada en la marca, vaya a **Administración de marcas** para configurar marcas, alias de marcas y definir competidores con los cuales realizar el seguimiento. **Brands Management** también se usa para configurar integraciones como la consola de búsqueda de Google, Adobe Analytics y el reenvío de registros de CDN en relación con las direcciones URL asociadas con las marcas. Para ello, haga clic en las pestañas correspondientes: GSC, CDN, etc.

![Gestión de marcas — Navegación de aplicaciones (experiencia centrada en las marcas)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Administración de marcas — información general sobre la configuración (experiencia centrada en las marcas)](/help/assets/brand-centric-experience/brands-management-configuration.png)

>[!IMPORTANT]
>
> Para obtener información detallada sobre cómo configurar las categorías, temas e indicaciones, consulte la página [Prácticas recomendadas para configurar categorías, temas e indicaciones](/help/overview/best-practices-topics-prompts.md).

## Indicaciones {#prompts-brand}

Desde la ficha **Indicadores**, puede revisar, administrar y personalizar los mensajes. Puede cargar un archivo .csv de [análisis de Presencia de marca](/help/dashboards/brand-presence.md), y la lista se rellenará con indicaciones y temas de ese análisis, o [descargar una biblioteca de indicaciones](/help/overview/best-practices-topics-prompts.md) creada por Adobe. También puede eliminar, modificar y añadir temas y sus indicaciones asociadas según sea necesario.

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

Para que los clientes que están en la experiencia centrada en la marca agreguen temas e indicadores, vaya a **Administración de indicadores**.

![Administración de indicadores (experiencia centrada en la marca)](/help/assets/brand-centric-experience/prompts-management.png)

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

Para eliminar un alias de marca, haz clic en el icono **Eliminar** de la lista de alias.

## Configuración de la CDN {#cdn-configuration}

Desde esta pestaña, puede configurar los flujos de CDN para permitir que Adobe LLM Optimizer analice los datos de CDN. Estos datos se utilizarán para impulsar los paneles de control (como el tráfico agéntico), lo que proporcionará perspectivas sobre los patrones de tráfico, las métricas de rendimiento y las oportunidades de optimización. Para incorporar su proveedor de CDN, haga clic en **Incorporar CDN**.

![CDN de configuración de cliente](/help/overview/assets/cc-cdn.png)

En la ventana **Incorporar proveedor de CDN**, haga lo siguiente:

1. Seleccione su proveedor de CDN.
2. Haga clic en **Incorporar** para habilitar el reenvío de registros.

Si selecciona **Otro**, tendrá que ponerse en contacto con llmo-now@adobe.com para obtener ayuda.

## Consola de búsqueda de Google {#google-console}

Adobe LLM Optimizer le permite integrar su cuenta de Google Search Console para llevar las consultas de búsqueda real directamente a la interfaz. Al mostrar consultas reales de la consola de búsqueda de Google, puede crear conjuntos de mensajes basados en el comportamiento de búsqueda real y en patrones de detección de alta intención. Esto le ayuda a priorizar los indicadores en función de la demanda comprobada y alinea los esfuerzos de optimización de LLM con la forma en que los usuarios buscan actualmente. Además, permanece en control total porque las consultas nunca se agregan automáticamente y deben seleccionarse explícitamente antes de convertirse en mensajes activos.

### Funcionamiento {#how-it-works}

Lo principal que hay que recordar acerca de la integración entre LLM Optimizer y la consola de búsqueda de Google es lo siguiente: en lugar de adivinar manualmente qué podrían preguntar los clientes a un asistente de IA, vemos lo que **ya están buscando** y transformamos esas consultas reales en mensajes naturales y conversacionales. Este proceso de pasar de consultas de búsqueda a peticiones de datos de IA se ejemplifica en el diagrama siguiente.

![Flujo de proceso](/help/dashboards/assets/diagram-flow.png)

En términos generales, el proceso consta de cinco pasos:

#### Paso 1: Recopilar los datos de búsqueda real {#gsc-one}

El proceso comienza con las palabras clave que la audiencia está utilizando cuando encuentra el sitio web a través de Google. Este conjunto de datos sin procesar (a menudo miles de consultas únicas) es la base de todo lo que sigue.

#### Paso 2: Analizar el significado y filtrar por seguridad {#gsc-two}

Cada consulta se analiza por su significado semántico (lo que el usuario realmente está preguntando) y se analiza a través de un filtro de seguridad que elimina el contenido inapropiado o fuera de marca. Esto garantiza que solo las palabras clave relevantes y limpias avancen.

#### Paso 3: Agrupar en categorías y temas {#gsc-three}

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
| Región | El mercado objetivo (por ejemplo, EE. UU., Reino Unido, etc.). |
| Intención | La mentalidad del usuario: informativa, comparativa, transaccional, instruccional, de planificación o de delegación. |
| Tipo | El tipo puede ser de marca (menciona la marca o los productos) o sin marca (pregunta genérica del sector). |

### Usos {#how-to-use}

Siga los pasos presentados a continuación para integrar y utilizar las consultas de la consola de búsqueda de Google con LLM Optimizer.

#### Conectar la consola de búsqueda de Google {#connect-console}

Antes de utilizar esta función, debe integrar su cuenta de Google Search Console con el optimizador LLM.

1. Abra el panel **Configuración del cliente** (navegación clásica) o **Administración de marcas** (experiencia de Brand Centric) y, a continuación, vaya a la integración de Google Search Console (etiqueta GSC en la experiencia de Brand Centric).
1. Vaya a la pestaña Google Search Console y haga clic en **Conectar cuenta**.
   ![Consola de búsqueda de Google](/help/dashboards/assets/google-console.png)
1. Inicie sesión con una cuenta de Google que tenga acceso a la propiedad de Search Console deseada.
   ![Cuenta de Google](/help/dashboards/assets/google-account.png)
1. Elija la propiedad que desea conectar.
   ![Propiedad de la consola](/help/dashboards/assets/console-property.png)
1. Una vez finalizada la conexión, LLM Optimizer empieza a recuperar las consultas de búsqueda relevantes.
   ![Recuperando datos](/help/dashboards/assets/console-complete.png)

#### Consultas de revisión y búsqueda {#search-query}

Después de integrar la cuenta de Google Search Console con el optimizador LLM, puede revisar la lista de temas y peticiones de datos procedentes de la consola de búsqueda y añadirlos desde la lista.

1. En la pestaña Consola de búsqueda de Google, revise la lista de temas y preguntas procedentes de la Consola de búsqueda.
   ![Lista de indicadores](/help/dashboards/assets/prompts-list.png)
1. Haga clic en el tema o categoría de solicitud que desee para expandir la lista.
1. Utilice el botón **Agregar** para agregar mensajes de la lista. También puede agregar avisos y categorías de forma masiva usando **Agregar todo**.
   ![Agregar indicadores](/help/dashboards/assets/add-prompts.png)
1. Una vez que esté satisfecho con la selección, haga clic en **Guardar** en el mensaje de notificación.

#### Ver consultas agregadas en la lista de indicadores {#prompts-list}

After a query is added, it appears in the [Prompts](#prompts-brand) tab within the Customer Configuration dashboard (classic experience) or in **Prompts Management** (Brand Centric experience). Prompts sourced from the Google Search Console are marked with a Google Search Console icon in the **Origin** column. The icon helps you distinguish between prompts that are grounded in actual user search behavior from those added manually or from other sources.

### Preguntas frecuentes {#gsc-faq}

Q: How often are prompts updated in the Google Search Console dashboard?

Prompts sourced from the Google Search Console are usually refreshed once per month. Each refresh pulls the latest search query data from your Google Search Console, re-runs the generation pipeline, and updates your prompt set. This ensures your prompts stay aligned with current search trends and seasonal shifts in user behavior.

Q: How many prompts are typically sourced from the Google Search Console?

The number depends on the size of your deployment and the amount of categories tracked. Por ejemplo:

| Categorías | Total Topics | Prompts Delivered |
|---------|----------|----------|
| 1–2 | 3–8 | ~65–180 |
| 4–5 | 12–20 | ~270–450 |
| 10 | 30–40 | ~675–900 |

We aim to deliver prompt sets that meet the quality targets communicated during trial and onboarding: at least 20 prompts per topic, with 3–4 topics per category, and a healthy branded/unbranded balance.

Q: How soon will I see prompts sourced from the Google Search Console after I connect to the Google Search Console?

Prompts are typically available **within a few hours** after your Google Search Console connection is established. The pipeline automatically pulls your search data, processes it through the generation and quality assurance steps and delivers the final prompt set to LLM Optimizer.

Q: Who can connect to the Google Search Console?

Anyone with **Owner** or **Full Permission** on the Google Search Console property can authorize the connection. These are the permission levels that grant read access to search query data. If you are unsure about your permission level, you can check it under **Settings>Users** and permissions in your Google Search Console.

Q: Can I mark prompts as ignored or skipped so that I do not see them in the Google Search Console prompts list?

Yes, you can delete any prompt you do not want to monitor. Deleted prompts are removed from your active prompt list and will not appear in future reporting. If a deleted prompt is regenerated in a subsequent monthly refresh, you can remove it again.

Q: Once I add prompts from Google Search Console to my prompts list, how soon will I see Brand Presence data for those prompts?

Brand Presence data for newly added prompts will appear during the next scheduled data refresh, which typically runs at the beginning of each week. Depending on when you add the prompts, you may see results within a few days.
