---
title: Prácticas recomendadas para categorías, temas, indicaciones y otros
description: Optimice las perspectivas de LLM al configurar las categorías, los temas, las indicaciones y otras marcas para rastrear, incluyendo a la competencia, para la monitorización de marcas personalizadas y el análisis de contenido estratégico.
feature: Best Practices, Customer Configuration
autotag-review: '2026-07-15T17:42:20.391Z'
TQID: 'https://experienceleague.adobe.com/nnLohajbU-fogbmBfGE5PUzdsoTJ5fjwW-ruVTjOWtM'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c898dfb2-0885-42fb-b2af-b2d756752646id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: e69d5a42-0217-4ca5-9396-a9a826a170da
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: addf009e-030a-4310-8534-776a3e62ed48id: b5520579-b31f-4df7-9281-f0d9f91e2edcid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d00e9f03-e50b-4162-b143-0c0817c937c2id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: f8667931-f646-4dd3-af2a-b9d0cb8098ad
source-git-commit: 74484901cba1f054070673f2d706b26b6360aacb
workflow-type: tm+mt
source-wordcount: 1482
ht-degree: 77%

---

# Prácticas recomendadas para configurar categorías, temas, indicadores y otras marcas para realizar el seguimiento

En esta sección se describen las prácticas recomendadas para decidir cómo desea configurar las categorías, los temas, los mensajes y otras marcas que se van a rastrear. Además, incluye información sobre la biblioteca de indicaciones del sector, que Adobe desarrolló con una amplia investigación con expertos del sector.

Esta configuración es un primer paso vital. Lo que decida ahora determina cómo se adapta la información a su contexto empresarial. Cualquier cambio en las categorías en el futuro restablecerá los datos históricos.

En el tablero de [[!UICONTROL Brands Management]](/help/dashboards/customer-configuration.md) se define cómo se supervisa y analiza la marca en la plataforma del optimizador LLM.

Aquí puede personalizar categorías (como unidades de negocio o líneas de productos), rastrear otras marcas y agregar alias de mención de la marca para capturar todas las variaciones de su marca en los mensajes. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

De forma predeterminada, cada organización comienza con una marca activa y marcas sugeridas adicionales para elegir.

![Administración de marcas - navegación por la aplicación (experiencia centrada en la marca)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Administración de marcas - información general de configuración](/help/assets/brand-centric-experience/brands-management-configuration.png)

Para configurar temas y mensajes para una marca específica, use el panel **Biblioteca de mensajes**.

<!-- Add link to Prompt Library page when available-->

![Administración de indicaciones](/help/assets/brand-centric-experience/prompts-management.png)

## Biblioteca de indicaciones del sector

Para empezar a utilizar indicaciones y temas, Adobe ha creado una biblioteca de indicaciones del sector, que se desarrolló con una amplia investigación de expertos del sector y análisis del comportamiento de la búsqueda por IA en más de 6000 clientes. Esta biblioteca identifica los temas y las indicaciones más relevantes en función de las tendencias específicas del sector, los objetivos comerciales validados y los patrones de búsqueda de clientes reales.

Para usar la biblioteca de indicaciones del sector, haga lo siguiente:

1. Vaya al panel **Biblioteca de mensajes**.
1. Seleccione **Descargar biblioteca de mensajes** para descargar el archivo de biblioteca de LLM Optimizer.
1. Revise los **temas** e **indicaciones** sugeridas para la industria de su marca en la pestaña correspondiente y elija las opciones que sean más relevantes.
1. Revise la **columna fase de Recorrido del cliente** para ver las opciones de solicitud en todo el ciclo de vida del cliente (por ejemplo, la detección para la conversión a retención). La fase inicial/parte superior de las indicaciones de embudo son de alta prioridad, pero también hay que tener en cuenta las opciones de fase posterior para fomentar la retención, habilitar la asistencia al cliente, etc.
1. Modifique los temas o las indicaciones según sea necesario para lograr los objetivos y las metas antes de cargar los temas y las indicaciones en Adobe LLM Optimizer (por ejemplo, añada el nombre de su marca/producto o la terminología coherente con la marca). Las indicaciones se pueden añadir a LLM Optimizer manualmente o con la carga masiva mediante la plantilla *.CSV* proporcionada.

