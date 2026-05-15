---
title: Enriquecimiento del catálogo de productos
description: Descubra cómo LLM Optimizer identifica productos con descripciones genéricas o técnicamente densas y cómo mejorarlos mediante enriquecimientos narrativos generados por IA con tecnología Adobe Commerce.
feature: Opportunities
autotag-review: '2026-05-15T17:45:51.619Z'
TQID: 'https://experienceleague.adobe.com/5ihGQ8L-37uWsZSDo4TVCUPBPqsqqQ5waGbH3VKPIig'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1266
ht-degree: 0%

---


# Enriquecimiento del catálogo de productos

Los LLM intentan conectar los atributos del producto con el valor real, los casos de uso y la intención del comprador. Cuando los nombres y las descripciones de los productos no comunican claramente ese valor, es menos probable que sus productos se citen, recomienden o aparezcan en un descubrimiento impulsado por IA. Esto se debe a que los agentes de IA razonan a través de relaciones, no de campos de datos sin procesar. Una lista de productos con un nombre como &quot;Coffee Grinder X200&quot; y una descripción que enumera las especificaciones técnicas (potencia del motor, configuración de molienda, etc.) da a un LLM muy poco con lo que trabajar cuando un comprador pide &quot;el mejor molinillo de espresso para un barista casero&quot;.

La oportunidad de enriquecimiento del catálogo de productos identifica los productos del catálogo de Commerce donde los nombres y las descripciones son demasiado genéricos, demasiado densos técnicamente o demasiado ambiguos para que los LLM los interpreten con precisión. Con la tecnología de Adobe Commerce, genera enriquecimientos basados en narrativas e intencionados para los nombres y descripciones de sus productos y los aplica directamente al catálogo de Commerce con un solo clic.

De un vistazo, muestra dos métricas clave:

- **URL**: una lista de páginas de detalles del producto (productos del catálogo) que se han evaluado para comprobar la calidad del enriquecimiento.
- **Tráfico agéntico**: El total de visitas e interacciones en un sitio que inician e impulsan agentes de IA autónomos (como asistentes o bots con tecnología LLM) que actúan en nombre de usuarios para descubrir, recuperar o interactuar con contenido.

![Enriquecer el tablero del catálogo de productos](/help/dashboards/opportunities/assets/enrich-product-catalog-overview.png)

>[!NOTE]
>
>Actualmente, esta oportunidad está en Beta y los clientes de Adobe Commerce pueden activarla. Póngase en contacto con el administrador de su cuenta para obtener acceso a la versión beta.

## Funcionamiento

El agente de catálogo de Adobe Commerce lee los datos del catálogo de productos y analiza cada SKU de producto, incluidos todos sus atributos técnicos, contexto de categoría, variantes y nombre y descripción existentes. Identifica los productos en los que el nombre o la descripción actuales no comunican el valor relevante para el comprador y genera una alternativa enriquecida que traduce los detalles técnicos a un lenguaje claro y alineado con la intención.

Por ejemplo, un producto llamado *&quot;Coffee Grinder X200&quot;* con una descripción que enumera &quot;18 ajustes de molienda, motor de 450 W&quot; puede enriquecerse para explicar que &quot;El X200 ofrece consistencia de espresso a nivel de café porque su sistema de molienda de 18 pasos está emparejado con un motor de alto par para obtener resultados repetibles en casa&quot;. Los atributos como el precio y el inventario se excluyen intencionadamente del enriquecimiento: el agente de catálogo se centra en atributos que impulsan el valor y explican qué es el producto, cómo se utiliza y por qué importa a un comprador.

Los productos con sugerencias de enriquecimiento aparecen en la tabla **URL con sugerencias**, priorizados por el impacto de enriquecimiento. Para cada producto identificado, LLM Optimizer proporciona:

- **Nombre actual**: el nombre del producto existente tal como aparece en su catálogo de Adobe Commerce.
- **Nombre actualizado**: el nombre del producto generado por IA y basado en valores que comunica el contexto y la intención relevantes para el comprador a los LLM.
- **Descripción actual**: la descripción del producto existente tal como aparece en su catálogo de Adobe Commerce.
- **Descripción sugerida**: la descripción generada por IA que traduce los atributos técnicos del producto en una narrativa que ayuda a los LLM a comprender qué es el producto, el valor narrativo y por qué importa.

![Productos con tabla de sugerencias](/help/dashboards/opportunities/assets/enrich-product-catalog-suggestions.png)

## Productos con sugerencias

La tabla **URL con sugerencias** enumera todos los productos con oportunidades de enriquecimiento. Para cada producto puede:

- **Expanda la fila** para ver el análisis de IA y el enriquecimiento propuesto.
- **Edite** el nombre o la descripción del producto propuesto antes de aplicar, para alinearlo con las directrices de comercialización y voz de su marca.
- **Implemente la optimización** para los productos que desea enriquecer y publíquelo directamente en su catálogo de Adobe Commerce.
- **Marcar como fijo** una vez que se haya revisado y aplicado el enriquecimiento.
- **Ignorar** sugerencias que no sean relevantes para su estrategia de catálogo.

