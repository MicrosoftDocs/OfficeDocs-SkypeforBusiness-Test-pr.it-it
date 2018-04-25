---
title: 'Lync Server 2013: Collocazione dei server in una distribuzione server Standard Edition'
TOCTitle: Collocazione dei server in una distribuzione server Standard Edition
ms:assetid: 0763ffab-4fd6-463a-8e62-d97876b376d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398131(v=OCS.15)
ms:contentKeyID: 49299577
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Collocazione dei server in una distribuzione server Standard Edition per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-01-20_

In questa sezione vengono illustrati i ruoli del server, i database e le condivisioni file che è possibile collocare in una distribuzione di server Standard Edition di Lync Server 2013.

## Ruoli del server

In Lync Server 2013 il servizio A/V Conferencing, il Mediation Server, il Monitoring Server e il server di archiviazione sono collocati nel Front End Server, ma per abilitarli sono necessarie alcune operazioni di configurazione aggiuntive. Si può scegliere di distribuire il Mediation Server in server separati.

È possibile collocare un server applicazioni attendibili in un server Standard Edition.

I ruoli del server seguenti devono essere ognuno distribuito in un computer distinto:

  - Server Director

  - server perimetrale

  - Mediation Server (se non collocato con il server Standard Edition)

  - Server Office Web Apps

## Database

Per impostazione predefinita, il database back-end di SQL Server Express è collocato nel server Standard Edition. Non è possibile spostarlo in un computer separato. Con una sola eccezione, non è possibile collocare altri database nel server Standard Edition. Se si sceglie di distribuire server Chat persistente in un server Standard Edition, è possibile collocare il database di Chat persistente e il database di Conformità chat persistente nello stesso server Standard Edition.

È possibile collocare ognuno dei database seguenti in un singolo server di database:

  - database di monitoraggio

  - database di archiviazione

  - Un database back-end per un pool Enterprise Edition Front End

È possibile collocare uno, più o tutti questi database in una singola istanza SQL oppure utilizzare un'istanza SQL separata per ognuno, con le limitazioni seguenti:

  - Ogni istanza SQL può includere solo un database back-end (per un pool Enterprise Edition Front End), un database di monitoraggio, un database di archiviazione, un database Persistent Chat e un database di Conformità Persistent Chat.

  - Il server di database non può supportare più di un pool Enterprise Edition Front End, un server di archiviazione, un Monitoring Server, un database di Chat persistente e un database di Conformità Chat persistente, ma può supportare uno di ognuno, indipendentemente dal fatto che i database utilizzino la stessa istanza di SQL Server o istanze di SQL Server separate.

È possibile collocare una condivisione file con i database, come descritto più avanti in questa sezione.


> [!NOTE]
> Lync Server 2013 consente di integrare l'archivio del Monitoring Server e quello del server di archiviazione con l'archivio di Exchange 2013 per uno o tutti gli utenti della distribuzione. Non è possibile distribuire server che eseguono Lync Server o componenti negli stessi server dell'archivio di Exchange.



<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sebbene la collocazione dei database sia supportata, la dimensione dei database può aumentare rapidamente. Ad esempio, se si intende collocare il database di archiviazione con altri database, è opportuno tenere presente che l'archiviazione dei messaggi di più utenti può comportare un notevole aumento dello spazio su disco richiesto dal database di archiviazione. Per questo motivo, non è consigliabile collocare più database, in particolare il database di archiviazione, il database di Chat persistente e il database di Conformità Chat persistente, con il database back-end di un pool Enterprise.</td>
</tr>
</tbody>
</table>


## Condivisioni file

La condivisione file può essere un server separato o essere collocata nello stesso server utilizzato da uno, più o tutti gli elementi seguenti:

  - Server di database, inclusi il server back-end di un pool Enterprise Edition Front End

  - database di archiviazione

  - database di monitoraggio

  - Database di Chat persistente

  - Database di Conformità Chat persistente

Una singola condivisione file può essere utilizzata per più pool Front End e server Standard Edition, tutti nello stesso sito.


> [!NOTE]
> In Lync Server 2013, Monitoring Server e server di archiviazione usano la condivisione file di Lync Server come server Standard Edition.



## Altri componenti

Non è possibile collocare un server proxy inverso, che non è un componente di Lync Server 2013, ma è necessario nella distribuzione se si desidera supportare la condivisione del contenuto Web per gli utenti federati, con alcun ruolo del server di Lync Server 2013. È tuttavia possibile implementare il supporto del proxy inverso per una distribuzione di Lync Server 2013 configurando il supporto in un server proxy inverso esistente dell'organizzazione utilizzato per altre applicazioni.

Non è possibile collocare alcun componente di Messaggistica unificata di Exchange o di SharePoint con alcun ruolo di Lync Server 2013.

