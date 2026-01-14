---
title: Prácticas recomendadas para categorías, temas, indicadores y otros
description: Optimice las perspectivas de LLM configurando categorías, temas, indicadores y otras marcas para rastrear, incluyendo a la competencia, para monitorizar marcas personalizadas y analizar contenido estratégico.
feature: Best Practices, Customer Configuration
source-git-commit: a4dd9b1aece2936fb95a2e831ec8b41946bc5f46
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Prácticas recomendadas para configurar categorías, temas, indicadores y otros para realizar seguimientos

En esta sección se describen las prácticas recomendadas para decidir cómo desea configurar las categorías, los temas, los indicadores y otros elementos para realizar un seguimiento. Además, incluye información sobre la Biblioteca de indicadores del sector, que Adobe desarrolló con una amplia investigación con expertos del sector.

Este es un primer paso vital. Lo que decida ahora determina cómo se adapta la información a su contexto empresarial. Cualquier cambio en las categorías en el futuro restablecerá los datos históricos.

En el tablero de [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) se define cómo se supervisará y analizará su marca dentro de la plataforma del optimizador LLM. Consulte [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) para obtener información sobre cómo usar el tablero.

![Ventana de configuración del cliente](/help/assets/best-practices/customer-configuration-best-practices.png)

En el panel [!UICONTROL Configuración del cliente], puede personalizar categorías (como unidades de negocio o líneas de productos), realizar un seguimiento de otras marcas y agregar alias de mención de marcas para capturar todas las variaciones de su marca en las distintas indicaciones. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

## Biblioteca de indicadores del sector

Para ayudarle a empezar a usar las indicaciones y los temas, Adobe ha creado una biblioteca de indicaciones del sector, que se ha desarrollado mediante una amplia investigación con expertos del sector y análisis del comportamiento de búsqueda de IA en más de 6000 clientes. Esta biblioteca identifica los temas y los indicadores más relevantes en función de las tendencias específicas del sector, los objetivos empresariales validados y los patrones de búsqueda de clientes en el mundo real.

Para usar la Biblioteca de indicadores del sector:

1. Descargue el archivo de la biblioteca Prompt de LLM Optimizer navegando hasta el panel **Configuración del cliente**.
2. Revise los **temas** y **indicadores** sugeridos para el sector de su marca en la ficha correspondiente y elija las opciones que sean más relevantes.
3. Revise la **columna Fase de Recorrido del cliente** para ver las opciones de solicitud en todo el ciclo de vida del cliente (por ejemplo, la detección para la conversión a retención). La fase inicial/parte superior de las solicitudes de funnel son de alta prioridad, pero también hay que tener en cuenta las opciones de fase posterior para fomentar la retención, habilitar la asistencia al cliente, etc.
4. Modifique los temas o las indicaciones según sea necesario para lograr sus objetivos y metas antes de cargarlos en Adobe LLM Optimizer (por ejemplo, añada su nombre de marca/producto, agregue terminología propia de la marca). Los indicadores se pueden agregar a LLMO manualmente o cargados en lotes mediante la plantilla *.csv* proporcionada.

>[!TIP]
>
> Utilice una combinación de indicadores específicos del dominio recomendados por LLM Optimizer durante la configuración inicial y la Biblioteca de indicadores del sector para depurar la estrategia de mensajes.

### Prompt Library Research Foundation

La Industry Prompt Library se desarrolló a través de una iniciativa de investigación integral que combina lo siguiente:

* **Inteligencia de clientes:** análisis del comportamiento y las preferencias de búsqueda de IA entre más de 6000 clientes
* **Experiencia en la industria:** Perspectivas de expertos en los sectores automotriz, servicios financieros, atención médica, telecomunicaciones y viajes.
* **Perspectivas basadas en datos:** Identificación de temas de alto impacto y patrones de consulta que impulsan la participación y conversión de los clientes.

Temas principales buscados por clientes en todos los sectores:

