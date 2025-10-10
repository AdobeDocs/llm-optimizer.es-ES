---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se supervisará y analizará su marca dentro de la plataforma del optimizador LLM.
source-git-commit: 7d01b35cb2153e020f0b64e493aad263fb9bb09f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Configuración del cliente

Configuración del cliente es donde se define cómo se supervisará y analizará la marca dentro de la plataforma del optimizador de LLM. Puede personalizar categorías (como unidades de negocio o líneas de productos), rastrear competidores y agregar alias de mención de marca para capturar todas las variaciones de su marca en los mensajes. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

![Panel de configuración del cliente](/help/dashboards/assets/customer-config.png)

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Categorías](#categories)
* [Seguimiento de competidores](#competitor-tracking)
* [Alias de marca](#brand-aliases)
* [Data Insights](#data-insights)
* [CDN agéntico](#agentic-cdn)

## Categorías {#categories}

Desde la pestaña Categorías, puede definir las categorías empresariales o las líneas de producto que desea rastrear y asociarlas a regiones específicas. En general, la pestaña Categorías está relacionada con cualquier otra personalización de esta página, porque las categorías aparecerán en el campo Categoría para las demás personalizaciones (seguimiento de competidores, alias, etc.). Para agregar una nueva categoría:

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

