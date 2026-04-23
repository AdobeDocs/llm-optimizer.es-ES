---
title: Prácticas recomendadas para categorías, temas, indicaciones y otros
description: Optimice las perspectivas de LLM al configurar las categorías, los temas, las indicaciones y otras marcas para rastrear, incluyendo a la competencia, para la monitorización de marcas personalizadas y el análisis de contenido estratégico.
feature: Best Practices, Customer Configuration
source-git-commit: 625807b8905f741aa89d551483d89cca2ef91873
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 93%

---


# Prácticas recomendadas para configurar categorías, temas, indicaciones y otros para realizar seguimientos

En esta sección se describen las prácticas recomendadas para decidir cómo desea configurar las categorías, los temas, las indicaciones y otros elementos para realizar un seguimiento. Además, incluye información sobre la biblioteca de indicaciones del sector, que Adobe desarrolló con una amplia investigación con expertos del sector.

Este es un primer paso fundamental. Lo que decida ahora determina cómo se adapta la información a su contexto empresarial. Cualquier cambio en las categorías en el futuro restablecerá los datos históricos.

En el panel [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) se define cómo se supervisa y analiza su marca dentro de la plataforma de LLM Optimizer. Consulte [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) para obtener información sobre cómo usar el panel de control.

![Ventana de configuración del cliente](/help/assets/best-practices/customer-configuration-best-practices.png)

En el panel de control [!UICONTROL Configuración del cliente], puede personalizar categorías (como unidades de negocio o líneas de productos), realizar un seguimiento de otras marcas y añadir alias de mención de la marca para capturar todas las variaciones de su marca en las indicaciones. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

## Experiencia centrada en la marca

De forma predeterminada, los nuevos clientes empiezan en una interfaz centrada y de marca con una configuración basada en la incorporación. En esta nueva interfaz, cada organización comienza con una marca activa y marcas sugeridas adicionales para elegir. Los clientes existentes de LLM Optimizer cambiarán gradualmente a esta experiencia centrada en la marca.

Si se encuentra en la experiencia de Brand Centric, **Brands Management** es donde define cómo se supervisa y analiza su marca.

![Gestión de marcas — Navegación de aplicaciones (experiencia centrada en las marcas)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Administración de marcas — información general sobre la configuración](/help/assets/brand-centric-experience/brands-management-configuration.png)

Para configurar los temas y las indicaciones de una marca específica, use **Administración de indicaciones**.

![Administración de indicadores](/help/assets/brand-centric-experience/prompts-management.png)

## Biblioteca de indicaciones del sector

Para empezar a utilizar indicaciones y temas, Adobe ha creado una biblioteca de indicaciones del sector, que se desarrolló con una amplia investigación de expertos del sector y análisis del comportamiento de la búsqueda por IA en más de 6000 clientes. Esta biblioteca identifica los temas y las indicaciones más relevantes en función de las tendencias específicas del sector, los objetivos comerciales validados y los patrones de búsqueda de clientes reales.

Para usar la biblioteca de indicaciones del sector, haga lo siguiente:

1. Vaya al panel de control **Configuración del cliente**.
1. Seleccione **Descargar biblioteca de indicaciones** para descargar el archivo de la biblioteca de LLM Optimizer.
   ![Descarga de Biblioteca de indicaciones de la industria](/help/assets/best-practices/customer-configuration-prompts-library.png)
1. Revise los **temas** e **indicaciones** sugeridas para la industria de su marca en la pestaña correspondiente y elija las opciones que sean más relevantes.
1. Revise la **columna fase de Recorrido del cliente** para ver las opciones de solicitud en todo el ciclo de vida del cliente (por ejemplo, la detección para la conversión a retención). La fase inicial/parte superior de las indicaciones de embudo son de alta prioridad, pero también hay que tener en cuenta las opciones de fase posterior para fomentar la retención, habilitar la asistencia al cliente, etc.
1. Modifique los temas o las indicaciones según sea necesario para lograr los objetivos y las metas antes de cargar los temas y las indicaciones en Adobe LLM Optimizer (por ejemplo, añada el nombre de su marca/producto o la terminología coherente con la marca). Las indicaciones se pueden añadir a LLM Optimizer manualmente o con la carga masiva mediante la plantilla *.CSV* proporcionada.

>[!TIP]
>
> Utilice una combinación de indicaciones específicas del dominio recomendadas por LLM Optimizer durante la configuración inicial y la biblioteca de indicaciones de la industria para depurar la estrategia de indicaciones.

