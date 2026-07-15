---
title: Integración de Adobe Analytics
description: Aprenda a conectar Adobe Analytics con LLM Optimizer para medir el descubrimiento basado en la IA, la participación en el sitio y los resultados comerciales en el panel de control de Tráfico de referencia.
feature: Referral Traffic
autotag-review: '2026-07-15T16:46:49.693Z'
TQID: 'https://experienceleague.adobe.com/H0p8HV2bf1KuKYqF1ByAF2BpGlb4YScsWDQU5mMkTRY'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: e69d5a42-0217-4ca5-9396-a9a826a170da
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 950
ht-degree: 92%

---


# Integración de Adobe Analytics

La integración de Adobe Analytics conecta LLM Optimizer con los datos de Adobe Analytics de su organización para que pueda medir cómo el descubrimiento basado en la IA se traduce en una participación real en el sitio web y en resultados comerciales. Una vez finalizado el proceso de integración, los datos estarán disponibles en el panel de control **Tráfico de referencia** en la pestaña **Impacto en la empresa**.

Al vincular los datos analíticos con la información de visibilidad de la IA, LLM Optimizer le ayuda a realizar un seguimiento de lo siguiente:

* Participación del usuario en páginas referenciadas por IA.
* Señales de conversión vinculadas a los procesos de descubrimiento de la IA.
* Impacto en el rendimiento de las optimizaciones GEO.

Esta integración tiende un puente entre la medición de la visibilidad de la IA y el análisis del rendimiento empresarial. Ahora, los equipos pueden ver no solo dónde aparece la marca en las respuestas de la IA, sino también qué ocurre después de que los usuarios lleguen.

## Disponibilidad {#availability}

>[!IMPORTANT]
>
>La integración de Adobe Analytics está incluida en la oferta de pago de LLM Optimizer. Los clientes que utilicen la versión de prueba gratuita no podrán conectar Adobe Analytics hasta que actualicen a una oferta de pago.

## Conectar Adobe Analytics con el panel de control de tráfico de referencia {#connect}

El flujo de conexión empieza desde el panel de control [Tráfico de referencia](/help/dashboards/referral-traffic.md) de la siguiente manera:

