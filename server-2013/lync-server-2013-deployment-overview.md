---
title: 'Lync Server 2013: Panoramica della distribuzione'
TOCTitle: Panoramica della distribuzione
ms:assetid: da67555e-f410-4c37-9996-d511f37da8d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205305(v=OCS.15)
ms:contentKeyID: 49302160
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica della distribuzione per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-12_

Come differenza principale tra Lync Server 2013  Enterprise Edition e Lync Server 2013  Standard Edition, nei server Standard Edition non sono supportate le funzionalità di disponibilità elevata incluse nei server Enterprise Edition. Per la disponibilità elevata, è necessario distribuire più Front End Server in un pool e quindi eseguire il mirroring del server che esegue SQL Server. Con la versione Enterprise Edition è possibile scegliere di collocare o definire un Mediation Server autonomo. Il Monitoring Server e il server di archiviazione possono utilizzare un server autonomo che esegue SQL Server oppure possono disporre di istanze di SQL Server in esecuzione nel server di database per i Front End Server e i pool.

I server con Lync Server 2013Standard Edition sono destinati a organizzazioni di piccole dimensioni e a postazioni remote, non incluse geograficamente nella distribuzione principale di un'organizzazione. Un server Standard Edition è destinato a un numero di utenti pari a circa 5000 utenti ospitati. Non è possibile creare pool di server Standard Edition come per i Front End Server in Enterprise Edition. Inoltre, il database di SQL Server utilizzato nella versione Standard Edition è un server collocato che esegue SQL Server Express progettato per la gestione di carichi di lavoro di server Standard Edition. Con questo non si intende affermare che tutti i ruoli devono essere contenuti in un server Standard Edition. È possibile disporre di Mediation Server e server perimetrali autonomi. Il database di SQL Server per l' archivio di gestione centrale e per gli scopi di Lync Server 2013 deve trovarsi nel server Standard Edition collocato con il server che esegue SQL Server. Il Monitoring Server e il server di archiviazione utilizzano un server autonomo con il database di SQL Server.

