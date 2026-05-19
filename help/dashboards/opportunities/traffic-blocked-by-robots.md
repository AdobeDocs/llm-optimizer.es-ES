---
title: Tráfico bloqueado por robots.txt
description: Descubra cómo LLM Optimizer detecta cuándo el archivo robots.txt bloquea el acceso de los agentes de IA al contenido y cómo solucionarlo.
feature: Opportunities
autotag-review: '2026-05-15T18:00:25.453Z'
TQID: 'https://experienceleague.adobe.com/9LGbxeIbWYZp-MN5Zww6g-dQ6BZT0IWzlA7XB-2Xlho'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 817
ht-degree: 100%

---


# Tráfico bloqueado por robots.txt

El archivo `robots.txt` controla qué rastreadores pueden acceder al sitio. Cuando a los agentes de IA se les bloquea de forma selectiva el acceso al contenido que, por lo demás, es accesible para los rastreadores generales, esos agentes no pueden indexar ni citar ese contenido, lo que reduce directamente la visibilidad de su marca en las respuestas generadas por IA.

La oportunidad de Tráfico bloqueado por robots.txt analiza el archivo `robots.txt` en relación con las páginas principales e identifica las reglas que impiden que los agentes de IA accedan al contenido al que deberían poder acceder. Muestra los resultados a nivel de cada línea del archivo `robots.txt` para que pueda revisar y actualizar directivas específicas en lugar de realizar una auditoría de todo el archivo manualmente.

Permite ver de un vistazo dos métricas clave:

- **Total de URL**: número de direcciones URL afectadas por las reglas de bloqueo en su archivo `robots.txt`.
- **Agentes bloqueados**: número de agentes de IA a los que se les impide acceder a esas direcciones URL.

![Panel de control Tráfico bloqueado por robots.txt](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-overview.png)

## Funcionamiento

LLM Optimizer recupera el archivo `robots.txt` y comprueba las páginas principales con seis de los principales agentes de usuario del agente de IA:

- ClaudeBot
- GPTBot
- OAI-SearchBot
- OAI-User
- PerplexityBot
- Perplexity-User

Una dirección URL solo se marca cuando **está permitida para el agente de usuario comodín (`*`), pero no para un agente de IA específico**. No se informa del bloqueo generalizado, en el que todos los rastreadores se ven restringidos por igual. La auditoría se centra específicamente en la exclusión selectiva de agentes de IA, lo que constituye el resultado más procesable para GEO.

>[!NOTE]
>Esta oportunidad no utiliza la IA para desarrollar o enviar sugerencias. Los resultados se basan por completo en el análisis directo del archivo `robots.txt`.

Los resultados se muestran en dos pestañas: **robots.txt** y **Detalles de tráfico bloqueado por agente**.

## robots.txt

Esta pestaña muestra el archivo `robots.txt` completo con las directivas de bloqueo resaltadas en rojo. Cada línea resaltada representa una regla que bloquea de forma selectiva el acceso de uno o más agentes de IA a una URL, que, por lo demás es de acceso público.

![Vista de robots.txt con las directivas de bloqueo resaltadas](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-robotstxt.png)

Al hacer clic en una directiva resaltada, se muestra más información sobre su impacto y la solución sugerida.

## Detalles de tráfico bloqueado por agente

En esta pestaña se ofrece un desglose del tráfico bloqueado organizado por el agente de IA. Para cada agente bloqueado, muestra lo siguiente:

- **Descripción del problema**: una explicación de qué agente se está bloqueando y por qué es importante.
- **Resolución**: directrices para abrir el archivo `robots.txt` y revisar el número de línea específico que aparece junto a cada dirección URL afectada.
- Una tabla de direcciones URL afectadas con **Línea**, **Clasificación** y **URL** para cada página bloqueada.

Cada agente (por ejemplo, OAI-User, GPTBot, OAI-SearchBot) tiene su propia subpestaña para poder abordar los bloqueos por agente.

## Cómo solucionarlo

Para resolver un problema de agente bloqueado, abra el archivo `robots.txt` y busque el número de línea que aparece junto a cada dirección URL afectada en la pestaña Detalles de tráfico bloqueado por agente. Actualice o elimine la directiva No permitir para el agente de IA correspondiente para permitir el acceso a la URL afectada.

Por ejemplo, para desbloquear GPTBot de una página específica, quite o actualice la directiva:

```
User-agent: GPTBot
Disallow: /blog/cold-brewing-101
```

Cuando el archivo `robots.txt` se haya actualizado y vuelto a publicar, LLM Optimizer detectará el cambio en la siguiente ejecución de auditoría y marcará la sugerencia como resuelta.

## Probar en la demostración

Vea la oportunidad de Tráfico bloqueado por robots.txt en acción utilizando el entorno de demostración de Frescopa.

[Ver Tráfico bloqueado por robots.txt en la demostración de Frescopa](https://play.llmo.now/org/demo-org/opportunities/blocked-urls-llm-agents)

## Preguntas frecuentes

**¿Por qué el bloqueo de agentes de IA es importante para GEO?**

La optimización del motor generativo requiere que los rastreadores de IA puedan acceder al contenido del sitio e indexarlo. Bloquear agentes de IA evita directamente que sus páginas aparezcan en respuestas generadas por IA, lo que reduce las citas, las menciones de la marca y la visibilidad general de la IA. Incluso una sola página de alto tráfico bloqueada puede representar una pérdida significativa de exposición de marca impulsada por IA.

**¿Cuál es la diferencia entre el bloqueo general y el bloqueo selectivo?**

El bloqueo general significa que todos los rastreadores, incluidos los rastreadores web generales, están restringidos desde una página. El bloqueo selectivo significa que los rastreadores generales pueden acceder a la página, pero los agentes de IA específicos no. Esta oportunidad solo indica el bloqueo selectivo porque representa una exclusión intencionada o accidental de los agentes de IA del contenido que, de lo contrario, es público, y es el hallazgo más procesable.

**¿Qué agentes de IA comprueba LLM Optimizer?**

LLM Optimizer comprueba ClaudeBot, GPTBot, OAI-SearchBot, OAI-User, PerplexityBot y Perplexity-User.

**¿Qué sucede si quiero bloquear intencionalmente a ciertos agentes de IA?**

Puede revisar cada directiva marcada y elegir mantener el bloque intencionadamente. Las sugerencias omitidas se conservan en las ejecuciones de auditoría y no se volverán a mostrar a menos que el archivo `robots.txt` cambie y vuelva a aparecer la regla.

**¿Cómo realiza LLM Optimizer el seguimiento de los cambios en mi archivo robots.txt a lo largo del tiempo?**

LLM Optimizer usa el hash para hacer un seguimiento del contenido de `robots.txt` entre ejecuciones. Si vuelve a aparecer una regla de bloqueo resuelta anteriormente (por ejemplo, después de una actualización de `robots.txt`), se volverá a mostrar como una nueva sugerencia.

**¿Cómo se determinan las páginas principales?**

Las páginas provienen de una combinación de sus páginas de SEO de mayor tráfico, las principales URL visitadas por el agente de IA de los registros de CDN y cualquier URL personalizada especificada en la configuración del sitio.