### Fundación de investigación de la biblioteca de indicaciones

La biblioteca de indicaciones del sector se desarrolló a través de una iniciativa de investigación integral que combina lo siguiente:

* **Conocimiento del cliente:** análisis del comportamiento y las preferencias de la búsqueda por IA en más de 6000 clientes.
* **Experiencia del sector:** perspectivas de expertos en los sectores automotriz, servicios financieros, atención médica, telecomunicaciones y viajes.
* **Perspectivas basadas en datos:** identificación de temas de alto impacto y patrones de consulta que impulsan la participación y conversión de los clientes.

Temas principales buscados por clientes en todos los sectores:

* **Automóvil:** resolución de problemas de automóviles, comparación de vehículos y financiación/leasing.
* **Servicios financieros:** investigación de productos financieros.
* **Atención médica:** búsqueda de síntomas o problemas de salud, comparación de opciones de tratamiento, comprensión de los resultados de laboratorio o los términos médicos.
* **Telecomunicaciones:** comparación de planes, condiciones y promociones de contratos, comprobación del servicio en el área local.
* **Viajes:** preparación, investigación y reserva de viajes.

Tendencias del cliente en la búsqueda por IA y comportamiento de las indicaciones en las herramientas LLM:

* Los clientes prefieren hacer preguntas en lugar de utilizar palabras clave al utilizar las herramientas de búsqueda LLM.
* Utilizan principalmente herramientas de búsqueda LLM para la investigación y el descubrimiento en las primeras etapas.
* Los clientes tienden a mencionar una marca o un nombre de producto específico en sus indicaciones.

## Prácticas recomendadas para categorías

Las categorías permiten organizar el contenido en unidades de negocio estratégicas o agrupaciones lógicas. Representan la acción de compartimentar el contenido y una estructura organizativa de nivel superior.

Al decidir cómo configurar categorías, debe tener en cuenta sus objetivos y quién debe actuar en función de lo que esté informando.

>[!IMPORTANT]
>
> Asegúrese de que las categorías estén correctamente configuradas desde el principio, ya que los cambios en las categorías restablecen los datos históricos. Esto significa que, si las modifica, perderá datos históricos de antes del cambio.

A continuación se muestra una descripción general de los tipos de enfoques que puede adoptar y cuándo elegir un enfoque concreto:

| Enfoque | Descripción | Ventaja |
|---------|----------|---------|
| Unidad estratégica de negocio (UEN) | Utilice este enfoque si su organización está dividida en pérdidas y ganancias (por ejemplo, consumidores, empresas, servicios). | Obtendrá informes claros por línea de negocio y una delimitación de responsabilidades más sencilla. |
| Directorio de nivel superior del sitio web (DIR_URL) | Utilícelo si la arquitectura de información del sitio refleja la propiedad (/products/, /support/, /docs/, /news/). | Puede alinearse con la forma en que los equipos publican y mantienen el contenido. |
| Categoría (o servicio) de producto | Utilícelo si vende un catálogo (SKU/servicios). | Obtendrá vistas de surtidos, análisis de brechas y respuestas a “qué categoría necesita contenido”. |

La forma de decidir cómo se configuran las categorías se basa en una pregunta: **¿Quién debe actuar sobre el informe?**

* Si es un *líder de la empresa*, elija el enfoque **UEN**.
* Si es un *propietario de contenidos/web*, elija el enfoque **DIR_URL**.
* Si es un *administrador de comercialización/ofertas*, elija el enfoque de **categoría de producto/servicio**.

![Incorporación de categorías en LLM Optimizer](/help/assets/best-practices/add-category.png)

>[!IMPORTANT]
>
> * Elija un enfoque y manténgase fiel a él.
> * Solo puede tener **un** modelo de categoría por cuenta o marca. No mezcles **SBU** y **URL_DIR** al mismo tiempo.
<!--Can you mix Product/Service with these?-->

Ejemplo:

| Tipo de sitio | Categoría | Ejemplos de taxonomía de temas |
|---------|----------|---------|
| Empresas con varios negocios | UEN | Conjunto de pequeñas intenciones (procedimientos, solución de problemas, comparación, precios, política) |
| Sitio con gran cantidad de documentación/asistencia técnica | DIR_URL | Procedimientos, solución de problemas, referencia, notas de la versión |
| Catálogo de comercio electrónico/servicios | Producto/servicio | Comparación, opiniones, precios/disponibilidad, procedimientos, solución de problemas |

