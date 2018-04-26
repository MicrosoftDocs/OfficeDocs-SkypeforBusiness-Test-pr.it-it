---
title: Configurazione dell'archivio per l'archiviazione
TOCTitle: Configurazione dell'archivio per l'archiviazione
ms:assetid: f751245c-743e-454f-8325-968ae5e3de71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205392(v=OCS.15)
ms:contentKeyID: 49302499
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'archivio per l'archiviazione

 

_**Ultima modifica dell'argomento:** 2013-12-17_

L'archiviazione per Lync Server 2013 include quanto segue:

  - **Archivio dati**   L'archivio dati è necessario per archiviare il contenuto della messaggistica istantanea.

  - **Archivio file**   L'archivio file è necessario per archiviare dati e file del contenuto delle conferenze (riunioni).

## Configurazione dell'archivio dati

I requisiti per la configurazione dell'archivio dati per l'archiviazione in Lync Server 2013 dipendono da come si desidera archiviare i dati di archiviazione:

  - Integrare l'archiviazione di Lync Server 2013 con la distribuzione di Exchange per archiviare i dati di archiviazione utilizzando l'archivio di Exchange.

  - Configurare server di database SQL Server distinti per archiviare i dati di archiviazione.

## Configurazione dell'archiviazione di Exchange per l'archiviazione dei dati

Per configurare l'archiviazione dei dati in Exchange è necessario che Exchange 2013 sia in esecuzione nella distribuzione di Exchange. È inoltre necessario ospitare le cassette postali degli utenti nel server di Exchange 2013 e impostare le cassette postali su Archiviazione sul posto. Per ulteriori informazioni sulla configurazione di Exchange 2013, vedere la documentazione del prodotto di Exchange.

## Configurazione dei server database di SQL Server per l'archiviazione dei dati

Per eseguire l'archiviazione in Lync Server 2013, è necessario che il software database di SQL Server archivi i dati archiviati, a meno che la distribuzione non venga integrata con Exchange.

Per i database di archiviazione di SQL Server è necessario installare SQL Server nel computer che ospiterà il database di archiviazione. È possibile utilizzare la stessa istanza SQL utilizzata per il database back-end di un pool Front End. Per ottenere prestazioni ottimali, è consigliabile distribuire il database di archiviazione in un computer distinto dall'archivio di gestione centrale. Per informazioni dettagliate sulla collocazione dei componenti di Lync Server 2013, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md) nella documentazione relativa al supporto.

È necessario che tutti i server di database eseguano una versione supportata di SQL Server. Per informazioni dettagliate sulle versioni supportate, vedere [Requisiti tecnici per l'archiviazione in Lync Server 2013](lync-server-2013-technical-requirements-for-archiving.md) nella documentazione relativa alla pianificazione.

È necessario configurare le piattaforme di SQL Server prima di distribuire e abilitare l'archiviazione. Se l'account da utilizzare per pubblicare la topologia dispone delle autorizzazioni e dei diritti di amministratore appropriati, è possibile creare il database di archiviazione (LcsLog) quando si pubblica la topologia. È anche possibile creare il database successivamente includendolo alla procedura di installazione. Per informazioni dettagliate su SQL Server, vedere il TechCenter di SQL Server all'indirizzo [http://go.microsoft.com/fwlink/?linkid=129045\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=129045%26clcid=0x410).


> [!NOTE]
> Assicurare che il tipo di avvio del servizio SQL Server Agent sia impostato su Automatico e che il servizio SQL Server Agent sia in esecuzione per l'istanza SQL che include i database di archiviazione, in modo che sia possibile eseguire i processi di manutenzione predefiniti di SQL Server per l'archiviazione in base alla relativa pianificazione sotto il controllo del servizio SQL Server Agent.



## Configurazione dell'archiviazione dei file

L'archiviazione utilizza la condivisione di file di Lync Server 2013 specificata durante la configurazione del pool Front End o del server Standard Edition. Non è possibile modificare la condivisione di file utilizzata per l'archiviazione. Per informazioni dettagliate sui sistemi di archiviazione di file supportati, vedere [Supporto dell'archiviazione di file in Lync Server 2013](lync-server-2013-file-storage-support.md) nella documentazione relativa alla supportabilità.

