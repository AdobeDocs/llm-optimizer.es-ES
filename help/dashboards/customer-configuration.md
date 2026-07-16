---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se monitorizará y analizará su marca dentro de la plataforma del optimizador de LLM.
feature: Customer Configuration
autotag-review: '2026-07-15T17:48:20.742Z'
TQID: 'https://experienceleague.adobe.com/BvaFF-pMzojy1TNZvCQQRbcT5c5AQ75OqjclmDi14Z0'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c898dfb2-0885-42fb-b2af-b2d756752646
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
subfeature_v2:
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fc314d1d-7cb9-4a38-8dbd-8f9b6478f40d
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 3935
ht-degree: 57%

---


# Configuración del cliente {#customer-configuration}

El panel de control Configuración del cliente es una potente herramienta que proporciona perspectivas sobre la visibilidad de su marca en los LLM. Al configurar correctamente categorías, temas e indicaciones, puede asegurarse de que la marca esté bien posicionada para aparecer en las respuestas generadas por LLM. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

El panel de control de configuración del cliente (que se muestra a continuación) se aplica cuando su organización sigue utilizando esta navegación.

![Panel de control Configuración del cliente](/help/dashboards/assets/customer-config.png)

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Indicaciones](#prompts-brand)
* [Categorías](#categories)
* [Otras marcas](#other-brands)
* [Alias de marca](#brand-aliases)
* [Configuración de la CDN](#agentic-cdn)
* [Consola de búsqueda de Google](#google-console)
* [Sugerencias rápidas basadas en intentos de citas y Tráfico de referencia](#prompt-suggestions)

Si se encuentra en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), vaya a **Administración de marcas** para configurar marcas, alias de marcas y definir los competidores de los cuales desea realizar un seguimiento. **Administración de marcas** también se usa para configurar integraciones como Google Search Console, Adobe Analytics y el reenvío de registros de CDN en relación con las direcciones URL asociadas con las marcas. Para ello, haga clic en las pestañas correspondientes: GSC, CDN, etc.

![Administración de marcas: navegación por las aplicaciones (experiencia centrada en las marcas)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Administración de marcas: información general sobre la configuración (experiencia centrada en la marca)](/help/assets/brand-centric-experience/brands-management-configuration.png)

>[!IMPORTANT]
>
> Para obtener información detallada sobre cómo configurar las categorías, temas e indicaciones, consulte la página [Prácticas recomendadas para configurar categorías, temas e indicaciones](/help/overview/best-practices-topics-prompts.md).

## Indicaciones {#prompts-brand}

En la pestaña **Indicaciones**, puede revisar, administrar y personalizar las indicaciones. Puede cargar un archivo .csv de [análisis de Presencia de marca](/help/dashboards/brand-presence.md), y la lista se rellenará con indicaciones y temas de ese análisis, o [descargar una biblioteca de indicaciones](/help/overview/best-practices-topics-prompts.md) creada por Adobe. También puede eliminar, modificar y añadir temas y sus indicaciones asociadas según sea necesario.

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

Para que los clientes que se encuentran en la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience) añadan temas e indicaciones, vaya a **Administración de indicaciones**.

![Administración de indicaciones (experiencia centrada en la marca)](/help/assets/brand-centric-experience/prompts-management.png)

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

Para eliminar un alias de marca, haga clic en el icono **Eliminar** en la lista de alias.

## Configuración de la CDN {#cdn-configuration}

Desde esta pestaña, puede configurar los flujos de CDN para permitir que Adobe LLM Optimizer analice los datos de CDN. Estos datos se utilizarán para impulsar los paneles de control (como el tráfico agéntico), lo que proporcionará perspectivas sobre los patrones de tráfico, las métricas de rendimiento y las oportunidades de optimización. Para incorporar su proveedor de CDN, haga clic en **Incorporar CDN**.

![CDN de configuración de cliente](/help/overview/assets/cc-cdn.png)

En la ventana **Incorporar proveedor de CDN**, haga lo siguiente:

1. Seleccione su proveedor de CDN.
2. Haga clic en **Incorporar** para habilitar el reenvío de registros.

Si selecciona **Otro**, tendrá que ponerse en contacto con llmo-now@adobe.com para obtener ayuda.

## Consola de búsqueda de Google {#google-console}

Adobe LLM Optimizer le permite integrar su cuenta de Google Search Console para incorporar consultas de búsqueda reales directamente en la interfaz. Al mostrar consultas reales de Google Search Console, puede crear conjuntos de indicaciones basados en el comportamiento de búsqueda real y en patrones de detección con alta intención. Esto le ayuda a priorizar las indicaciones en función de la demanda comprobada y adapta los esfuerzos de optimización de LLM a la forma en que los usuarios realizan búsquedas actualmente. Además, tendrá control total porque las consultas nunca se añaden automáticamente y deben seleccionarse explícitamente antes de convertirse en indicaciones activas.

### Funcionamiento {#how-it-works}

Lo que hay que recordar principalmente sobre la integración entre LLM Optimizer y Google Search Console es lo siguiente: en lugar de adivinar manualmente qué podrían preguntar los clientes a un Asistente de IA, vemos lo que **ya están buscando** y transformamos esas consultas reales en indicaciones naturales y conversacionales. Este proceso de pasar de consultas de búsqueda a indicaciones de IA se muestra en el diagrama siguiente.

![Flujo de proceso](/help/dashboards/assets/diagram-flow.png)

En términos generales, el proceso consta de cinco pasos:

#### Paso 1: Recopilar los datos de búsqueda reales {#gsc-one}

El proceso comienza con las palabras clave que el público está utilizando cuando encuentra el sitio web a través de Google. Este conjunto de datos sin procesar (a menudo miles de consultas únicas) es la base de todo lo que sigue.

#### Paso 2: Analizar el significado y filtrar por seguridad {#gsc-two}

Cada consulta se analiza para determinar su significado semántico (lo que el usuario realmente está preguntando) y se somete a un filtro de seguridad que elimina el contenido inapropiado o ajeno a la marca. Esto garantiza que solo se mantengan las palabras clave relevantes y limpias.

#### Paso 3: Agrupar en categorías y temas {#gsc-three}

Las consultas relacionadas se agrupan automáticamente en **categorías** (temas empresariales generales) y **temas** (subtemas centrados dentro de cada categoría). El sistema prioriza las categorías que ya están configuradas en la configuración de LLM Optimizer. Además, también pueden surgir nuevas categorías que los datos de búsqueda revelen, pero que aún no se estén monitorizando. En el siguiente diagrama se muestra un ejemplo de categorías y temas para una marca de muebles:

![Marca de muebles](/help/dashboards/assets/diagram-example.png)

#### Paso 4: Generar indicaciones basadas en palabras clave reales {#gsc-four}

Para cada tema, el sistema genera indicaciones similares a cómo las personas reales hablan con los asistentes de IA. Cada indicación se ve directamente influida por las palabras clave de búsqueda reales de Google Search Console, lo que transforma la intención de la palabra clave en preguntas conversacionales naturales.

Este enfoque (basado en palabras clave) significa lo siguiente:

* Las indicaciones reflejan una demanda real, no preguntas hipotéticas.
* El lenguaje refleja cómo sus clientes se expresan realmente.
* La cobertura abarca todo lo que las personas buscan en el sitio.

La generación de indicaciones también tiene en cuenta el perfil de su marca, incluidos los productos, la competencia, el posicionamiento en el sector y el público destinatario, para garantizar que las indicaciones sean precisas desde el punto de vista contextual.

#### Paso 5: Control de calidad y envío {#gsc-five}

Antes de enviarse, cada indicación se somete a varias comprobaciones de calidad automatizadas:

* Anulación de duplicación: se eliminan las indicaciones casi idénticas.
* Equilibrio de proporción de marca: garantiza una combinación realista (aproximadamente 75 % sin marca, ~25 % con marca).
* Calidad del lenguaje: elimina la fraseología robótica para que las indicaciones suenen naturales.
* Comprobaciones de coherencia: valida, elimina las frases de relleno y garantiza una longitud concisa.

Además, cada indicación se etiqueta con su categoría, tema, tipo de intención y clasificación con marca/sin marca, lista para que LLM Optimizer empiece a monitorizarla.

#### Anatomía de la indicación {#prompt-anatomy}

Una vez completado el proceso anterior, cada indicación enviada a LLM Optimizer tiene los siguientes atributos:

| Campo | Descripción |
|---------|----------|
| Texto | La indicación, similar a cómo la escribiría un usuario en un Asistente de IA |
| Categoría | El tema empresarial general asignado a esta indicación. |
| Tema | El subtema específico dentro de la categoría. |
| Región | El mercado de destino (por ejemplo, EE. UU., Reino Unido, etc.). |
| Intención | La mentalidad del usuario: informativa, comparativa, transaccional, instruccional, de planificación o delegación. |
| Tipo | El tipo puede ser con marca (menciona la marca o los productos) o sin marca (pregunta genérica del sector). |

### Usos {#how-to-use}

Siga los pasos que se indican a continuación para integrar y utilizar las consultas de Google Search Console con LLM Optimizer.

#### Conectar Google Search Console {#connect-console}

Antes de utilizar esta función, debe integrar su cuenta de Google Search Console con LLM Optimizer.

1. Abra el panel de control **Configuración del cliente** (navegación clásica) o **Administración de marcas** (experiencia centrada en la marca) y, a continuación, vaya a la integración de Google Search Console (etiqueta GSC en la experiencia centrada en la marca).
1. Vaya a la pestaña de Google Search Console y haga clic en **Conectar cuenta**.
   ![Google Search Console](/help/dashboards/assets/google-console.png)
1. Inicie sesión con una cuenta de Google que tenga acceso a la propiedad de Search Console deseada.
   ![Cuenta de Google](/help/dashboards/assets/google-account.png)
1. Elija la propiedad que desea conectar.
   ![Propiedad de la consola](/help/dashboards/assets/console-property.png)
1. Una vez finalizada la conexión, LLM Optimizer empieza a recuperar las consultas de búsqueda relevantes.
   ![Recuperación de datos](/help/dashboards/assets/console-complete.png)

#### Revisión y búsqueda de consultas {#search-query}

Después de integrar la cuenta de Google Search Console con LLM Optimizer, puede revisar la lista de temas e indicaciones de datos procedentes de la consola de búsqueda y añadirlas desde la lista.

1. En la pestaña Google Search Console, revise la lista de temas e indicaciones procedentes de Search Console.
   ![Lista de indicaciones](/help/dashboards/assets/prompts-list.png)
1. Haga clic en el tema o categoría de indicación que desee para expandir la lista.
1. Utilice el botón **Añadir** para añadir indicaciones de la lista. También puede añadir indicaciones y categorías de forma masiva usando **Añadir todo**.
   ![Añadir indicaciones](/help/dashboards/assets/add-prompts.png)
1. Una vez que esté satisfecho con la selección, haga clic en **Guardar** en el mensaje de notificación.

#### Visualización de las consultas añadidas en la lista de indicaciones {#prompts-list}

Después de añadir una consulta, aparecerá en la pestaña [Indicaciones](#prompts-brand) en el panel de control de configuración del cliente (navegación clásica) o en **Administración de indicaciones** (experiencia centrada en la marca). Las indicaciones procedentes de Google Search Console se marcan con un icono de Google Search Console en la columna **Origen**. El icono le ayuda a distinguir entre las indicaciones basadas en el comportamiento de búsqueda real del usuario y las añadidas manualmente o desde otras fuentes.

### Preguntas frecuentes {#gsc-faq}

P: ¿Con qué frecuencia se actualizan las indicaciones en el panel de control de Google Search Console?

Las indicaciones procedentes de Google Search Console generalmente se actualizan una vez al mes. Cada actualización extrae los datos de consulta de búsqueda más recientes de Google Search Console, vuelve a ejecutar la canalización de generación y actualiza el conjunto de indicaciones. Esto garantiza que las indicaciones se mantengan en consonancia con las tendencias de búsqueda actuales y los cambios estacionales en el comportamiento del usuario.

P: ¿Cuántas indicaciones suelen proceder de Google Search Console?

El número depende del tamaño de la implementación y de la cantidad de categorías rastreadas. Por ejemplo:

| Categorías | Total de temas | Indicaciones enviadas |
|---------|----------|----------|
| 1-2 | 3-8 | ~65–180 |
| 4-5 | 12-20 | ~270–450 |
| 10 | 30-40 | ~675–900 |

Nuestro objetivo es ofrecer conjuntos de indicaciones rápidas que cumplan los objetivos de calidad comunicados durante la versión de prueba y la incorporación: al menos 20 indicaciones por tema, con 3-4 temas por categoría y un equilibrio adecuado entre con marca y sin marca.

P: ¿Con qué frecuencia veré las indicaciones procedentes de Google Search Console después de conectarme a Google Search Console?

Las indicaciones suelen estar disponibles **al cabo de unas pocas horas** después de que se haya establecido la conexión a Google Search Console. La canalización extrae automáticamente los datos de búsqueda, los procesa a través de los pasos de generación y control de calidad y envía la indicación final definida a LLM Optimizer.

P: ¿Quién puede conectarse a Google Search Console?

Cualquier persona que sea **Propietaria** o tenga **Permiso completo** en la propiedad de Google Search Console puede autorizar la conexión. Son niveles de permiso que conceden acceso de lectura a los datos de consulta de búsqueda. Si no está seguro del nivel de permiso, puede comprobarlo en **Configuración>Usuarios** y en los permisos de Google Search Console.

P: ¿Puedo marcar las indicaciones como ignoradas u omitidas para que no las vea en la lista de indicaciones de Google Search Console.

Sí, puede eliminar cualquier indicación que no desee monitorizar. Las indicaciones eliminadas se eliminarán de la lista de indicaciones activa y no aparecerán en el sistema de informes futuros. Si una indicación eliminada se vuelve a generar en una actualización mensual posterior, puede eliminarla de nuevo.

P: Una vez que añada indicaciones procedentes de Google Search Console a mi lista de indicaciones, ¿con qué frecuencia veré datos de Presencia de marca para dichas indicaciones?

Los datos de Presencia de marca de las indicaciones recién añadidas aparecerán durante la siguiente actualización de datos programada, que generalmente se ejecuta al principio de cada semana. Según el momento en el que añada las indicaciones, es posible que obtenga resultados en unos días.

## Sugerencias rápidas basadas en intentos de citas y Tráfico de referencia {#prompt-suggestions}

En lugar de adivinar qué indicadores importan, **Sugerencias de mensajes** empiezan por lo que los agentes de IA y los usuarios ya están accediendo o a lo que se hace referencia en el sitio.

Adobe LLM Optimizer analiza los datos de su CDN para identificar a qué páginas acceden ya de forma coherente los agentes de IA (intentos de citas) y los usuarios de referencia (tráfico de referencia LLM). Después, genera automáticamente sugerencias rápidas en función de los huecos en la cobertura de mensajes actual. En lugar de adivinar qué direcciones URL priorizar y qué indicadores crear, el flujo de trabajo comienza a partir de señales de tráfico reales: páginas a las que los agentes ya están buscando y, a continuación, definiendo el tipo de indicadores de usuario que esas páginas deben responder.

Cuando los agentes de IA ya acceden de forma constante a una página, la pregunta no es cómo hacer que los agentes conozcan la página, sino qué preguntas podría responder el contenido de la página. Si no hay mensajes configurados para estas páginas, no tendrá visibilidad de cómo se muestra su marca en las respuestas de IA sobre los temas más importantes. Sugerencias rápidas del tráfico de la agencia cierra esa brecha para que pueda iniciar el seguimiento y mejorar la visibilidad de la marca de las páginas en las que los agentes ya están más activos.

>[!NOTE]
>
> En la [experiencia centrada en la marca](/help/overview/quick-start.md#brand-centric-experience), las sugerencias de mensajes aparecen en la sección **Administración de mensajes**.

### Funcionamiento {#prompt-suggestions-how-it-works}

El flujo de trabajo Sugerencias de mensajes se ejecuta en cuatro pasos, lo que convierte las señales de tráfico de CDN en sugerencias de mensajes listas para configurar. Cada paso se basa en el anterior: a partir de páginas en las que la actividad del agente de IA ya está probada, comprender de qué tratan esas páginas, comprobar lo que ya se cubre y generar indicadores específicos, basados en tierra y listos para publicar.

![Sugerencias de mensajes del flujo de trabajo de tráfico del agente](/help/dashboards/assets/prompt-suggestions-workflow.png)

#### Paso 1: Identificación de páginas de alta señal de tráfico auténtico {#prompt-suggestions-step-1}

La canalización comienza identificando páginas del sitio con las que los sistemas de IA ya están interactuando de forma activa, mediante dos señales de los datos de CDN: la frecuencia con la que los sistemas de IA acceden a las páginas como fuente al responder preguntas reales del usuario y si esas páginas ya están dirigiendo a los usuarios reales a su sitio desde respuestas generadas por IA.

* **Intentos de cita**: cómo los sistemas de IA accedieron a una página como fuente potencial al responder preguntas del usuario. La canalización busca páginas que muestran intentos de citas coherentes semana tras semana, lo que ofrece una imagen más holística del interés que un solo punto en el tiempo.
* **tráfico de referencia LLM**: casos en los que un usuario hizo clic desde una respuesta generada por IA para aterrizar en la dirección URL. La canalización se centra en los datos de referencia más recientes y prioriza las páginas con el mayor volumen de visitas impulsadas por IA, lo que garantiza que las sugerencias se basen en los patrones de recomendación de IA actuales y comprobados.

| Señal | Lo que significa |
|--------|---------------|
| Solo intentos de cita | Los agentes acceden de forma consistente a esta página como un origen potencial |
| Solo tráfico de referencia LLM | Los agentes están enviando usuarios a esta página de forma activa |
| Ambas | Los agentes acceden a él y los usuarios hacen clic en él, el destinatario de mayor confianza |

Una página puede calificarse a través de una señal o de ambas. Las páginas que muestran ambas señales representan los objetivos de mayor confianza para la generación rápida.

#### Paso 2: Análisis del contenido y la intención de la página {#prompt-suggestions-step-2}

Para cada página correspondiente, la canalización lee el contenido de la página y:

* **Lo resume** en una descripción concisa basada en hechos que se convierte en la base de todo lo que sigue.
* **Clasifica** el tipo de página, ya sea un producto, un recurso, un soporte técnico o un concentrador.
* Identifica la **intención de recorrido principal**: el tipo de pregunta que la página está en mejor posición para responder, como informativa, instructiva, comparativa o transaccional.

Las dos clasificaciones funcionan juntas. Por ejemplo, es más probable que los mensajes generados a partir de una página de asistencia, como una guía de configuración o un tutorial, sean relevantes para un perfil de usuario existente que para una nueva audiencia.

#### Paso 3: Comprobar la cobertura de mensajes existente {#prompt-suggestions-step-3}

Antes de generar algo nuevo, la canalización comprueba si cada página elegible ya está cubierta por mensajes configurados en su cuenta de LLM Optimizer, que se ejecutan en dos pasos:

1. Un análisis de similitud semántica que identifica rápidamente los mensajes candidatos de la biblioteca de mensajes existente que están potencialmente relacionados con la página.
2. Una revisión con tecnología LLM que puntúa cómo se alinea cada candidato puntual con el contenido de la página, no solo si está relacionado temporalmente, sino si cubre de qué trata la página.

Una página se considera cubierta si al menos un mensaje existente cumple ese umbral. Las páginas sin coincidencia adecuada se identifican como brechas y se mueven al paso 4.

#### Paso 4: Generación, comprobación de calidad y clasificación de mensajes por dirección URL {#prompt-suggestions-step-4}

![Generación de mensajes y comprobación de calidad](/help/dashboards/assets/prompt-suggestions-generation.png)

Para cada página con espacios, la canalización genera mensajes que suenan naturales basados en el contenido de la página. Comienza identificando personas relevantes: alguien que de manera realista haría preguntas a las que esta página responde y construye un escenario realista alrededor de esa persona antes de generar peticiones de candidatos.

Cada mensaje pasa por una revisión de calidad automatizada en tres dimensiones:

* Si es **específico** para esta página en lugar de una pregunta genérica que podría aplicarse a cualquier página de la categoría.
* Si está **conectado a tierra** en el contenido real de la página.
* Si suena como algo que un **usuario real** escribiría en una herramienta de IA como ChatGPT.

Las peticiones de datos que no pasan esta revisión se vuelven a escribir con comentarios específicos y se vuelven a revisar. Si todavía no pasan, se caen.

El paso final es una comprobación de la diversidad, los indicadores de dirección URL demasiado similares se eliminan de la lista final. Cada mensaje está etiquetado con el tema y la categoría preconfigurados, e incluye un campo de razonamiento que explica por qué la URL de origen se segmentó en función de sus señales de intento de cita y tráfico de referencia. A los indicadores también se les asigna una clasificación de prioridad para que sepa sobre qué sugerencias actuar primero: una prioridad mayor significa una señal de IA combinada más fuerte desde la dirección URL de origen. Los indicadores están listos para revisarse en la ficha **Sugerencias para los mensajes** del panel de configuración del cliente.

### Usos {#prompt-suggestions-how-to-use}

1. Abra el panel **Configuración del cliente** y vaya a la pestaña **Sugerencias de mensajes**.
1. Use el filtro **Source** para seleccionar **Intento de cita** y ver las sugerencias generadas a partir del tráfico auténtico.
1. Revise las columnas **Razonamiento** y **Prioridad** para evaluar cada sugerencia.
1. Seleccione los indicadores que desee agregar y haga clic en **Agregar selección** para agregarlos a los indicadores configurados.

![Pestaña Sugerencias de mensajes con el filtro de origen Intento de cita](/help/dashboards/assets/prompt-suggestions-citation-attempt.png)

![Agregar sugerencias de solicitud seleccionadas](/help/dashboards/assets/prompt-suggestions-add-selection.png)

### Preguntas frecuentes {#prompt-suggestions-faq}

P: ¿Necesita mi organización alguna configuración adicional para utilizar esta función?

Esta función se basa en los datos de registro de CDN. Si ya ha habilitado el [reenvío de registros de CDN](#cdn-configuration), no se necesita ninguna configuración adicional. Sin los registros de CDN, los datos de intentos de cita o tráfico de referencia no estarán disponibles para su análisis.

P: ¿Por qué no aparece una dirección URL específica en las sugerencias?

Hay algunas razones comunes. Es posible que la página aún no tenga una actividad de recuperación de IA coherente o un tráfico de referencia significativo; sin una de esas señales, no entra en la canalización. Es posible que ya esté cubierto por una solicitud configurada existente, ya que la canalización solo genera sugerencias para lagunas reales. O puede que el tipo de página no sea apto para la generación de mensajes.

P: ¿Las sugerencias pueden cambiar con el tiempo?

Sí. La canalización se ejecuta periódicamente a medida que hay nuevos datos de CDN disponibles. A medida que evoluciona el comportamiento de los usuarios y los agentes (a qué páginas se accede, con qué frecuencia y cuáles generan tráficos de referencia), las sugerencias reflejan esos cambios. Las páginas que antes no eran de alta señal pueden calificarse en ejecuciones futuras y las lagunas existentes que se han abordado ya no generarán nuevas sugerencias.

P: ¿Por qué veo direcciones URL que no esperaba en las sugerencias?

Las direcciones URL que aparecen se basan completamente en el comportamiento agéntico observado: páginas a las que los sistemas de IA han accedido o al que han hecho referencia constantemente los usuarios, independientemente de su importancia en la estrategia de contenido. En algunos casos, pueden ser páginas que nunca consideró importantes, pero que AI ha buscado repetidamente. Si aparece una dirección URL en las sugerencias, es porque los datos la admiten. Siempre es libre de ignorar las sugerencias que no se ajustan a su estrategia, pero los datos detrás de cada sugerencia se basan en una actividad de IA real.

P: ¿Qué significa el campo de razonamiento?

Cada mensaje incluye una explicación de por qué su dirección URL de origen se enumeró como sugerencia. Para las páginas que cumplen los requisitos mediante intentos de citas, muestra cómo la página se clasifica entre todas las páginas a las que se accede en función de los intentos semanales. Para las páginas que se clasifican mediante el tráfico de referencia, muestra lo mismo para las vistas de página de referencia. Las páginas con ambas señales muestran ambas. Esto le ayuda a comprender la prioridad y elegir qué sugerencias publicar primero.

Para una página con ambas señales, el razonamiento podría ser: *Generado para [URL de página] — se encuentra en el 3% superior por la mediana de intentos de citas semanales y en el 1% superior por el tráfico de referencia LLM.*

P: ¿Cómo se determina la prioridad?

La prioridad se basa en una puntuación combinada de dos señales: cómo una página se clasifica entre todas las páginas por intentos de citas y cómo se clasifica entre todas las páginas por vistas de páginas de referencia de LM. Ambos se expresan como percentiles y se suman, de modo que las páginas que marcan con fuerza en ambas señales ascienden naturalmente a la parte superior. Una página a la que AI accede de forma constante y a la que envía usuarios de forma activa, siempre tendrá una clasificación más alta que una página con una sola señal.

P: ¿Cómo decide la canalización qué páginas cumplen los requisitos en función de los intentos de citas?

La canalización busca páginas que muestren una actividad de recuperación de IA coherente a lo largo del tiempo. Para ello, una página debe cumplir dos condiciones: debe mostrar actividad significativa en al menos la mitad de las semanas en los datos disponibles y su recuento medio de visitas reales durante esas semanas activas debe estar en el 25 % superior en todas las páginas. Ambas condiciones deben mantenerse: la frecuencia por sí sola no es suficiente y el volumen de visitas por sí solo tampoco es suficiente.

P: ¿Cómo decide la canalización qué páginas cumplen los requisitos en función del tráfico de referencia?

Una página cumple los requisitos si aparece en el 10 % de todas las páginas según el total de visitas de recomendación de LLM en los últimos tres meses. Esto garantiza que las sugerencias se basen en páginas que ya están generando clics reales y mensurables a partir de respuestas de IA, según el comportamiento reciente.

P: ¿Las sugerencias rápidas están disponibles en idiomas distintos del inglés?

Todavía no. Actualmente, la canalización solo genera peticiones de datos en inglés. En una versión futura se añadirá compatibilidad con varios idiomas.