* **Automático:** Resolución de problemas de automóviles, Comparación de vehículos y Financiación/Leasing
* **Servicios financieros:** Investigación de productos financieros
* **Atención médica:** Busca síntomas o problemas de salud, Compara opciones de tratamiento, Entiende los resultados de laboratorio o los términos médicos
* **Telecomunicaciones:** Comparando planes, términos y promociones del contrato, comprobando el servicio en el área local
* **Viajes:** Preparación para un viaje, Investigación y reserva de viajes

Tendencias del cliente sobre la búsqueda de IA y el comportamiento del prompt en las herramientas LLM:

* Los clientes prefieren hacer preguntas en lugar de utilizar palabras clave al utilizar las herramientas de búsqueda de LLM.
* Utilizan principalmente herramientas de búsqueda LLM para la investigación y el descubrimiento en las primeras etapas.
* Los clientes tienden a mencionar una marca o un nombre de producto específico en sus mensajes.

## Prácticas recomendadas para categorías

Las categorías permiten organizar el contenido en unidades de negocio estratégicas o agrupaciones lógicas. Son el bloque &quot;donde pertenece&quot; y la estructura organizativa de nivel superior para su contenido.

Al decidir cómo configurar categorías, debe tener en cuenta sus objetivos y quién debe actuar en función de lo que esté informando.

>[!IMPORTANT]
>
> Asegúrese de que las categorías estén correctamente configuradas desde el principio, ya que los cambios en las categorías restablecen los datos históricos. Esto significa que, si los cambia, perderá datos históricos de antes del cambio.

A continuación se muestra una descripción general de los tipos de enfoques que puede adoptar y cuándo elegir un enfoque concreto:

| Enfoque | Descripción | Ventaja |
|---------|----------|---------|
| Unidad Estratégica de Negocio (SBU) | Utilice este método si su organización está dividida por pérdidas y ganancias (por ejemplo, consumidores, empresas, servicios). | Obtendrá informes limpios por línea de negocio y una responsabilidad más sencilla. |
| Directorio de nivel superior del sitio web (URL_DIR) | Utilícelo si la arquitectura de información del sitio refleja la propiedad (/products/, /support/, /docs/, /news/). | Puede alinearse con la forma en que los equipos publican y mantienen el contenido. |
| Categoría del producto (o servicio) | Utilícelo si vende un catálogo (SKU/servicios). | Obtendrá vistas de surtido, análisis de brechas y respuestas de &quot;qué categoría necesita contenido&quot;. |

La forma de decidir cómo se configuran las categorías se basa en una pregunta: **¿Quién debe modificar el informe?**

* Si usted es un *líder empresarial*, elija el enfoque de **SBU**.
* Si usted es *propietario de contenido/web*, elija el método **URL_DIR**.
* Si usted es un *administrador de ofertas/comercialización*, elija el enfoque de **categoría de producto/servicio**.

![Agregando categorías en LLM Optimizer](/help/assets/best-practices/add-category.png)

>[!IMPORTANT]
>
> * Elige un enfoque y apégate a él.
> * Solo puede tener **un** modelo de categoría por cuenta o marca. No mezcles **SBU** y **URL_DIR** al mismo tiempo.
<!--Can you mix Product/Service with these?-->

Ejemplo:

| Tipo de sitio | Categoría | Ejemplos de taxonomía de temas |
|---------|----------|---------|
| Empresas con varios negocios | SBU | Conjunto de intención pequeño (procedimientos, resolución de problemas, comparación, precios, política) |
| Documentación/sitio con gran presencia de asistencia | URL_DIR | Instrucciones, resolución de problemas, referencia, notas de la versión |
| Catálogo de eCommerce/Services | Producto/servicio | Comparación, comentarios, precios/disponibilidad, procedimientos, resolución de problemas |

## Prácticas recomendadas por temas

Los temas le ayudan a comprender la intención del usuario: le muestran lo que este quiere. Permiten agrupar indicadores con una intención de usuario similar. Piense en ello como agrupar los indicadores relevantes.

>[!IMPORTANT]
>
>Los temas son universales en **todas** las categorías, lo que significa que permanecen consistentes independientemente de la categoría a la que estén asignados. Representan grupos de preguntas o indicadores que comparten una intención común.

