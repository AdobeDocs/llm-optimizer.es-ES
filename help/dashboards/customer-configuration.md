---
title: Configuración del cliente
description: Utilice la configuración del cliente para definir cómo se supervisará y analizará su marca dentro de la plataforma del optimizador LLM.
source-git-commit: a37c4e7d2e26f16dc10dc7bc39ba58ba1df77cd5
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---


# Configuración del cliente {#customer-configuration}

El panel de configuración del cliente es una potente herramienta que proporciona perspectivas sobre la visibilidad de su marca en los LLM. Al configurar correctamente categorías, temas y mensajes, puede asegurarse de que la marca esté bien posicionada para aparecer en las respuestas generadas por LLM. Esta configuración garantiza que la plataforma adapte las perspectivas a su contexto empresarial, lo que permite una visibilidad precisa, el tráfico y el análisis de oportunidades.

![Panel de configuración del cliente](/help/dashboards/assets/customer-config.png)

Para configurar cómo LLM Optimizer monitoriza y analiza su presencia de marca en diferentes mercados y entornos competitivos, tiene acceso a las siguientes pestañas:

* [Categorías](#categories)
* [Seguimiento de otros](#others-tracking)
* [Alias de marca](#brand-aliases)
* [Data Insights](#data-insights)
* [Configuración de la CDN](#agentic-cdn)

>[!IMPORTANT]
>
> Para obtener más información sobre cómo configurar las categorías, temas y preguntas, consulte la página [Prácticas recomendadas para configurar categorías, temas y preguntas](/help/overview/best-practices-topics-prompts.md).

## Categorías {#categories}

Desde la pestaña Categorías, puede definir las categorías de negocio o las líneas de producto que desea rastrear y asociarlas a regiones específicas. En general, la pestaña Categorías está relacionada con casi todas las demás personalizaciones de esta página, ya que las categorías aparecen en el campo Categoría para las demás personalizaciones (seguimiento de otras, alias, etc.). Para agregar una nueva categoría:

1. Haga clic en el botón **Agregar**.
2. En la nueva ventana de configuración, agregue **Nombre de categoría**.
3. Personalice la **región asociada** donde se supervisará la categoría.
4. Haz clic en **Guardar** y la nueva categoría aparecerá en la lista de categorías.

Añadir nuevas categorías no generará automáticamente temas ni peticiones de datos, estos deberán añadirse manualmente desde la pestaña [Data Insights](#data-insights).

Para eliminar una categoría, haga clic en el icono Eliminar de la lista de categorías. Tenga cuidado, porque **al eliminar una categoría también se eliminarán los elementos asociados**, como alias de marca vinculados a esa categoría específica.

## Seguimiento de otros {#others-tracking}

Con esta pestaña, puede realizar un seguimiento de cómo se mencionan los demás en relación con su marca en diferentes categorías y regiones. Monitorice su presencia y rendimiento en sus segmentos de mercado. Para personalizar el seguimiento:

1. Haga clic en el botón **Agregar**.
2. En la nueva ventana de configuración, seleccione **Categoría**. Las categorías creadas anteriormente aparecerán aquí.
3. Añada el nombre del otro.
4. Personalice los demás alias y dominios si es necesario.
5. Haga clic en **Guardar**.

Para eliminar una entrada de la lista, haga clic en el icono Eliminar.

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

## Configuración de la CDN {#cdn-configuration}

Desde esta pestaña, puede configurar los flujos de CDN para permitir que Adobe LLM Optimizer analice los datos de CDN. Estos datos se utilizarán para impulsar los paneles (como el tráfico de la Agencia), lo que proporcionará perspectivas sobre los patrones de tráfico, las métricas de rendimiento y las oportunidades de optimización. Para incorporar su proveedor de CDN, haga clic en **Incorporar CDN**.

![CDN de configuración de cliente](/help/overview/assets/cc-cdn.png)

En la ventana **Incorporar proveedor de CDN**:

1. Seleccione su proveedor de CDN.
2. Haga clic en **Incorporar** para habilitar el reenvío de registros.

Si seleccionas **Otro**, tendrás que ponerte en contacto con Adobe para obtener ayuda.
