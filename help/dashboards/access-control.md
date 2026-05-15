---
title: Control de acceso
description: Descubra cómo difieren los usuarios asignados al producto y los usuarios de la organización en Adobe LLM Optimizer, lo que ven los usuarios de solo lectura en la interfaz de usuario y cómo los administradores asignan el acceso en Adobe Admin Console.
feature: Customer Configuration
autotag-review: '2026-05-15T17:26:43.837Z'
TQID: 'https://experienceleague.adobe.com/hJpQQpuHBRMdKT5oKA9z0Y8H3d3p6To-n2hWKrXgZsQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: b704f6a0-b2fb-4df0-9177-9753751004f5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 618
ht-degree: 4%

---


# Control de acceso

Adobe LLM Optimizer admite el control de acceso básico, basado en perfiles de usuario. Esta capacidad está disponible solamente para **clientes de pago** y se habilita a solicitud. No está disponible para clientes de prueba.

>[!IMPORTANT]
>
>Para solicitar acceso a esta función, los clientes de pago deben ponerse en contacto con el administrador de cuentas de Adobe.

## Usuarios asignados a productos {#product-assigned-users}

Si está asignado al producto, tiene las mismas capacidades que un usuario organizativo estándar, además de los siguientes permisos:

* Acceso de escritura en [Configuración del cliente](/help/dashboards/customer-configuration.md) para preguntas, categorías, temas y configuración relacionada.
* Implementar [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) optimizaciones y administrar sugerencias.
* Administrar las configuraciones de la consola de búsqueda de Google.
* Administre las configuraciones de Optimizar en Edge y CDN.
* Incorporar un nuevo sitio.

## Usuarios de la organización {#organizational-users}

Los usuarios de la organización son usuarios estándar **no** asignados al producto. Si es un usuario de la organización, tiene acceso de **solo lectura** a los [paneles de LLM Optimizer](/help/dashboards/dashboards-overview.md) y a las vistas relacionadas. Se aplican las siguientes restricciones.

### Configuración del cliente {#customer-configuration-restrictions}

* **Indicadores de carga** deshabilitados.
* La administración y edición de peticiones de datos, categorías, temas y regiones está desactivada.

  ![Restricciones de configuración del cliente para usuarios de solo lectura](/help/dashboards/assets/access-control-customer-configuration.png)

### Configuración de CDN (Configuración de cliente) {#cdn-configuration-restrictions}

* **La red CDN** integrada está deshabilitada (los usuarios de solo lectura no pueden agregar un proveedor CDN).
* **Eliminar CDN** está deshabilitado (los usuarios de solo lectura no pueden quitar una configuración de CDN existente).
* El botón **Enviar** del cuadro de diálogo integrado de CDN está deshabilitado (los usuarios de solo lectura no pueden completar la configuración de CDN).

  ![Restricciones de configuración de CDN para usuarios de solo lectura](/help/dashboards/assets/access-control-cdn-configuration.png)

### Presencia de marca: perspectivas de datos {#brand-presence-restrictions}

* Los botones **Eliminar** junto a los temas están ocultos (los usuarios de solo lectura no pueden quitar temas del seguimiento).
* Los botones **Eliminar** junto a los mensajes están ocultos (los usuarios de solo lectura no pueden eliminar los mensajes del seguimiento).

  ![Acciones de Presencia de marca ocultas para usuarios de solo lectura](/help/dashboards/assets/access-control-brand-presence.png)

### Oportunidades de tráfico agéntico (oportunidades de página de error) {#agentic-opportunities}

Para oportunidades como páginas de error 404, 403 y 503:

* **Optimización de implementación** está oculta.
* Una alerta informativa explica que se requiere el acceso de implementación.

  ![Optimización de implementación oculta en oportunidades de tráfico de agente](/help/dashboards/assets/access-control-agentic-deploy.png)

### Otras páginas de oportunidad {#other-opportunities}

El comportamiento de solo lectura también se aplica a tipos de oportunidades como:

* Tabla de contenido
* Resumen
* Legibilidad
* Procesamiento previo
* Encabezados
* Preguntas frecuentes
* Faltan datos estructurados
* Oportunidad de parche genérico

Para estas páginas:

* **Optimización de implementación** está oculta cuando el usuario no tiene acceso de implementación.
* Una alerta en línea explica que se requiere acceso de implementación. El mensaje es similar al siguiente: *Se requiere acceso de implementación. No tiene permiso para implementar optimizaciones o administrar sugerencias. Póngase en contacto con el administrador para solicitar acceso.*
* La barra inferior fija con acciones de implementación está oculta.

  ![Alerta en línea cuando se requiere acceso de implementación](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Optimizar en Edge implementa acciones ocultas para usuarios de solo lectura](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Configuración de petición de datos de Google Search Console {#gsc-restrictions}

* Las acciones Administrar y conectar están deshabilitadas u ocultas.
* La columna de acciones utilizada para agregar indicadores está oculta.

  ![Restricciones de configuración de la consola de Google Search](/help/dashboards/assets/access-control-gsc.png)

### Incorporación de un nuevo sitio {#onboarding-restrictions}

* La incorporación de un nuevo sitio está deshabilitada para los usuarios sin control de acceso.

  ![Nuevo sitio incorporado deshabilitado](/help/dashboards/assets/access-control-onboarding.png)

## Asignar el producto a un usuario o grupo {#assign-product}

Un **administrador del sistema** de su organización puede usar [Adobe Admin Console](https://adminconsole.adobe.com/) para asignar Adobe LLM Optimizer a un usuario o grupo.

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/) con una cuenta que tenga derechos administrativos para su organización.
1. Asigne el perfil de producto de Adobe LLM Optimizer (o el derecho de producto equivalente de su organización) al usuario o grupo que debe recibir las funciones asignadas al producto.

Para ver los pasos detallados, consulte [Administrar productos en Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-products.html) y [Administrar grupos de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html).

>[!NOTE]
>
>Los flujos de pantalla de Adobe Admin Console pueden cambiar entre versiones. Si las opciones anteriores no coinciden con su consola, utilice los vínculos de ayuda del producto en Adobe Admin Console o póngase en contacto con el equipo de la cuenta de Adobe.
