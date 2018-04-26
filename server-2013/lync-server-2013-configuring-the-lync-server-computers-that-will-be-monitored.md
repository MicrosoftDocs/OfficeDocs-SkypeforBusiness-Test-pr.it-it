---
title: Configurazione del computer Lync Server da monitorare
TOCTitle: Configurazione del computer Lync Server da monitorare
ms:assetid: 9f1b2b91-d5af-42ad-a27d-b0815f762ad8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205118(v=OCS.15)
ms:contentKeyID: 49301507
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del computer Lync Server da monitorare

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Poiché Lync Server 2013 non usa il processo di individuazione centrale impiegato in Microsoft Lync Server 2010, ogni computer Lync Server 2013 da monitorare deve essere in grado di autosegnalare la sua esistenza al server di gestione. A tale scopo, è necessario installare i file degli agenti di Operations Manager in ognuno dei computer da monitorare. Dopo aver installato i file degli agenti, è necessario configurare il computer affinché funzioni come proxy di System Center. Tenere presente che queste procedure devono essere eseguite dopo aver installato e configurato Lync Server nei computer.

