---
title: "Lync Server 2013: Requisiti tecnici per l'archiviazione"
TOCTitle: Requisiti tecnici per l'archiviazione
ms:assetid: 896d60e2-be4b-462d-8357-4cd307ab7304
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205059(v=OCS.15)
ms:contentKeyID: 49301236
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per l'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-09_

I requisiti tecnici di Lync Server 2013 includono:

  - Requisiti dell'infrastruttura

  - Software prerequisito da installare per l'archiviazione

  - Requisiti di archiviazione dati per l'archiviazione

  - Considerazioni e requisiti per l'implementazione della scalabilità per la distribuzione di archiviazione

  - Considerazioni e requisiti di prestazioni per i database di archiviazione


> [!NOTE]
> In questa versione di Lync Server 2013 non sono presenti informazioni su scalabilità e rendimento.



## Requisiti dell'infrastruttura

I requisiti dell'infrastruttura di archiviazione di Lync Server 2013 sono gli analoghi ai requisiti della distribuzione di Lync Server 2013. Per informazioni dettagliate, vedere [Determinazione dei requisiti dell'infrastruttura per Lync Server 2013](lync-server-2013-determining-your-infrastructure-requirements.md) nella documentazione relativa alla pianificazione.

## Prerequisiti per l'archiviazione

Lync Server 2013 semplifica i prerequisiti per l'archiviazione, poiché:

  - L'archiviazione non è più un ruolo del server. Ora, gli agenti di raccolta dati unificati sono eseguiti sui server Front End Server in un pool e sui server Standard Edition per la raccolta dei dati di archiviazione, in modo da evitare la configurazione di piattaforme di sistema separate per l'archiviazione.

  - Archiviazione di serve dell'archiviazione file di Lync Server 2013 per archiviare provvisoriamente i file di contenuto delle riunioni, in modo tale da evitare la configurazione di un archivio file separato.

  - In Lync Server 2013, l'accodamento dei messaggi non è richiesto.

## Requisiti di archiviazione dati per l'archiviazione

È inoltre necessario configurare l'infrastruttura per l'archiviazione, eseguendo una o entrambe le operazioni seguenti:

  - **Microsoft Exchange archiviazione**. I file di contenuto delle riunioni, ad esempio le presentazioni PowerPoint, sono archiviate come allegati. Per utilizzare l'integrazione di Microsoft Exchange affinché i dati di archivio di Lync siano archiviati con i dati di conformità di Exchange, è necessario utilizzare Exchange 2013 per la distribuzione di Exchange e assicurarsi che le dimensioni massime di archiviazione supportino l'archiviazione dei file di contenuto della conferenza. Se si distribuisce l'archiviazione attraverso l'opzione di integrazione di Microsoft Exchange, i dati di archivio di Lync sono archiviati insieme ai dati di conformità di Exchange 2013 degli utenti ospitati sui server di Exchange 2013. È necessario distribuire Exchange 2013 prima di distribuire e abilitare l'archiviazione attraverso l'opzione di integrazione di Microsoft Exchange. Se si sceglie di utilizzare l'archiviazione di Exchange 2013, non è necessario distribuire database separati di SQL Server per l'archiviazione, a meno che non esistano utenti di Lync non ospitati sui server di Exchange 2013.

  - Archiviazione database di **SQL Server**. Per supportare gli utenti non ospitati su server di Exchange 2013, o se non si desidera utilizzare l'opzione di integrazione di Microsoft Exchange, è necessario distribuire l'archiviazione con un database di SQL Server. Lync Server 2013 supporta le seguenti versioni a 64 bit di SQL Server:
    
      - Microsoft SQL Server 2008 R2 Enterprise
    
      - Microsoft SQL Server 2008 R2 Standard
    
      - Microsoft SQL Server 2012 Enterprise
    
      - Microsoft SQL Server 2012 Standard
    

    > [!NOTE]
    > Microsoft SQL Server 2008 R2 Express e Microsoft SQL Server 2012 Express non sono supportati per l'archiviazione. Le versioni a 32 bit di SQL Server non sono supportate. Per requisiti e limitazioni aggiuntive di SQL Server, vedere <A href="lync-server-2013-database-software-support.md">Supporto per il software di database in Lync Server 2013</A> nella documentazione relativa alla pianificazione o al supporto.

    
    È necessario configurare le piattaforme di SQL Server prima di distribuire e abilitare l'archiviazione. Se l'account da utilizzare per pubblicare la topologia dispone delle autorizzazioni e dei diritti di amministratore appropriati, è possibile creare il database di archiviazione (LcsLog) quando si pubblica la topologia. È anche possibile creare il database successivamente includendolo alla procedura di installazione. Per informazioni dettagliate su SQL Server, vedere il TechCenter di SQL Server all'indirizzo [http://go.microsoft.com/fwlink/?linkid=129045\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=129045%26clcid=0x410).

