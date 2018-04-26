---
title: Configurazione delle piattaforme del sistema per l'archiviazione
TOCTitle: Configurazione delle piattaforme del sistema per l'archiviazione
ms:assetid: 2df40fdf-0e32-46d4-9fb2-1ce1d7bfa328
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204768(v=OCS.15)
ms:contentKeyID: 49300044
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle piattaforme del sistema per l'archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Prima di iniziare la distribuzione di Archiviazione, è necessario installare il sistema operativo richiesto e gli altri componenti software prerequisiti in un'infrastruttura hardware che soddisfi i requisiti si sistema:

  - Piattaforma di **Lync Server 2013**   Le distribuzioni di Lync Server 2013 non dispongono di server di archiviazione. Vengono invece eseguiti agenti di raccolta dati unificati sui Front End Server e sui server Standard Edition per acquisire dati per l'archiviazione e pertanto non è richiesta una piattaforma di sistema separata per ospitare Archiviazione.

  - **Piattaforma di archiviazione dati**   In Lync Server 2013 è possibile archiviare i dati usando una delle opzioni seguenti:
    
      - Integrazione di **Microsoft Exchange**   Se si desidera archiviare i dati di Archiviazione di Lync Server 2013 usando la distribuzione di Exchange 2013, anziché o in aggiunta all'impostazione di un database separato per l'archiviazione dei dati di Archiviazione, è necessario che la distribuzione di Exchange esegua Exchange 2013. Per informazioni dettagliate sull'impostazione delle piattaforme di sistema per Exchange 2013, vedere la documentazione relativa al prodotto Exchange.
    
      - **SQL Server**   Se si desidera usare un database SQL Server separato per archiviare i dati di archiviazione, anziché o in aggiunta all'uso dell'integrazione di Microsoft Exchange, è necessario impostare la piattaforma di sistema per il database prima della distribuzione di Archiviazione. I requisiti specifici della piattaforma di sistema variano a seconda che venga usato Microsoft SQL Server 2008 R2 o Microsoft SQL Server 2012 come database di archiviazione. Per informazioni dettagliate sull'impostazione delle piattaforme di sistema per questi database, vedere la documentazione relativa ai prodotti Microsoft SQL Server 2008 R2 e Microsoft SQL Server 2012.

  - **Piattaforma del file server**   Lync Server 2013 archivia i file di archiviazione di Lync Server nella stessa posizione specificata per l'archiviazione dei file durante l'installazione dei Front End Server o dei server Standard Edition. Non è possibile specificare una posizione separata per l'archiviazione dei file di archiviazione e pertanto non è richiesta una piattaforma di sistema separata per tale archiviazione. Se si usa l'integrazione di Microsoft Exchange, i file di Exchange 2013 per le comunicazioni di Lync archiviate vengono archiviati sui server Exchange 2013 per gli utenti disponibili su tali server Exchange.

