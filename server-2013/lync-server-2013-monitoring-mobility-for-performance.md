---
title: Monitoraggio dei dispositivi mobili per le prestazioni in Lync Server 2013
TOCTitle: Monitoraggio dei dispositivi mobili per le prestazioni in Lync Server 2013
ms:assetid: 9c831c63-9a7d-48ec-9118-f8a7e80ddd04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690033(v=OCS.15)
ms:contentKeyID: 49301475
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio dei dispositivi mobili per le prestazioni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-14_

Il servizio per dispositivi mobili di Lync Server aumenta il carico sui Front End Server e i pool Front End. I dispositivi mobili che mantengono una connessione al server anche quando l'applicazione mobile è ridotta a icona, ad esempio i dispositivi Android e Nokia, impongono un carico superiore rispetto a quelli che nella stessa situazione interrompono la connessione al server. Man mano che l'utilizzo dei dispositivi mobili aumenta, è necessario monitorarne le prestazioni per determinare se sia necessario un aumento della capacità.

Le prestazioni dei dispositivi mobili sono influenzate da svariati limiti:

  - Memoria disponibile

  - Limite della coda di richieste

  - Connessioni simultanee

  - Lunghezza della coda IIS

Altri limiti dei server che possono incidere sulle prestazioni dei dispositivi mobili sono un massimo di dodici accessi, autenticazioni, rinnovi e terminazioni di sessione eseguiti simultaneamente. Nella maggior parte delle distribuzioni non è necessario modificare questi valori massimi.

## Argomenti della sezione

  - [Monitoraggio dei limiti di capacità della memoria del server](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)

  - [Monitoraggio del servizio per dispositivi mobili e dell'utilizzo di UCWA](lync-server-2013-monitoring-mobility-service-and-ucwa-usage.md)

  - [Configurazione del servizio per dispositivi mobili per ottenere prestazioni elevate](lync-server-2013-configuring-mobility-service-for-high-performance.md)

  - [Monitoraggio dei file di registro di traccia delle richieste IIS](lync-server-2013-monitoring-iis-request-tracing-log-files.md)

  - [Contatori delle prestazioni per dispositivi mobili](lync-server-2013-mobility-performance-counters.md)

