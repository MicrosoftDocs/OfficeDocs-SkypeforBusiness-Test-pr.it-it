---
title: "Lync Server 2013: Componenti e topologie per l'archiviazione"
TOCTitle: Componenti e topologie per l'archiviazione
ms:assetid: 5893063d-a44a-4034-aba9-cbe883ecf710
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204916(v=OCS.15)
ms:contentKeyID: 49300644
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per l'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Se si vuole archiviare contenuto di conferenze e messaggistica istantanea di Lync Server 2013, è possibile implementare l'archiviazione in Lync Server.

## Componenti di archiviazione

La funzionalità di archiviazione include i componenti seguenti:

  - **Agenti di archiviazione**. Gli agenti di archiviazione, noti anche come agenti di raccolta dati unificata, vengono installati e attivati automaticamente in ogni pool Front End e in ogni server Standard Edition. Anche se gli agenti di archiviazione vengono attivati automaticamente, l'acquisizione dei messaggi inizia solo dopo che l'archiviazione è stata abilitata e configurata in modo appropriato.

  - **Archivio dati di archiviazione**. L'archivio dati per Lync Server 2013 può essere costituito da uno dei seguenti:
    
      - Archivio Exchange 2013. Se si abilita l'opzione di integrazione di Microsoft Exchange, le cassette postali degli utenti ospitate nel server Exchange 2013 usano l'archivio Exchange 2013 per i dati archiviati, ma solo se le cassette postali sono impostate per l'archiviazione sul posto.
    
      - Archivio SQL Server. Se nella distribuzione alcuni utenti sono ospitati in Lync Server 2013, per consentire l'archiviazione di questi è possibile installare database di archiviazione che eseguono una versione supportata di SQL Server.

L'archiviazione richiede anche un archivio file, ma usa lo stesso archivio file dei Front End Server o del server Standard Edition.

Per l'elenco dei requisiti hardware e software per l'archiviazione, vedere [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) e [Supporto dell'infrastruttura e del software server in Lync Server 2013](lync-server-2013-server-software-and-infrastructure-support.md) nella documentazione relativa alla supportabilità.

## Topologie supportate

È necessario distribuire la funzionalità di archiviazione in ogni pool in cui si trovano utenti che richiedono il supporto dell'archiviazione. L'archiviazione viene eseguita su Front End Server in pool di Enterprise Edition e su server Standard Edition. L'archivio dati di archiviazione può essere:

  - Integrato con l'archivio Exchange 2013

  - Distribuito usando database SQL Server separati

Se la distribuzione Exchange 2013 non include tutti gli utenti della distribuzione Lync Server, è necessario usare l'integrazione di Microsoft Exchange per gli utenti le cui cassette postali sono disponibili in server Exchange 2013 ed è necessario distribuire database SQL Server separati per l'archiviazione per tutti gli altri utenti Lync.

## Collocazione supportata

Lync Server 2013 supporta diversi scenari di collocazione, che offrono la flessibilità necessaria per risparmiare sui costi hardware grazie all'esecuzione di più componenti su un solo server (se l'organizzazione è di piccole dimensioni) o alla possibilità di eseguire singoli componenti in server differenti (se l'organizzazione è più grande e richiede scalabilità e prestazioni elevate). Prima di decidere se collocare i componenti, è sicuramente importante considerare i fattori di scalabilità.

L'archiviazione viene distribuita nei Front End Server di un pool o in server Standard Edition. Per informazioni dettagliate sui componenti che possono essere collocati, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md) nella documentazione relativa alla supportabilità.

Se per l'archiviazione si usano database SQL Server separati, in sostituzione o in aggiunta all'integrazione dell'archivio con l'archivio Exchange 2013, è possibile collocare il database di archiviazione con:

  - database di monitoraggio

  - Database back-end di un pool Enterprise Edition Front End


> [!NOTE]
> Il server che ospita il database di archiviazione può ospitare altri database. Se, tuttavia, si desidera collocare il database di archiviazione con altri database, è opportuno tenere presente che l'archiviazione dei messaggi di più utenti può comportare un notevole aumento dello spazio su disco richiesto dal database di archiviazione. Per questo motivo non è consigliabile collocare il database di archiviazione con il database back-end.



Se si colloca il database di archiviazione con il database di monitoraggio, il database back-end o entrambi i database, è possibile usare una singola istanza SQL per uno o per tutti i database o, in alternativa, usare un'istanza SQL separata per ogni database, con la limitazione seguente:

  - Ogni istanza SQL può contenere un singolo database back-end, un singolo database di monitoraggio e un singolo database di archiviazione.

Per informazioni dettagliate sulla collocazione di tutti i ruoli server e database, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md) nella documentazione relativa alla supportabilità.