<!--![Industry prompt library download](/help/assets/best-practices/download-prompts.png) - add screenshot to steps-->

>[!TIP]
>
> Utilice una combinación de indicaciones específicas del dominio recomendadas por LLM Optimizer durante la configuración inicial y la biblioteca de indicaciones de la industria para depurar la estrategia de indicaciones.

### Fundación de investigación de la biblioteca de indicaciones

La biblioteca de indicaciones del sector se desarrolló a través de una iniciativa de investigación integral que combina lo siguiente:

* **Conocimiento del cliente:** análisis del comportamiento y las preferencias de la búsqueda por IA en más de 6000 clientes.
* **Experiencia del sector:** perspectivas de expertos en los sectores automotriz, servicios financieros, atención médica, telecomunicaciones y viajes.
* **Perspectivas basadas en datos:** identificación de temas de alto impacto y patrones de consulta que impulsan la participación y conversión de los clientes.

Temas principales buscados por clientes en todos los sectores:

* **Automático:** Resolución de problemas de automóviles, comparación de vehículos y financiación/leasing
* **Servicios financieros:** investigación de productos financieros.
* **Atención médica:** Busca síntomas o problemas de salud, compara opciones de tratamiento y comprende los resultados de laboratorio o los términos médicos
* **Telecomunicaciones:** Comparar planes, términos y promociones de contrato y comprobar el servicio en el área local
* **Viajes en avión:** Prepararse para un viaje, e investigar y reservar viajes

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

<!--How do you pick a region? Or is that handled differently?-->

![Incorporación de categorías en LLM Optimizer](/help/assets/best-practices/create-category1.png)

>[!IMPORTANT]
>
> * Elija un enfoque y manténgase fiel a él.
> * Solo puede tener **un** modelo de categoría por cuenta o marca. No combine **UEN** y **DIR_URL** al mismo tiempo.

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

![Incorporación de temas en LLM Optimizer](/help/assets/best-practices/add-new-topic1.png)

A la hora de crear la lista, tenga en cuenta lo siguiente:

* ¿Puede alguien entender el tema en 5 segundos a partir del texto del mensaje? Si no es así, cambie el nombre o simplifíquelo.
* ¿La corrección de diferentes temas será responsabilidad de un equipo? Si es así, ha elegido temas útiles.

<!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algunas sugerencias útiles adicionales:

* Emplee el conocimiento de su empresa o sitio para definir temas que se ajusten a los objetivos estratégicos de su marca.
* Considere cómo se compara su marca con otras dentro de temas específicos.

>[!IMPORTANT]
>
> * Mantenga los temas basados en intenciones, no en la organización.
> * No agregue categorías/filtros para marcas/no marcas/zonas geográficas, ya que puede filtrar específicamente para esto en el panel **[!UICONTROL Presencia de marca]**.
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

El seguimiento de otras marcas le permite supervisar la visibilidad y las menciones de las respuestas de LLM en busca de preguntas y temas importantes para su empresa.

[!UICONTROL **Otras marcas para rastrear**] está disponible en **Administración de marcas** > **Seguimiento de mercados** y le permite agregar otras, incluyendo competidores, para rastrear su visibilidad en preguntas y temas específicos.

Con otras marcas que rastrear, puede ver con qué frecuencia se mencionan otras marcas junto con su marca en diferentes regiones y categorías y comparar su visibilidad con la suya propia.

>[!TIP]
>
>Revise periódicamente las menciones y citas de la competencia o de otras personas para identificar las áreas en las que su marca puede mejorar.

## Más información

* [Administración de marcas](/help/dashboards/customer-configuration.md) es donde configuras tus categorías y otras marcas para que las rastreen.
* [Biblioteca de mensajes](/help/dashboards/customer-configuration.md) es donde se configuran los temas y mensajes.
* [Prácticas recomendadas en LLM Optimizer](/help/tutorials/best-practices.md) describe las prácticas recomendadas en la optimización de LLM

