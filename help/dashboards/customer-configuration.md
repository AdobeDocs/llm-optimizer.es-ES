---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se supervisará y analizará su marca dentro de la plataforma del optimizador LLM.
source-git-commit: 653a6be856412faac8783fa9dc7b759a7c6e1f68
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---


# Configuración del cliente

Configuración del cliente es donde se define cómo se supervisará y analizará la marca dentro de la plataforma del optimizador de LLM. Puede personalizar categorías (como unidades de negocio o líneas de productos), rastrear competidores y agregar alias de mención de marca para capturar todas las variaciones de su marca en los mensajes. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

![Panel de configuración del cliente](/help/dashboards/assets/customer-config.png)


## Prácticas recomendadas para configurar categorías, temas y preguntas

En esta sección se describen las prácticas recomendadas para decidir cómo desea configurar las categorías, los temas, los mensajes y la competencia.

Este es un primer paso vital. Lo que decida ahora determina cómo se adapta la información a su contexto empresarial. Cualquier cambio en las categorías en el futuro restablecerá los datos históricos.

### Prácticas recomendadas para categorías

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

Ejemplo:

| Tipo de sitio | Categoría | Ejemplos de taxonomía de temas |
|---------|----------|---------|
| Empresas con varios negocios | SBU | conjunto de intención pequeño (procedimientos, resolución de problemas, comparación, precios, política) |
| Documentación/sitio con gran presencia de asistencia | URL_DIR | Instrucciones, resolución de problemas, referencia, notas de la versión |
| Catálogo de eCommerce/Services | Producto/servicio | Comparación, comentarios, precios/disponibilidad, procedimientos, resolución de problemas |

### Prácticas recomendadas por temas

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
* Corporativo / Noticias (si realmente los necesita)

Al crear la lista, tenga en cuenta lo siguiente:

* ¿Puede un editor comprender el tema en 5 segundos desde el texto del mensaje? Si no es así, cambie el nombre o simplifique.
* ¿Será propiedad de un equipo diferente la corrección de diferentes temas? Si es así, ha elegido temas útiles.

Algunas sugerencias útiles adicionales:

* Use el conocimiento de su negocio o sitio para definir temas que se alineen con los objetivos estratégicos de su marca
* Considere cómo se compara su marca con la competencia dentro de temas específicos.

>[!IMPORTANT]
>
> * Mantenga los temas basados en intenciones, no en la organización.
> * No agregue categorías/filtros para marcas/no marcas/zonas geográficas, ya que puede filtrar específicamente para esto en la pestaña **Marcas**.
> * Los temas se distribuyen en varias categorías. **no** puede tener diferentes temas por categoría.
> * Una sola solicitud puede existir en varios temas o categorías.

### Prácticas recomendadas para mensajes

Los indicadores identifican las preguntas o consultas específicas que los clientes formulan y que pueden afectar a su negocio. Son las preguntas o consultas reales que los usuarios introducen en los LLM.

Asegúrese de revisar y actualizar las solicitudes regularmente para asegurarse de que se alinean con las necesidades del cliente y los objetivos empresariales.

>[!TIP]
>
>* Puede utilizar herramientas como LLM Optimizer y la consola de búsqueda de Google con filtros regex para identificar estructuras de preguntas comunes (por ejemplo, &quot;cómo&quot;, &quot;qué&quot;, &quot;cuándo&quot;, &quot;dónde&quot;).
>* Para saber qué indicadores son relevantes para su sitio/marca, puede utilizar datos de búsqueda en el sitio, preguntas frecuentes en las páginas de resultados de motores de búsqueda o incluso preguntar directamente a los bots de chat de LLM qué preguntas podrían hacer los clientes sobre su marca.

### Prácticas recomendadas para la competencia

Los competidores le permiten supervisar la visibilidad y las menciones en las respuestas de LLM para obtener indicaciones y temas que son importantes para su negocio.

La pestaña [!UICONTROL **Seguimiento de competidores**] le permite agregar competidores y rastrear su visibilidad para preguntas y temas específicos.

Con el seguimiento de competidores, puede ver con qué frecuencia se mencionan los competidores junto con su marca en diferentes regiones y categorías y comparar su visibilidad con la suya propia.

>[!TIP]
>
>Revise regularmente las menciones y citas de los competidores para identificar las áreas en las que su marca puede mejorar.

## Panel de configuración del cliente

