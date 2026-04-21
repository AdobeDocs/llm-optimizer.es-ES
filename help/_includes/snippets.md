---
source-git-commit: b13f91d144d4899198891c4dcd841de8cfbb2355
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---
# Fragmentos

## Comprobación del estado del enrutamiento en LLM Optimizer {#verify-routing-status-in-ui}

El estado del enrutamiento de tráfico también se puede comprobar en la interfaz de usuario de LLM Optimizer. Vaya a **Configuración del cliente** y seleccione la pestaña **Configuración de CDN**.

![Implementar optimizaciones en agentes de IA — completado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Permitir la optimización en Edge mediante reglas de cortafuegos (opcional) {#waf-allowlist-setup}

Si su CDN utiliza un WAF o un Bot Manager:

* Lista de permitidos el agente de usuario `*AdobeEdgeOptimize/1.0*` en su WAF o Administrador de bots para que el servicio Optimizar en Edge pueda recuperar el contenido de origen.
* Si el firewall requiere una verificación adicional más allá del agente de usuario, genere un secreto (por ejemplo, `openssl rand -hex 32`) y:
   * Agregue `x-edgeoptimize-fetcher-key` con el secreto en sus reglas de enrutamiento junto con los otros `x-edgeoptimize-*` encabezados.
   * Agregue una regla de WAF o Bot Manager para permitir solicitudes en las que `x-edgeoptimize-fetcher-key` coincida con el mismo secreto.
* Optimizar en Edge reenvía este encabezado tal cual: usted es el propietario del ciclo de vida completo de la clave.

## Volver a la descripción general {#return-to-overview}

Para obtener más información sobre Optimizar en Edge, incluidas las oportunidades disponibles, los flujos de trabajo de optimización automática y las preguntas frecuentes, vuelve a [Optimizar en la descripción general de Edge](/help/dashboards/optimize-at-edge/overview.md).
