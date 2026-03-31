---
title: Integración de Adobe Analytics
description: Aprenda a conectar Adobe Analytics con LLM Optimizer para medir la detección basada en IA, la participación en el sitio y los resultados empresariales en el panel de Tráficos de referencia.
feature: Referral Traffic
source-git-commit: e7c9bc1d40267dc92608baa005f85f4be21cfda1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 4%

---


# Integración de Adobe Analytics

La integración de Adobe Analytics conecta LLM Optimizer con los datos de Adobe Analytics de su organización para que pueda medir cómo la detección impulsada por IA se traduce en participación real en el sitio web y resultados comerciales. Una vez completado el proceso de integración, los datos estarán disponibles en el panel **Tráfico de referencia** en la pestaña **Impacto en la empresa**.

Al vincular datos de análisis con perspectivas de visibilidad de IA, LLM Optimizer le ayuda a realizar el seguimiento:

* Participación del usuario en páginas referidas a IA.
* Señales de conversión vinculadas a recorridos de detección de IA.
* Impacto en el rendimiento de las optimizaciones GEO.

Esta integración reduce la brecha entre la medición de visibilidad de IA y los análisis de rendimiento empresarial. Los equipos ahora pueden ver no solo dónde aparece la marca en las respuestas de IA, sino también qué sucede después de que llegan los usuarios.

## Disponibilidad {#availability}

>[!IMPORTANT]
>
>La integración de Adobe Analytics se incluye en la oferta de LLM Optimizer de pago. Los clientes que utilicen la prueba gratuita no podrán conectar Adobe Analytics hasta que se actualicen a una oferta de pago.

## Conectar Adobe Analytics al tablero de Tráfico de referencia {#connect}

El flujo de conexión se inicia desde el panel [Tráfico de referencia](/help/dashboards/referral-traffic.md) de la siguiente manera:

