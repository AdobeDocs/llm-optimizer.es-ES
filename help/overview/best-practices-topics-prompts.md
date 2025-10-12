---
title: Prácticas recomendadas para categorías, temas e indicadores
description: Optimice las perspectivas de LLM configurando categorías, temas, indicadores y competidores para un seguimiento de marca y un análisis de contenido estratégico personalizados.
source-git-commit: c7c66566137ad1f5bda89f55748b9d81ddf36f76
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# Prácticas recomendadas para configurar categorías, temas, mensajes y competidores

En esta sección se describen las prácticas recomendadas para decidir cómo desea configurar las categorías, los temas, los mensajes y la competencia.

Este es un primer paso vital. Lo que decida ahora determina cómo se adapta la información a su contexto empresarial. Cualquier cambio en las categorías en el futuro restablecerá los datos históricos.

En el tablero de [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) se define cómo se supervisará y analizará su marca dentro de la plataforma del optimizador LLM. Consulte [[!UICONTROL Configuración del cliente]](/help/dashboards/customer-configuration.md) para obtener información sobre cómo usar el tablero.

![Ventana de configuración del cliente](/help/assets/best-practices/customer-configuration-best-practices.png)

En el tablero de [!UICONTROL Configuración del cliente], puede personalizar categorías (como unidades de negocio o líneas de productos), rastrear competidores y agregar alias de mención de marca para capturar todas las variaciones de su marca en los mensajes. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

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

>[!IMPORTANT]
>
> * Elige un enfoque y apégate a él.
> * Solo puede tener **un** modelo de categoría por cuenta o marca. No mezcles **SBU** y **URL_DIR** al mismo tiempo.
>   <!--Can you mix Product/Service with these?-->

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

Al crear la lista, tenga en cuenta lo siguiente:

* ¿Puede un editor comprender el tema en 5 segundos desde el texto del mensaje? Si no es así, cambie el nombre o simplifique.
* ¿Será propiedad de un equipo diferente la corrección de diferentes temas? Si es así, ha elegido temas útiles.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algunas sugerencias útiles adicionales:

* Use el conocimiento de su negocio o sitio para definir temas que se alineen con los objetivos estratégicos de su marca
* Considere cómo se compara su marca con la competencia dentro de temas específicos.

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

## Prácticas recomendadas para la competencia

Los competidores le permiten supervisar la visibilidad y las menciones en las respuestas de LLM para obtener indicaciones y temas que son importantes para su negocio.

La pestaña [!UICONTROL **Seguimiento de competidores**] le permite agregar competidores y rastrear su visibilidad para preguntas y temas específicos.

Con el seguimiento de competidores, puede ver con qué frecuencia se mencionan los competidores junto con su marca en diferentes regiones y categorías y comparar su visibilidad con la suya propia.

>[!TIP]
>
>Revise regularmente las menciones y citas de los competidores para identificar las áreas en las que su marca puede mejorar.

## Más información

* [Panel de configuración del cliente](/help/dashboards/customer-configuration.md) es donde configuras tus categorías, temas, mensajes y competidores.
* [Prácticas recomendadas de LLM Optimizer](/help/tutorials/best-practices.md) describe las prácticas recomendadas en la optimización de LLM

