---
title: Accesso ai dati di monitoraggio in Lync Server 2013
TOCTitle: Accesso ai dati di monitoraggio in Lync Server 2013
ms:assetid: 845385ca-5532-4fa2-91b9-51c6de6fec91
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688116(v=OCS.15)
ms:contentKeyID: 49887638
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Accesso ai dati di monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

I dati di monitoraggio sono archiviati in una coppia di database di SQL Server: LcsCdr per i dati di registrazione dettagli chiamata, e QoEMetrics per i dati QoE. Questi sono normali database, ed è possibile accedere ai dati in essi contenuti tramite tutti gli strumenti solitamente utilizzati per accedere e analizzare i dati di SQL Server.

Uno strumento da considerare per l'analisi e l'accesso ai dati di monitoraggio è Lync Server Monitoring Reports, un insieme di rapporti standard pubblicati da Microsoft SQL Server Reporting Services. Questi rapporti, cui è possibile accedere utilizzando un browser, contengono informazioni sull'utilizzo, di diagnostica della chiamate e sulla qualità multimediale, tutte basate su record di registrazione dettagli chiamata e QoE (Quality of Experience) archiviati nei database CDR e QoE. Monitoring Reports funziona con Lync Server 2013 e può essere installato attraverso la procedura guidata di Lync Server dopo che Lync Server è stato installato, e il monitoraggio configurato.

Monitoring Reports richiede l'utilizzo di SQL Server Reporting Service. SQL Server Reporting Service può essere installato contemporaneamente a SQL Server o dopo l'installazione di SQL Server.

Per ulteriori informazioni, vedere l'argomento [Installazione dei rapporti di monitoraggio di Lync Server 2013](lync-server-2013-installing-lync-server-2013-monitoring-reports.md) nella guida alla distribuzione di Lync Server 2013.