## Prácticas recomendadas para temas

Los temas le ayudan a comprender la intención del usuario: le muestran lo que este quiere. Le permiten agrupar las indicaciones con una intención de usuario similar. Es como si agrupara indicaciones relevantes.

>[!IMPORTANT]
>
>Los temas son universales en **todas** las categorías, lo que significa que se mantienen constantes independientemente de la categoría a la que estén asignados. Representan grupos de preguntas o indicaciones que comparten una intención común.

A la hora de decidir los temas, desea crear una lista breve y sencilla (entre 6 y 12 como máximo). Por ejemplo:

* Productos y servicios
* Procedimientos (configuración/uso)
* Solución de problemas (errores/problemas)
* Comparación (X frente a Y; “mejor... para...”)
* Opiniones y valoraciones
* Precios y disponibilidad
* Política y garantía
* Contacto de atención al cliente
* Corporativo/noticias (si realmente lo necesita)

![Incorporación de temas en LLM Optimizer](/help/assets/best-practices/add-topic.png)

A la hora de crear la lista, tenga en cuenta lo siguiente:

* ¿Puede un editor comprender el tema en cinco segundos a partir del texto de indicación? Si no es así, cambie el nombre o simplifíquelo.
* ¿La corrección de diferentes temas será responsabilidad de un equipo? Si es así, ha elegido temas útiles.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algunas sugerencias útiles adicionales:

* Emplee el conocimiento de su empresa o sitio para definir temas que se ajusten a los objetivos estratégicos de su marca.
* Considere cómo se compara su marca con otras dentro de temas específicos.

>[!IMPORTANT]
>
> * Mantenga los temas basados en intenciones, no en la organización.
> * No añada categorías o filtros para marcas/no marcas/zonas geográficas, ya que puede filtrar específicamente por esto en la pestaña **[!UICONTROL Marcas]**.
> * Los temas se distribuyen en varias categorías. **No puede** definir temas únicos para cada categoría.
> * **Puede** haber una sola indicación en varios temas o categorías.

## Prácticas recomendadas para las indicaciones

Las indicaciones identifican las preguntas o consultas específicas que los clientes formulan y que pueden afectar a su empresa. Son las preguntas o consultas reales que los usuarios introducen en los LLM.

Asegúrese de revisar y actualizar las indicaciones regularmente para asegurarse de que se alineen con las necesidades del cliente y los objetivos de la empresa.

Prácticas recomendadas para las indicaciones:

* Agrupe indicaciones similares en función de lo que pregunten las personas.
* Céntrese en las indicaciones que sean más importantes para sus clientes.
* Compruebe si su marca tiene una buena posibilidad de que se le mencione en relación con determinadas indicaciones.

>[!TIP]
>
>* Puede utilizar herramientas como Adobe LLM Optimizer y Google Search Console con filtros de expresiones regulares (regex) para identificar las estructuras de preguntas comunes (por ejemplo, “cómo”, “qué”, “cuándo”, “dónde”) y descubrir qué términos utilizan las personas al visitar su sitio web.
>* Para saber qué indicaciones son relevantes para su sitio/marca, utilizar los datos de búsqueda del sitio, las preguntas frecuentes en las páginas de resultados de los motores de búsqueda o incluso preguntar directamente a los bots de chat de LLM qué preguntas podrían hacer los clientes sobre su marca.

## Prácticas recomendadas para el seguimiento de otras marcas

Realizar un seguimiento de otros le permite monitorizar la visibilidad y las menciones en las respuestas de LLM en busca de indicaciones y temas que son importantes para su empresa.

La pestaña [!UICONTROL **Seguimiento de otros**] le permite añadir a otros, incluida la competencia, para rastrear su visibilidad en busca de indicaciones y temas específicos.

Con el seguimiento de otros, puede descubrir con qué frecuencia se mencionan otras marcas junto con su marca en diferentes regiones y categorías y comparar su visibilidad con la suya propia.

>[!TIP]
>
>Revise periódicamente las menciones y citas de la competencia o de otras personas para identificar las áreas en las que su marca puede mejorar.

## Más información

* [Panel de control Configuración del cliente](/help/dashboards/customer-configuration.md) es el lugar donde se configuran las categorías, los temas, las indicaciones y el seguimiento de otros.
* [Prácticas recomendadas en LLM Optimizer](/help/tutorials/best-practices.md) describe las prácticas recomendadas en la optimización de LLM