Las sugerencias están organizadas en tres vistas: **Sugerencias actuales**, **Sugerencias fijas** y **Sugerencias ignoradas**. Una vez aplicado un enriquecimiento, pasa a Fixed Suggestions con un estado de **Applied** y una acción de **View in Catalog** para comprobar la actualización en Adobe Commerce. Los enriquecimientos aplicados se pueden revertir en cualquier momento, restaurando el nombre y la descripción del producto original.

<!--[Fixed suggestions with Applied status](/help/dashboards/opportunities/assets/enrich-product-catalog-fixed.png)-->

## Implementación de la optimización

Una vez que haya revisado y opcionalmente editado las sugerencias para los productos seleccionados, haga clic en **Implementar optimizaciones** para publicar el nombre y la descripción actualizados del producto en su catálogo de Adobe Commerce. Un cuadro de diálogo de confirmación muestra los productos seleccionados y los cambios que se aplican. Después de la confirmación, una pantalla de resultados confirma qué productos se actualizaron correctamente.

Dado que los enriquecimientos se aplican directamente al catálogo de Adobe Commerce, los nombres y las descripciones de los productos actualizados están disponibles de inmediato en todos los canales que utilizan el catálogo, incluidos los escaparates, las fuentes de anuncios y cualquier integración directa de productos de LLM. Esto garantiza que cada superficie donde aparezca su producto comunique información coherente y de alta calidad.

>[!NOTE]
>
>El enriquecimiento de catálogo requiere que LLM Optimizer esté conectado a Adobe Commerce. Si la instancia de Commerce aún no está conectada a LLM Optimizer, se le dirigirá a la configuración de conexión antes de que se puedan aplicar los enriquecimientos.

![Cuadro de diálogo Aplicar enriquecimientos](/help/dashboards/opportunities/assets/enrich-product-catalog-deploy.png)

## Probar en la demostración

Vea la oportunidad de enriquecer el catálogo de productos en acción usando el entorno de demostración de Frescopa.

[Ver el catálogo de productos enriquecidos en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Preguntas frecuentes

**¿Por qué los nombres de productos genéricos y las descripciones dañan la detección de IA?**

Los LLM no hacen coincidir productos con consultas de comprador buscando superposición de palabras clave. Razonan sobre las relaciones, conectando lo que un comprador intenta encontrar con lo que un producto realmente hace, para quién es y cómo se compara con las alternativas. Un nombre o una descripción de producto que enumera especificaciones técnicas sin comunicar el valor real proporciona a un LLM muy poco contexto para trabajar. El resultado es que es menos probable que se cite su producto cuando un comprador hace una pregunta relevante, incluso si su producto es el mejor para satisfacer sus necesidades.

**¿Qué atributos de producto utiliza el agente de catálogo para generar enriquecimientos?**

El agente de catálogo utiliza atributos que impulsan el valor en su catálogo Commerce y que ayudan a los LLM a comprender qué es un producto, cómo se utiliza y por qué importa. Atributos que impulsan el valor, como funciones de producto, casos de uso, propiedades de material, contexto de categoría y detalles de compatibilidad. Los atributos como el precio y los niveles de inventario se excluyen intencionalmente, ya que no contribuyen a la comprensión semántica del producto y pueden hacer que las descripciones sean menos duraderas a medida que cambian las condiciones.

**¿Puedo editar el enriquecimiento generado por IA antes de aplicarlo?**

Sí. Cada sugerencia incluye una previsualización editable del nombre y la descripción del producto propuesto. Puede modificar el enriquecimiento para alinearlo con la voz de su marca, corregir cualquier inexactitud o incorporar contexto adicional antes de aplicarlo al catálogo.

**¿Cambiará el enriquecimiento lo que los visitantes humanos ven en mi tienda?**

Sí, los visitantes humanos verán el nombre y la descripción actualizados del producto en la tienda, junto con todos los demás canales que proceden de su catálogo de Commerce. Esto es intencional: el objetivo es mejorar cómo se entiende su producto en todas partes, no solo por los agentes de IA y también para evitar riesgos de encubrimiento.

**¿Qué sucede en mis otros canales de ventas cuando aplico un enriquecimiento?**

Dado que el enriquecimiento se escribe directamente en el catálogo de Adobe Commerce, se propaga automáticamente a todos los canales que utilizan el catálogo comercial como fuente fiable; incluidas varias tiendas, canalizaciones de publicidad y cualquier fuente de productos LLM directa. Esto garantiza la coherencia de la marca y la información coherente del producto para los LLM que rastrean por Internet para sus productos.

**¿Puedo revertir un enriquecimiento si no estoy satisfecho con el resultado?**

Sí. Los enriquecimientos aplicados se pueden revertir en cualquier momento desde la vista Sugerencias fijas, restaurando el nombre y la descripción originales del producto en su catálogo de Adobe Commerce.