Al decidir los temas, desea crear una lista corta y plana (de 6 a 12 como máximo). Por ejemplo:

* Productos/servicios
* Procedimientos (configuración/uso)
* Solución de problemas (errores/problemas)
* Comparación (X frente a Y; &quot;mejor... para...&quot;)
* Opiniones y valoraciones
* Precios y disponibilidad
* Política y garantía
* Contacto de asistencia
* Corporativo/Noticias (si realmente lo necesita)

![Agregando temas en LLM Optimizer](/help/assets/best-practices/add-topic.png)

Al crear la lista, tenga en cuenta lo siguiente:

* ¿Puede un editor comprender el tema en 5 segundos desde el texto del mensaje? Si no es así, cambie el nombre o simplifique.
* ¿Será propiedad de un equipo diferente la corrección de diferentes temas? Si es así, ha elegido temas útiles.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algunas sugerencias útiles adicionales:

* Use el conocimiento de su negocio o sitio para definir temas que se alineen con los objetivos estratégicos de su marca
* Considere cómo se compara su marca con otras dentro de temas específicos.

>[!IMPORTANT]
>
> * Mantenga los temas basados en intenciones, no en la organización.
> * No agregue categorías/filtros para marcas/no marcas/zonas geográficas, ya que puede filtrar específicamente para esto en la pestaña **[!UICONTROL Marcas]**.
> * Los temas se distribuyen en varias categorías. Usted **no puede** definir temas únicos para cada categoría.
> * Un solo mensaje **can** existe en varios temas o categorías.

## Prácticas recomendadas para mensajes

Los indicadores identifican las preguntas o consultas específicas que los clientes formulan y que pueden afectar a su negocio. Son las preguntas o consultas reales que los usuarios introducen en los LLM.

Asegúrese de revisar y actualizar las solicitudes regularmente para asegurarse de que se alinean con las necesidades del cliente y los objetivos empresariales.

Prácticas recomendadas para mensajes:

* Agrupe indicaciones similares en función de lo que pregunte la gente.
* Céntrese en las indicaciones que sean más importantes para sus clientes.
* Compruebe si su marca tiene buenas posibilidades de que se le mencione en relación con determinadas indicaciones.

>[!TIP]
>
>* Puede utilizar herramientas como Adobe LLM Optimizer y la consola de búsqueda de Google con filtros regex para identificar estructuras de preguntas comunes (por ejemplo, &quot;cómo&quot;, &quot;qué&quot;, &quot;cuándo&quot;, &quot;dónde&quot;) y averiguar las indicaciones que utilizan los visitantes para visitar el sitio.
>* Para saber qué indicadores son relevantes para su sitio/marca, puede utilizar datos de búsqueda en el sitio, preguntas frecuentes en las páginas de resultados de motores de búsqueda o incluso preguntar directamente a los bots de chat de LLM qué preguntas podrían hacer los clientes sobre su marca.

## Prácticas recomendadas para rastrear otras marcas

El seguimiento de otros le permite supervisar la visibilidad y las menciones de las respuestas de LLM en busca de preguntas y temas que son importantes para su negocio.

La pestaña [!UICONTROL **Seguimiento de otros**] le permite agregar otros, incluidos competidores, para rastrear su visibilidad en busca de indicadores y temas específicos.

Con el seguimiento de otros, puede ver con qué frecuencia se mencionan otras marcas junto con su marca en diferentes regiones y categorías y comparar su visibilidad con la suya propia.

>[!TIP]
>
>Revise regularmente las menciones y citas de competidores u otras personas para identificar las áreas en las que su marca puede mejorar.

## Más información

* [Panel de configuración del cliente](/help/dashboards/customer-configuration.md) es donde se configuran las categorías, los temas, los mensajes y el seguimiento de otros.
* [Prácticas recomendadas de LLM Optimizer](/help/tutorials/best-practices.md) describe las prácticas recomendadas en la optimización de LLM

