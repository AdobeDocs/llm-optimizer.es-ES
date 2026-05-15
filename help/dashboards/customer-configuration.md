---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se monitorizará y analizará su marca dentro de la plataforma del optimizador de LLM.
feature: Customer Configuration
autotag-review: '2026-05-15T17:45:12.067Z'
TQID: 'https://experienceleague.adobe.com/qa7zk54n9G19-Azz9f6mn7V1kAGvnJSOJjpxbTBeHgc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 2249
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

Si estás en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), ve a **Administración de marcas** para configurar marcas, alias de marcas y definir competidores con los cuales realizar seguimientos. **Brands Management** también se usa para configurar integraciones como la consola de búsqueda de Google, Adobe Analytics y el reenvío de registros de CDN en relación con las direcciones URL asociadas con las marcas. Para ello, haga clic en las pestañas correspondientes: GSC, CDN, etc.

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

Para que los clientes que están en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience) agreguen temas e indicadores, vaya a **Administración de indicadores**.

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

Cualquier persona con **Propietario** o **Permiso completo** en la propiedad de la consola de búsqueda de Google puede autorizar la conexión. Niveles de permisos que conceden acceso de lectura a los datos de consulta de búsqueda. Si no está seguro del nivel de permisos, puede comprobarlo en **Configuración>Usuarios** y en los permisos de la consola de búsqueda de Google.

P: ¿Puedo marcar los mensajes como ignorados u omitidos para que no los vea en la lista de mensajes de la consola de búsqueda de Google?

Sí, puede eliminar cualquier mensaje que no desee supervisar. Los mensajes eliminados se eliminan de la lista de mensajes activa y no aparecerán en los informes futuros. Si una solicitud eliminada se vuelve a generar en una actualización mensual posterior, puede eliminarla de nuevo.

P: Una vez que añada peticiones de datos de la consola de búsqueda de Google a mi lista de peticiones de datos, ¿con qué frecuencia veo datos de Presencia de marca para ellas?

Los datos de presencia de marca de los mensajes recién añadidos aparecerán durante la siguiente actualización de datos programada, que generalmente se ejecuta al principio de cada semana. Según el momento en el que agregue los indicadores, es posible que vea los resultados en unos días.
