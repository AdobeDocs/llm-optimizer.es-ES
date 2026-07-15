---
title: Integración de Google Analytics
description: Aprenda a conectar Google Analytics 4 con LLM Optimizer para medir la detección basada en IA, la participación en el sitio y los resultados empresariales en el panel de Tráficos de referencia.
feature: Referral Traffic
autotag-review: '2026-07-15T17:51:53.586Z'
TQID: 'https://experienceleague.adobe.com/SvWn3W6hpVsWNzfWdJFvPs94lwlKX4ufjjcXKM-6xIc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: f5a6cbd1-8a9a-4c79-a6db-ba46537f516e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 1169
ht-degree: 17%

---


# Integración de Google Analytics

La integración de Google Analytics 4 (GA4) conecta LLM Optimizer con los datos de GA4 de su organización para que pueda medir cómo el descubrimiento impulsado por IA en plataformas como ChatGPT, Gemini, Copilot, Claude y Perplexity se traduce en participación real en el sitio web y resultados comerciales. Después de conectar una propiedad de GA4, LLM Optimizer extrae las métricas de tráficos de referencia, participación y conversión que GA4 atribuye a esas fuentes y las muestra en el panel **Tráficos de referencia** en la pestaña **Impacto en la empresa**.

>[!IMPORTANT]
>
>La integración de GA4 se incluye en la oferta de LLM Optimizer de pago. Los clientes que usen la prueba gratuita no podrán conectarse a GA4 hasta que se actualicen a una oferta de pago.

## Antes de empezar {#before-you-begin}

Para completar la conexión, necesita lo siguiente:

* Cuenta de Google con al menos acceso de **Viewer** en la propiedad de GA4 a la que desea conectarse. El acceso de nivel de propiedad se administra en Google Analytics en **Administración > Administración del acceso a propiedades**.
* Permiso para administrar la configuración en LLM Optimizer (de lo contrario, el botón Conectar está visible pero deshabilitado).
* Un explorador que permite elementos emergentes del origen de LLM Optimizer: el paso de inicio de sesión de Google se abre en una nueva pestaña.

No necesita **not** para crear un proyecto de Google Cloud, generar una cuenta de servicio, cargar una clave JSON o ingresar un ID de propiedad. LLM Optimizer intercambia la conexión a través de la pantalla de consentimiento estándar de OAuth de Google.

## Conecte GA4 al tablero de Tráficos de referencia {#connect}

El flujo de conexión empieza desde el panel de control [Tráfico de referencia](/help/dashboards/referral-traffic.md) de la siguiente manera:

1. Abra **Tráfico de referencia** en LLM Optimizer.

1. Abra la ficha **Impacto en la empresa**.

   ![Tablero de Tráfico de referencia, ficha Impacto empresarial](/help/dashboards/assets/ga4-integration-01-business-impact-tab.png)

1. Seleccione **Conectar con Analytics**. LLM Optimizer lo enruta a **Configuración del cliente > Analytics**. En el selector de proveedores de Analytics, seleccione **Conectar Google Analytics 4**.

   ![Configuración del cliente, ficha Analytics con GA4 seleccionado](/help/dashboards/assets/ga4-integration-02-analytics-ga4-picker.png)

1. Seleccione **Conectar cuenta**. Se abre una nueva pestaña del explorador en la pantalla de inicio de sesión de Google.

   ![Inicio de sesión de Google para la conexión GA4](/help/dashboards/assets/ga4-integration-03-google-sign-in.png)

1. Inicie sesión con la cuenta de Google que tiene acceso a la propiedad de GA4 a la que desea conectarse. Apruebe el permiso `See and download your Google Analytics data` (ámbito `analytics.readonly`) cuando Google se lo solicite.

1. Google le devuelve a LLM Optimizer, que enumera las propiedades de GA4 a las que puede acceder su cuenta. Seleccione la propiedad que desea conectar y enviar.

1. Vuelva a la pestaña LLM Optimizer. La pestaña Analytics detecta automáticamente la conexión completada y la tarjeta GA4 muestra el estado **Conectado**.

### Después de conectarse {#after-connect}

Después de conectar GA4 a LLM Optimizer, ocurre lo siguiente:

* LLM Optimizer rellena las **últimas cuatro semanas naturales completas** y la **semana natural actual hasta la fecha**.
* Después de rellenarse, los datos se actualizan **diariamente** con una extracción del **día completo anterior**.

>[!NOTE]
>
>El relleno puede tardar un par de horas en completarse. El tablero Impacto empresarial comienza a rellenarse progresivamente a medida que los datos aterrizan; no se requiere ninguna acción por su parte mientras se ejecuta el relleno.

Si se vuelve a conectar (por ejemplo, para cambiar la cuenta de Google o la propiedad de GA4), solo se vuelve a rellenar la semana natural actual, se conservan las semanas anteriores que ya se han cargado.

## Funcionamiento {#how-it-works}

### Modelo de conexión

La integración utiliza el flujo delegado por el usuario de OAuth 2.0 estándar de Google. LLM Optimizer almacena un token de actualización con ámbito en la propiedad de GA4 seleccionada y ese token permite a LLM Optimizer llamar a la API de datos de GA4 en su nombre (con acceso de solo lectura) hasta que la revoque de su cuenta de Google.

### Cómo se identifica el tráfico de LLM