El panel de configuración del cliente es una potente herramienta que proporciona perspectivas sobre la visibilidad de su marca en los LLM. Al configurar correctamente categorías, temas, indicadores y competidores, puede asegurarse de que su marca esté bien posicionada para aparecer en las respuestas generadas por LLM. Revisar regularmente perspectivas como la Cuota de voz, la visibilidad del contenido y las oportunidades le ayudará a adaptar su estrategia y a adelantarse a la competencia.

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Categorías](#categories)
* [Seguimiento de competidores](#competitor-tracking)
* [Alias de marca](#brand-aliases)
* [Data Insights](#data-insights)
* [CDN agéntico](#agentic-cdn)

## Categorías {#categories}

Desde la pestaña Categorías, puede definir las categorías empresariales o las líneas de producto que desea rastrear y asociarlas a regiones específicas. En general, la pestaña Categorías está relacionada con cualquier otra personalización de esta página, ya que las categorías aparecen en el campo Categoría para las demás personalizaciones (seguimiento de competidores, alias, etc.). Para agregar una nueva categoría:

1. Haga clic en el botón **Agregar**.
2. En la nueva ventana de configuración, agregue **Nombre de categoría**.
3. Personalice la **región asociada** donde se supervisará la categoría.
4. Haz clic en **Guardar** y la nueva categoría aparecerá en la lista de categorías.

Añadir nuevas categorías no generará automáticamente temas ni peticiones de datos, estos deberán añadirse manualmente desde la pestaña [Data Insights](#data-insights).

Para eliminar una categoría, haga clic en el icono Eliminar de la lista de categorías. Tenga cuidado, ya que **al eliminar una categoría también se eliminarán los elementos asociados**, como competidores, que podría haber configurado o alias de marca vinculados a esa categoría específica.

## Seguimiento de competidores {#competitor-tracking}

Mediante el seguimiento de competidores, puede rastrear cómo se mencionan sus competidores en relación con su marca en diferentes categorías y regiones. Monitorice su presencia y rendimiento en sus segmentos de mercado. Para personalizar el seguimiento de la competencia:

1. Para agregar un nuevo competidor, haz clic en el botón **Agregar**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Añada el nombre del competidor.
4. Personalice el Alias y los Dominios del competidor si es necesario.
5. Haz clic en **Guardar** y el nuevo competidor aparecerá en la lista de la competencia.

Para eliminar un competidor, haga clic en el icono Eliminar de la lista de competidores.

## Alias de marca {#brand-aliases}

Mediante alias de marca, puede configurar nombres alternativos y variaciones de su marca que deben rastrearse en diferentes categorías y regiones. Esto garantiza una monitorización completa de todas las menciones de marca. Para añadir un alias de marca:

1. Haga clic en el botón **Agregar**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Seleccione la **región** donde se supervisará el alias.
4. Añada el alias de la marca.
5. Haz clic en **Guardar** y el alias de la marca aparecerá en la lista.

Para eliminar un alias de marca, haga clic en el icono Eliminar de la lista de alias.

## Data Insights {#data-insights}

Desde esta pestaña, puede revisar, administrar y personalizar las solicitudes. Puede cargar un archivo .csv con [datos de presencia de marca](/help/dashboards/brand-presence.md#data-insights) y la lista se rellenará con preguntas y temas de ese análisis. También puede eliminar, modificar y agregar temas y sus indicadores asociados según sea necesario.

Para importar un archivo .csv de perspectivas de datos, primero debe exportar un archivo desde el panel de presencia de marca. Consulte la sección [data insights](/help/dashboards/brand-presence.md#data-insights) para obtener información sobre cómo hacerlo. Una vez que tenga el archivo:

1. En el panel, haga clic en **Cargar CSV**.
2. En la ventana Importar datos de Insights, arrastre y suelte o elija manualmente el archivo.
3. Haga clic en **Cargar datos**.

También puede crear un nuevo archivo CSV descargando la plantilla desde la ventana **Importar datos**. Una vez que tenga la plantilla, ábrala e introduzca los temas junto con sus peticiones de datos, categorías y regiones asociadas, cada uno en una nueva línea.

Además, también puede agregar temas/peticiones de datos a la lista independientemente de un archivo CSV. Para conseguirlo, en el panel, debe hacer lo siguiente:

1. Haga clic en el botón **Agregar tema**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Introduzca el nombre del tema.
4. Añada el texto del mensaje.
5. Seleccione la región.
6. Haga clic en **Agregar solicitud** y el tema con la solicitud aparecerá en la lista.

>[!NOTE]
>Los mensajes añadidos recientemente no aparecerán en la presencia de marca hasta que se complete el procesamiento.

En la lista, puede hacer clic en cada tema y aparecerán las peticiones de datos asociadas. Para eliminar el tema y sus peticiones de datos asociadas, haga clic en el icono Eliminar de la lista.

## CDN agéntico {#agentic-cdn}

No disponible (¿estará disponible para el lanzamiento?).

