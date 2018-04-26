---
title: "Lync Server 2013: Panoramica dell'archiviazione"
TOCTitle: Panoramica dell'archiviazione
ms:assetid: 1e3c2ef1-f561-4f57-8b6a-7d78addc1ed1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204729(v=OCS.15)
ms:contentKeyID: 49299875
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dell'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-09-30_

In Lync Server 2013 l'archiviazione è un modo di archiviare le comunicazioni inviate attraverso Lync Server 2013.

È possibile implementare l'archiviazione all'interno della distribuzione di Lync Server 2013 iniziale oppure aggiungerla a una distribuzione esistente. Per utilizzare i database di archiviazione di Lync Server 2013 (database di SQL Server) per l'archiviazione dei dati, utilizzare il Generatore di topologie per aggiungere i database alla topologia, quindi pubblicare nuovamente la topologia. Se tutti gli utenti risiedono in Exchange 2013 e le relative cassette postali sono impostate su Archiviazione sul posto, non è necessario aggiornare la topologia, ma soltanto abilitare l'integrazione di Microsoft Exchange per archiviare i dati in Exchange 2013.

Quando si implementa l'archiviazione, configurarla in modo da specificare ciò che viene archiviato. Per impostazione predefinita, non viene archiviato nulla. Configurare e gestire l'archiviazione utilizzando il Pannello di controllo di Lync Server 2013. È possibile implementare l'archiviazione per le comunicazioni interne, le comunicazioni esterne o entrambe. È possibile configurare le impostazioni di archiviazione per l'organizzazione e, facoltativamente, per siti, pool, utenti e gruppi di utenti specifici. Per informazioni dettagliate sulla determinazione delle opzioni appropriate per l'organizzazione, vedere [Definizione dei requisiti dell'organizzazione per l'archiviazione in Lync Server 2013](lync-server-2013-defining-your-requirements-for-archiving.md) nella documentazione relativa alla pianificazione. Per informazioni dettagliate sull'implementazione delle configurazioni e dei criteri di archiviazione e sulle informazioni che possono o non possono essere archiviate, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.