LLM Optimizer pregunta a GA4 solo por las sesiones que el propio GA4 atribuye a una plataforma LLM. Hoy, son sesiones cuyos `sessionSourceMedium` coinciden con uno de `chatgpt`, `gemini.google.com`, `copilot.microsoft.com`, `claude` o `perplexity`. Adobe mantiene la lista de fuentes de LLM admitidas, que pueden ampliarse con el tiempo.

### Datos ingeridos {#data-ingested}

Cada extracción diaria recupera un informe agregado que contiene lo siguiente:

**Dimensiones**

| Dimensión GA4 | Lo que representa |
| --- | --- |
| `date` | El día en que se produjo la sesión. |
| `landingPage` | Primera página que vio el visitante en el sitio. |
| `countryId` | El país del visitante determinado por la geolocalización de IP de GA4. |
| `deviceCategory` | Móvil / escritorio / tableta. |
| `sessionSourceMedium` | Fuente/medio de LLM atribuido por GA4. |

**Métricas**

| Métrica GA4 | Lo que representa |
| --- | --- |
| `sessions` | Número de sesiones en el bloque. |
| `screenPageViews` | Vistas de página en el bloque. |
| `bounceRate` | Fracción de sesiones que rebotaron. |
| `totalPurchasers` | Compradores distintos (si el comercio electrónico está configurado en GA4). |
| `transactions` | Recuento de transacciones (si está configurado el comercio electrónico). |
| `purchaseRevenue` | Ingresos por compras (USD). |
| `totalRevenue` | Ingresos totales (USD). |

### Cómo LLM Optimizer utiliza estos datos

LLM Optimizer utiliza estos datos para rellenar el rendimiento de nivel de página, los desgloses de origen, las divisiones de país y dispositivo y las tendencias temporales del panel de Impacto empresarial. No se utilizan datos para entrenar modelos ni se comparten fuera del inquilino.

### Qué no se ingiere

Sin identificadores de usuario (ID de cliente de Google, dirección IP, ID de dispositivo), sin filas de nivel de sesión, sin filas de nivel de evento, sin dimensiones o métricas personalizadas más allá de las enumeradas anteriormente y sin definiciones de audiencia o segmento de GA4.

## Preguntas frecuentes {#faq}

P: ¿La integración de GA4 está disponible durante la versión de prueba?

No. Esta integración solo está disponible para los clientes de pago de LLM Optimizer.

P: ¿Debo crear un proyecto o una cuenta de servicio de Google Cloud?

No. La conexión es un inicio de sesión estándar de Google. LLM Optimizer administra el cliente OAuth de Google del lado de Adobe; solo necesita una cuenta de Google con acceso de visor en la propiedad GA4.

P: ¿Qué datos se recopilan o almacenan?

LLM Optimizer funciona con métricas agregadas de la API de datos de GA4 autorizadas por su organización, no con datos sin procesar a nivel de evento.

P: ¿Cómo se ingieren los datos?

Su organización autoriza a LLM Optimizer a consultar la API de datos de GA4 para la propiedad seleccionada. El tráfico de referencia alineado con las fuentes LLM se consume a través de esa API.

P: ¿Con qué frecuencia se actualizan los datos?

Los datos se actualizan **diariamente** (día anterior completo después de que se complete el relleno).

P: ¿Los datos sin procesar a nivel de evento se almacenan en LLM Optimizer?

No. Solo se utilizan métricas **agregadas** para comprender los patrones y tendencias del tráfico.

P: ¿Se almacenan direcciones URL completas, cadenas de consulta o el contenido de página?

Las rutas de la página de aterrizaje se incorporan como parte del informe estándar; las cadenas de consulta y el contenido de la página no se incorporan para esta integración.

P: ¿Se almacenan los identificadores de usuario (ID de cliente de Google, dirección IP, ID de dispositivo)?

No.

P: ¿Durante cuánto tiempo se conservan los datos?

Actualmente, los datos se almacenan indefinidamente.

P: ¿Los datos se cifran en tránsito y en reposo?

Actualmente, los datos están cifrados en tránsito, no en reposo. Esto puede cambiar en futuras actualizaciones.

P: ¿Los datos históricos se rellenan?

Sí. Una vez completada correctamente la configuración, se rellenarán los datos de las cuatro últimas semanas naturales y de la semana natural actual. Consulte también [Después de conectarse](#after-connect).

P: ¿Puedo desconectar o revocar el acceso?

Sí, en cualquier momento. Puede volver a conectarse a una cuenta o propiedad diferente desde la tarjeta GA4 en LLM Optimizer o revocar el acceso de LLM Optimizer por completo desde su cuenta de Google en [https://myaccount.google.com/permissions](https://myaccount.google.com/permissions). La revocación del acceso detiene los nuevos datos extraídos; los datos agregados ingeridos anteriormente permanecen en LLM Optimizer.

P: Mi propiedad de GA4 está conectada, pero Impacto empresarial está vacío. ¿Por qué?

LLM Optimizer solo extrae sesiones que el propio GA4 atribuye a una fuente o medio LLM admitido (hoy: ChatGPT, Gemini, Copilot, Claude, Perplexity). Si la propiedad de GA4 aún no ha registrado sesiones de referencia de cualquiera de estas fuentes en la ventana de tiempo que se muestra, el panel estará vacío aunque la conexión esté en buen estado.
