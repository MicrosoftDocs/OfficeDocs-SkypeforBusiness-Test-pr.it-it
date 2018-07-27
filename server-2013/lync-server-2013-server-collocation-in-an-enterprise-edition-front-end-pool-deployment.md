---
title: 'Lync Server 2013: Collocazione dei server in una distribuzione di pool Enterprise Edition Front End'
TOCTitle: Collocazione dei server in una distribuzione di pool Enterprise Edition Front End
ms:assetid: 0516b18d-14c0-4237-9279-0f92e341b1bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398102(v=OCS.15)
ms:contentKeyID: 49299544
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Collocazione dei server in una distribuzione di pool Enterprise Edition Front End per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-11_

In questa sezione vengono illustrati i ruoli del server, i database e le condivisioni file che è possibile collocare in una distribuzione di pool Front End di Lync Server 2013.

## Ruoli del server

In Lync Server 2013 il servizio A/V Conferencing, il Mediation Server, il Monitoring Server e il server di archiviazione sono collocati nel Front End Server, ma per abilitarli sono necessarie alcune operazioni di configurazione aggiuntive. Se si sceglie di non collocare il Mediation Server nel Front End Server, è possibile distribuirlo come Mediation Server autonomo in un computer distinto.

È possibile collocare un server applicazioni attendibili nel Front End Server.

I ruoli del server seguenti devono essere ognuno distribuito in un computer distinto:

  - Server Director

  - server perimetrale

  - Mediation Server (se non collocato con il Front End Server)

  - Server Office Web Apps

Non è possibile collocare il ruolo server Chat persistente con Front End Server.

## Database

È possibile collocare ognuno dei database seguenti nello stesso server di database:

  - Database back-end

  - database di monitoraggio

  - database di archiviazione

  - Database di Chat persistente

  - Database di Conformità Chat persistente

È possibile collocare uno, più o tutti questi database in una singola istanza di SQL Server oppure utilizzare un'istanza di SQL Server separata per ognuno, con le limitazioni seguenti:

  - Ogni istanza di SQL Server può includere solo un database back-end, un database di monitoraggio, un database di archiviazione, un database di Chat persistente e un un database di Conformità Chat persistente.

  - Il server di database non è in grado di supportare più di un pool Front End, una distribuzione di archiviazione e una distribuzione di monitoraggio, ma può supportarne uno di ciascun tipo, indipendentemente dal fatto che i database utilizzino la stessa istanza di SQL Server o istanze di SQL Server separate.

È possibile collocare una condivisione file con i database, come descritto più avanti in questa sezione.


> [!NOTE]
> Lync Server 2013 consente di integrare l'archivio di archiviazione con l'archivio di Exchange 2013 per uno o tutti gli utenti della distribuzione. Non è possibile distribuire server che eseguono Lync Server o componenti negli stessi server dell'archivio di Exchange.



> [!IMPORTANT]  
> Sebbene la collocazione dei database sia supportata, la dimensione dei database può aumentare rapidamente. Ad esempio, se si intende collocare il database di archiviazione con altri database, è opportuno tenere presente che l'archiviazione dei messaggi di più utenti può comportare un notevole aumento dello spazio su disco richiesto dal database di archiviazione. Per questo motivo, non è consigliabile collocare più database, in particolare il database di archiviazione, il database di Chat persistente o il database di Conformità Chat persistente, con il database back-end.

## Condivisione file

La condivisione file può essere un server separato o essere collocata nello stesso server utilizzato da uno, più o tutti gli elementi seguenti:

  - Server di database, inclusi il server back-end di un pool Enterprise Edition Front End

  - database di archiviazione

  - database di monitoraggio

  - Database di Chat persistente

  - Database di Conformità Chat persistente

Una singola condivisione file può essere utilizzata per più pool Front End e server Standard Edition, tutti nello stesso sito.


> [!NOTE]
> In Lync Server 2013, Monitoring Server e server di archiviazione usano la condivisione file di Lync Server come Front End Server.



## Altri componenti

Non è possibile collocare un server proxy inverso, che non è un componente di Lync Server 2013, ma è necessario nella distribuzione se si desidera supportare la condivisione del contenuto Web per gli utenti federati, con alcun ruolo del server di Lync Server 2013. È tuttavia possibile implementare il supporto del proxy inverso per una distribuzione di Lync Server 2013 configurando il supporto in un server proxy inverso esistente dell'organizzazione utilizzato per altre applicazioni.

Non è possibile collocare alcun componente di Messaggistica unificata di Exchange o di SharePoint con alcun ruolo di SharePoint Server.

