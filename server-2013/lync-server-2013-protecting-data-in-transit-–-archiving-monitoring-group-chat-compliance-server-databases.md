---
title: 'Lync Server 2013: Protezione dei dati in transito – database di archiviazione, monitoraggio, server di conformità per chat di gruppo'
TOCTitle: Protezione dei dati in transito – database di archiviazione, monitoraggio, server di conformità per chat di gruppo in Lync Server 2013
ms:assetid: ea219705-1015-43a7-890b-e7e67b451e7c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518336(v=OCS.15)
ms:contentKeyID: 60490920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Protezione dei dati in transito – database di archiviazione, monitoraggio, server di conformità per chat di gruppo in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

Il server di archiviazione e Monitoring Server di Microsoft Lync Server 2013 usano entrambi il servizio Accodamento messaggi (noto anche come MSMQ) per raccogliere e trasferire in modo affidabile messaggi di dati dal punto di raccolta ai server repository. Il servizio di conformità raccoglie i dati in combinazione con Group Chat Server, che usa anch'esso Accodamento messaggi.

In Lync Server 2013 non esiste una protezione interna per i dati in transito. Se la protezione di questo traffico è un requisito, tuttavia, il servizio Accodamento messaggi può gestire la crittografia a livello di messaggio nella coda di invio dei messaggi. Questa funzionalità viene implementata tramite certificati gestiti da Servizi di dominio Active Directory. Per altri dettagli, vedere l'Appendice D: Accodamento messaggi ed effetti sulle comunicazioni Internet in Windows Server 2008 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=145238](http://go.microsoft.com/fwlink/p/?linkid=145238) oppure l'appendice I relativa ad Accodamento messaggi e alle comunicazioni Internet in Windows Server 2008 R2 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=211883](http://go.microsoft.com/fwlink/p/?linkid=211883) per Windows Server 2008 R2.