1. Abra el tablero [Tráfico de referencia](/help/dashboards/referral-traffic.md). La vista predeterminada es **Perspectivas de tráfico**.

   ![Tablero de Tráfico de referencia, ficha Perspectivas de tráfico](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Seleccione la ficha **Impacto en la empresa**. Si no hay ningún proveedor de análisis conectado, aparecerá un banner: **Conectar para ver el impacto en la empresa**, con **Conectarse a Analytics**.

   ![Pestaña Impacto empresarial con Connect to Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Seleccione **Conectarse a Analytics**. Se abrirá el panel de [Configuración del cliente](/help/dashboards/customer-configuration.md) en la ficha **Analytics**.

   ![Configuración del cliente, ficha Analytics](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. En **Credenciales**, escriba **ID de cliente** y **Secreto de cliente** y, a continuación, seleccione **Verificar y continuar**. Tenga en cuenta lo siguiente:

   * **Verificar y continuar** solo está disponible cuando se rellenan ambos campos.
   * Después de una verificación correcta, se cargan los grupos de informes.
   * Use **ID de cliente** y **Secreto de cliente** de una [cuenta técnica](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) que tenga acceso al grupo de informes que necesita.

   ![Credenciales de Analytics y Verificar y continuar](/help/dashboards/assets/aa-integration-04-credentials.png)

1. En **Configuración**, elija un **grupo de informes**.

   Cuando se selecciona un grupo de informes, LLM Optimizer carga las opciones de **URL de la página Dimension** disponibles para ese grupo de informes.

   ![Grupo de informes seleccionado y dimensiones cargando](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Elija una **URL de la página Dimension** (lista de dimensiones específica del grupo de informes) y, a continuación, seleccione **Guardar y habilitar**.

   * **La URL de la página Dimension** permanece deshabilitada hasta que se selecciona un grupo de informes y se cargan las dimensiones.
   * **Guardar y habilitar** solo está disponible después de seleccionar una dimensión de dirección URL de página.

   ![Dimensión de URL de página y Guardar y habilitar](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. Después de guardar, la configuración debería mostrar el estado **Conectado**. Puede volver al panel de Tráfico de referencia con **Ir al panel de Tráfico de referencia**. En el **Tráfico de referencia** de la ficha **Impacto en la empresa**, el estado debería aparecer como **Conectado a Adobe Analytics**.

   ![Conectado a Adobe Analytics en la configuración y el impacto empresarial](/help/dashboards/assets/aa-integration-07-connected.png)

### Después de conectar {#after-connect}

* LLM Optimizer rellena **las últimas cuatro semanas** y **el calendario actual hasta la fecha**.
* Después del relleno, los datos se actualizan **diariamente** con una extracción de **día anterior completo**.

>[!NOTE]
>
>El relleno puede tardar unas horas en completarse.

## Funcionamiento {#how-it-works}

### Configuración

Durante la configuración, puede definir qué grupo de informes y qué dimensión de página utiliza LLM Optimizer para la ingesta de Adobe Analytics. La dimensión de página puede ser la asignación estándar `variables/page` o una `eVar` personalizada, según el grupo de informes.

### Cómo se identifica el tráfico LLM

El tráfico originado en LLM se identifica mediante el tipo de referente de Adobe Analytics [Herramientas de inteligencia artificial aplicada a la conversación](https://experienceleague.adobe.com/es/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools).

### Datos introducidos {#data-ingested}

LLM Optimizer incorpora los siguientes datos:

**Dimensiones**

* Dominio de referente
* Tipo de referente
* País
* Tipo de dispositivo
* Dimensión de página seleccionada

**Métricas**

* Vistas de la página
* Visitas
* Visitantes
* Entradas
* Salidas
* Rechazos
* Visitas a una sola página
* Tiempo empleado
* Carritos
* Adiciones al carro
* Eliminaciones del carro
* Vistas del carro
* Cierres de compra
* Pedidos
* Ingresos
* Unidades

### Cómo utiliza LLM Optimizer estos datos

Este conjunto de datos alimenta las perspectivas de LLM Optimizer para:

* Rendimiento del tráfico LLM de nivel de página.
* Rendimiento del referente en todas las fuentes LLM.
* Tendencias regionales y de nivel de dispositivo.
* Resultados comerciales descendentes.

## Preguntas frecuentes {#faq}

P: ¿La integración de Adobe Analytics está disponible durante la versión de prueba?

No. La integración solo está disponible para clientes de LLM Optimizer de pago.

P: ¿Qué datos se recopilan o almacenan?

Consulte el capítulo [Datos ingeridos](#data-ingested) anterior. LLM Optimizer funciona con métricas agregadas de las API de Adobe Analytics autorizadas por su organización, no con los datos sin procesar en el nivel de visita.

P: ¿Cómo se incorporan los datos?

Su organización autoriza a LLM Optimizer a consultar las API de Adobe Analytics. El tráfico de referencia alineado con las fuentes LLM se consume a través de esas API.

P: ¿Con qué frecuencia se actualizan los datos?

Los datos se actualizan **diariamente** (día anterior completo después de que se complete el relleno).

P: ¿Los datos sin procesar en el nivel de visita se almacenan en LLM Optimizer?

No. Solo se usan **métricas agregadas** para comprender patrones y tendencias de tráfico.

P: ¿Se almacenan direcciones URL completas, cadenas de consulta o contenido de página?

Se pueden introducir las direcciones URL completas utilizadas para la dimensión de página seleccionada; las cadenas de consulta y el contenido de página no se incorporan para esta integración.

P: ¿Se almacenan los identificadores de usuario (ECID, dirección IP, ID de cookie)?

No.

P: ¿Durante cuánto tiempo se conservan los datos?

Tenga en cuenta que las políticas de retención pueden evolucionar. Actualmente, los datos se almacenan indefinidamente.

P: ¿Los datos están cifrados en tránsito y en reposo?

Actualmente, los datos se cifran en tránsito y no en reposo. Esto puede cambiar en futuras actualizaciones.

P: ¿Los datos históricos están rellenados?

Sí. Después de una configuración correcta, se rellenan las cuatro últimas semanas del calendario completo y la semana natural actual. Ver también [Después de conectar](#after-connect).
