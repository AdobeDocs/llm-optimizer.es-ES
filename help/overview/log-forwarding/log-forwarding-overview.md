---
title: Información general de reenvío de registros BYOCDN
description: Aprenda a reenviar los registros de CDN de su proveedor al bloque S3 de Adobe para la recopilación de datos de tráfico auténtico en LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:53:26.846Z'
TQID: 'https://experienceleague.adobe.com/EPQ6GBjNXpIwYTuzj1xDKkIzuFLOWFPmu0lqSGUAX3I'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 2%

---


# Información general de reenvío de registros BYOCDN {#cdn-log-forwarding}

El reenvío de registros para una CDN administrada por el cliente (BYOCDN) es el proceso de enviar sus registros de acceso de CDN al bloque de Amazon S3 de Adobe para que LLM Optimizer pueda recopilar y analizar datos de tráfico reales. Sin el reenvío de registros de CDN, el panel [Tráfico agéntico](/help/dashboards/agentic-traffic.md) no puede mostrar métricas.

Las guías que se proporcionan a continuación siguen el mismo flujo de trabajo en dos fases:

1. **Incorporado en LLM Optimizer**: registre su CDN en la página [Configuración de CDN](/help/dashboards/customer-configuration.md) para generar las credenciales de S3 y los detalles de ruta necesarios.
2. **Configurar su CDN**: use esos detalles para crear un trabajo de reenvío de registros (o cargar registros manualmente) en la consola de su proveedor de CDN. Para CloudFront, puede utilizar la consola o completar la configuración de la entrega solo con la **CLI de AWS**; consulte [CloudFront (CLI de AWS)](/help/overview/log-forwarding/cloudfront-cli.md).

## Proveedores de CDN {#cdn-providers}

Siga la guía correspondiente para su proveedor de CDN.

| Proveedor de CDN | Guía |
|---|---|
| Akamai | [Ver guía](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [Ver guía](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront (consola) | [Ver guía](/help/overview/log-forwarding/cloudfront.md) |
| CloudFront (CLI de AWS) | [Ver guía](/help/overview/log-forwarding/cloudfront-cli.md) |
| Fastly | [Ver guía](/help/overview/log-forwarding/fastly.md) |
| Imperva | [Ver guía](/help/overview/log-forwarding/imperva.md) |
| Otro (manual/CDN no compatible) | [Ver guía](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>Si su proveedor de CDN no aparece en la lista anterior, utilice la guía **Other (manual / unsupported CDN)**, que trata las cargas manuales, los scripts ad hoc y cualquier CDN que no sea compatible de forma nativa.
