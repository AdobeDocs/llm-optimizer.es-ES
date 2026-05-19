---
title: Control de acceso
description: Descubra en que se diferencian los usuarios asignados al producto de los usuarios de la organización en Adobe LLM Optimizer, lo que ven los usuarios de solo lectura en la interfaz de usuario y cómo los administradores asignan el acceso en Adobe Admin Console.
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
ht-degree: 100%

---


# Control de acceso

Adobe LLM Optimizer admite el control de acceso básico, basado en perfiles de usuario. Esta función solo está disponible para los **clientes de pago** y se habilita previa solicitud. No está disponible para los clientes de la versión de prueba.

>[!IMPORTANT]
>
>Para solicitar acceso a esta función, los clientes de pago deben ponerse en contacto con el administrador de cuentas de Adobe.

## Usuarios asignados a un producto {#product-assigned-users}

Si se le ha asignado el producto, cuenta con las mismas posibilidades que un usuario estándar de la organización, además de los siguientes permisos:

* Acceso de escritura en [Configuración del cliente](/help/dashboards/customer-configuration.md) para indicaciones, categorías, temas y configuración relacionada.
* Implemente las optimizaciones de [Optimizar en Edge](/help/dashboards/optimize-at-edge/overview.md) y administre las sugerencias.
* Administre las configuraciones de Google Search Console.
* Administre las configuraciones de Optimizar en Edge y CDN.
* Incorpore un nuevo sitio.

## Usuarios de la organización {#organizational-users}

Los usuarios de la organización son usuarios estándar que **no** se asignan al producto. Si es un usuario de la organización, cuenta con acceso de **solo lectura** a los [paneles de control de LLM Optimizer](/help/dashboards/dashboards-overview.md) y a las vistas relacionadas. Se aplican las siguientes restricciones.

### Configuración del cliente {#customer-configuration-restrictions}

* La opción **Cargar indicaciones** está desactivada.
* La administración y edición de indicaciones, categorías, temas y regiones está deshabilitada.

  ![Restricciones de configuración del cliente para usuarios de solo lectura](/help/dashboards/assets/access-control-customer-configuration.png)

### Configuración de la CDN (configuración del cliente) {#cdn-configuration-restrictions}

* La opción **Incorporar CDN** está desactivada (los usuarios de solo lectura no pueden añadir un proveedor de CDN).
* La opción **Eliminar CDN** está desactivada (los usuarios de solo lectura no pueden quitar una configuración de CDN existente).
* El botón **Enviar** del cuadro de diálogo incorporación de la CDN está desactivado (los usuarios de solo lectura no pueden completar la configuración de CDN).

  ![Restricciones de configuración de CDN para usuarios de solo lectura](/help/dashboards/assets/access-control-cdn-configuration.png)

### Presencia de marca: información de datos {#brand-presence-restrictions}

* Los botones **Eliminar** situados junto a los temas están ocultos (los usuarios de solo lectura no pueden quitar temas del seguimiento).
* Los botones **Eliminar** situados junto a las indicaciones están ocultos (los usuarios de solo lectura no pueden eliminar las indicaciones del seguimiento).

  ![Acciones de Presencia de marca ocultas para usuarios de solo lectura](/help/dashboards/assets/access-control-brand-presence.png)

### Oportunidades de Tráfico agéntico (oportunidades de la página de error) {#agentic-opportunities}

Para oportunidades como las páginas de error 404, 403 y 503:

* La opción **Implementar optimización** está oculta.
* Una alerta informativa explica que se requiere el acceso de implementación.

  ![Implementar optimización está oculto en las oportunidades del Tráfico agéntico](/help/dashboards/assets/access-control-agentic-deploy.png)

### Otras páginas de oportunidades {#other-opportunities}

El comportamiento de solo lectura también se aplica a tipos de oportunidades como:

* Tabla de contenido
* Resumen
* Legibilidad
* Procesamiento previo
* Encabezados
* Preguntas frecuentes
* Datos estructurados que faltan
* Oportunidad de parche genérico

Para estas páginas:

* **Implementar optimización** está oculto cuando el usuario no tiene acceso de implementación.
* Una alerta en línea explica que se requiere acceso de implementación. El mensaje es parecido al siguiente: *Se requiere acceso de implementación. No tiene permiso para implementar optimizaciones o administrar sugerencias. Póngase en contacto con su administrador para solicitar acceso*.
* La barra inferior fija con acciones de implementación está oculta.

  ![Alerta en línea cuando se requiere acceso de implementación](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Acciones de implementación de Optimizar en Edge ocultas para los usuarios de solo lectura](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Configuración de la indicación de Google Search Console {#gsc-restrictions}

* Las acciones Administrar y conectar están deshabilitadas u ocultas.
* La columna de acciones que se utiliza para añadir indicaciones está oculta.

  ![Restricciones de configuración de Google Search Console](/help/dashboards/assets/access-control-gsc.png)

### Incorporar un nuevo sitio {#onboarding-restrictions}

* La incorporación de un nuevo sitio está deshabilitada para los usuarios sin control de acceso.

  ![Incorporar un nuevo sitio deshabilitado](/help/dashboards/assets/access-control-onboarding.png)

## Asignar el producto a un usuario o grupo {#assign-product}

Un **administrador del sistema** de su organización puede utilizar [Adobe Admin Console](https://adminconsole.adobe.com/) para asignar Adobe LLM Optimizer a un usuario o grupo.

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/) con una cuenta que tenga derechos administrativos para su organización.
1. Asigne el perfil de producto de Adobe LLM Optimizer (o la licencia de producto equivalente de su organización) al usuario o grupo que debe recibir las funcionalidades asignadas al producto.

Para conocer los pasos detallados, consulte [Administración de productos en Admin Console](https://helpx.adobe.com/es/enterprise/using/manage-products.html?lang=es) y [Administrar grupos de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html).

>[!NOTE]
>
>Los flujos de pantalla en Adobe Admin Console pueden cambiar entre versiones. Si las opciones anteriores no coinciden con su consola, utilice los vínculos de ayuda integrados en el producto de Adobe Admin Console o póngase en contacto con el equipo de cuentas de Adobe.