1. Abra el panel de control [Tráfico de referencia](/help/dashboards/referral-traffic.md). La vista predeterminada es **Datos del tráfico**.

   ![Panel de control Tráfico de referencia, pestaña Perspectivas del tráfico](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Seleccione la pestaña **Impacto en la empresa**. Si no hay ningún proveedor de análisis conectado, aparecerá un banner: **Conectar para ver el impacto en la empresa**, con **Conectar con Analytics**.

   ![Pestaña Impacto en la empresa con Conectar con Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Seleccione **Conectar con Analytics**. Se abrirá el panel [Configuración del cliente](/help/dashboards/customer-configuration.md) en la pestaña **Análisis**.

   ![Configuración del cliente, pestaña Análisis](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. En **Credenciales**, introduzca el **ID de cliente** y el **Secreto de cliente**, y a continuación seleccione **Verificar y continuar**. Tenga en cuenta lo siguiente:

   * **Verificar y continuar** solo está disponible cuando ambos campos se han completado.
   * Tras una verificación satisfactoria, se cargarán los grupos de informes.
   * Utilice el **ID de cliente** y el **Secreto de cliente** de una [cuenta técnica](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) que tenga acceso al grupo de informes que necesita.

   ![Credenciales de análisis y Verificar y continuar](/help/dashboards/assets/aa-integration-04-credentials.png)

1. En **Configuración**, elija un **Grupo de informes**.

   Cuando se selecciona un conjunto de informes, LLM Optimizer carga las opciones **Dimensión de URL de página** disponibles para ese grupo.

   ![Se ha seleccionado el grupo de informes y se están cargando las dimensiones](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Elija una **dimensión de URL de página** (lista de dimensiones específicas del grupo) y, a continuación, seleccione **Guardar y habilitar**.

   * **Dimensión de URL de página** permanece deshabilitada hasta que se seleccione un grupo de informes y se carguen las dimensiones.
   * **Guardar y habilitar** solo está disponible después de seleccionar una dimensión de URL de página.

   ![Dimensión de URL de la página y Guardar y habilitar](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. Después de guardarla, la configuración debería mostrar el estado **Conectado**. Puede volver al panel de control de tráfico de referencia con **Ir al panel de control de tráfico de referencia**. En **Tráfico de referencia** en la pestaña **Impacto en la empresa**, el estado debería aparecer como **Conectado a Adobe Analytics**.

   ![Conectado a Adobe Analytics en la configuración e Impacto en la empresa](/help/dashboards/assets/aa-integration-07-connected.png)

### Después de conectarse {#after-connect}

* LLM Optimizer rellena las **últimas cuatro semanas naturales completas** y la **semana natural actual hasta la fecha**.
* Después de rellenarse, los datos se actualizan **diariamente** con una extracción del **día completo anterior**.

>[!NOTE]
>
>El relleno puede tardar un par de horas en completarse.

## Consulte Impacto empresarial en acción

La visibilidad de la IA es solo parte de la historia. Para comprender si sus esfuerzos de optimización están impulsando los resultados empresariales, debe saber qué sucede después de que los visitantes llegan al sitio.

Este vídeo presenta la vista **Impacto en la empresa**, que combina LLM Optimizer con Adobe Analytics para mostrar cómo el tráfico referido a IA se traduce en participación, conversiones e ingresos, lo que le ayuda a medir el verdadero valor de su presencia de IA.

>[!VIDEO](https://video.tv.adobe.com/v/3492503/?learn=on){transcript=true}

## Funcionamiento {#how-it-works}

### Configuración

Durante la configuración, debe definir qué conjunto de informes y dimensión de página utiliza LLM Optimizer para la ingesta de datos de Adobe Analytics. La dimensión de la página puede ser la asignación `variables/page` estándar o una `eVar` personalizada, dependiendo de su grupo de informes.

### Cómo se identifica el tráfico de LLM

El tráfico originado en LLM se identifica mediante el uso del [Tipo de referente: herramientas de IA conversacional](https://experienceleague.adobe.com/es/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools) de Adobe Analytics.

### Datos ingeridos {#data-ingested}

LLM Optimizer ingiere los siguientes datos:

**Dimensiones**

* Dominio del referente
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
* Tiempo dedicado
* Carros de compras
* Incorporaciones al carro de compras
* Eliminaciones del carro de compras
* Visualizaciones del carro de compras
* Cierres de compra
* Pedidos
* Ingresos
* Unidades

### Cómo LLM Optimizer utiliza estos datos

Este conjunto de datos proporciona información valiosa sobre LLM Optimizer para lo siguiente:

* Rendimiento del tráfico LLM a nivel de página.
* Rendimiento del referente en las distintas fuentes de LLM.
* Tendencias regionales y a nivel de dispositivo.
* Resultados comerciales posteriores.

## Preguntas frecuentes {#faq}

P: ¿Está disponible la integración de Adobe Analytics durante la versión de prueba?

No. Esta integración solo está disponible para los clientes de pago de LLM Optimizer.

P: ¿Qué datos se recopilan o almacenan?

Consulte el capítulo [Datos ingeridos](#data-ingested) anterior. LLM Optimizer funciona con métricas agregadas de las API de Adobe Analytics autorizadas por su organización, no con los datos sin procesar a nivel de visita.

P: ¿Cómo se ingieren los datos?

Su organización autoriza a LLM Optimizer a consultar las API de Adobe Analytics. El tráfico de referencia alineado con las fuentes de LLM se consume a través de esas API.

P: ¿Con qué frecuencia se actualizan los datos?

Los datos se actualizan **diariamente** (día anterior completo después de que se complete el relleno).

P: ¿Se almacenan los datos sin procesar a nivel de visita en LLM Optimizer?

No. Solo se utilizan métricas **agregadas** para comprender los patrones y tendencias del tráfico.

P: ¿Se almacenan direcciones URL completas, cadenas de consulta o el contenido de página?

Se pueden introducir las direcciones URL completas que se utilizan para la dimensión de página seleccionada; las cadenas de consulta y el contenido de página no se introducen para esta integración.

P: ¿Se almacenan los identificadores de usuario (ECID, dirección IP, ID de cookie)?

No.

P: ¿Durante cuánto tiempo se conservan los datos?

Tenga en cuenta que las políticas de retención pueden evolucionar. Actualmente, los datos se almacenan indefinidamente.

P: ¿Los datos se cifran en tránsito y en reposo?

Actualmente, los datos se cifran en tránsito y no en reposo. Esto puede cambiar en futuras actualizaciones.

P: ¿Los datos históricos se rellenan?

Sí. Una vez completada correctamente la configuración, se rellenarán los datos de las cuatro últimas semanas naturales y de la semana natural actual. Consulte también [Después de conectarse](#after-connect).
