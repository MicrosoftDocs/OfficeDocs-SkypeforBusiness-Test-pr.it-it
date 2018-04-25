---
title: 'Lync Server 2013: Componenti e topologie per il server Chat persistente'
TOCTitle: Componenti e topologie per il server Chat persistente
ms:assetid: 6a0a14a0-baad-44e9-b26e-4d192c0a0e70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398500(v=OCS.15)
ms:contentKeyID: 49300868
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

server Chat persistente supporta sia configurazioni con server singolo che con più server. È inoltre possibile eseguire server Chat persistente in un Lync Server 2013server Standard Edition. Queste configurazioni includono i componenti e le topologie seguenti di server Chat persistente.

## Componenti di server Chat persistente

L'installazione dell'ultima versione di server Chat persistente richiede i componenti seguenti:

  - Uno o più computer che eseguono server Chat persistente e offrono i servizi seguenti:
    
      - Servizio Chat persistente
    
      - Servizio di conformità, attivato se la conformità è abilitata
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>In Lync Server 2013, i servizi Web di Chat persistente per il caricamento e il download di file sono ora collocati con Lync Server 2013Front End Server.<br />
    Anche i servizi Web di Chat persistente per la gestione delle chat room sono collocati con Lync Server 2013Front End Server.</td>
    </tr>
    </tbody>
    </table>


  - Il server o i server (più server se si utilizza il mirroring) che ospitano il database back-end di SQL Server per l'hosting del database del contenuto di Chat persistente in cui vengono archiviati il contenuto delle chat room, le chat e le categorie.
    

    > [!NOTE]
    > Nel database back-end vengono archiviati i dati di cronologia delle chat, incluse informazioni sulle categorie e le chat di Chat persistente create.



  - Se è abilitata la conformità, il server o i server (più server se si utilizza il mirroring) che ospitano il database back-end di SQL Server per l'hosting del database di conformità di Chat persistente in cui vengono archiviati gli eventi relativi alla conformità e il contenuto delle chat riferito alla conformità.

Per amministrare server Chat persistente da un computer separato, come una console di amministrazione, utilizzare il Pannello di controllo di Lync Server nel computer. Questo computer deve essere poi distribuito in un dominio di Servizi di dominio Active Directory, con almeno un server di catalogo globale nella radice della foresta.

Per informazioni dettagliate sui requisiti hardware e software per server Chat persistente, vedere [Requisiti tecnici per il server Chat persistente in Lync Server 2013](lync-server-2013-technical-requirements-for-persistent-chat-server.md), [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) e [Supporto dell'infrastruttura e del software server in Lync Server 2013](lync-server-2013-server-software-and-infrastructure-support.md) nella documentazione relativa alla supportabilità.

## Collocazione supportata

Lync Server 2013 supporta diversi scenari di collocazione, che offrono la flessibilità necessaria per risparmiare sui costi hardware grazie all'esecuzione di più componenti su un solo server (se l'organizzazione è di piccole dimensioni) o alla possibilità di eseguire singoli componenti in server differenti (se l'organizzazione è più grande e richiede scalabilità e prestazioni elevate). Prima di decidere se collocare i componenti, è sicuramente importante considerare i fattori di scalabilità.

Il servizio di conformità di Chat persistente, se la conformità è abilitata, è collocato con Lync Server 2013Front End Server.

È possibile distribuire server Chat persistente nel Server Standard Edition. Il server back-end di server Chat persistente e il database di conformità di Chat persistente possono essere collocati nel server Standard Edition nel server back-end locale di SQL Server Express. Per informazioni dettagliate sui componenti che possono essere collocati, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md) nella documentazione relativa alla supportabilità.

Per Lync Server 2013Enterprise Edition non è consentita la collocazione di server Chat persistente nel Server Enterprise Edition. Il database di SQL Server per server Chat persistente può essere collocato con il database del server back-end di un Enterprise Editionpool Front End. Il database di SQL Server per la conformità di Chat persistente può essere inoltre collocato con il database del server back-end di un pool Enterprise Edition.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il server che ospita il database di Chat persistente può ospitare altri database. Se, tuttavia, si desidera collocare il database di Chat persistente con altri database, è opportuno tenere presente che l'archiviazione dei messaggi di più utenti può comportare un notevole aumento dello spazio su disco richiesto dal database di Chat persistente. Per questo motivo non è consigliabile collocare il database di Chat persistente con il database back-end.</td>
</tr>
</tbody>
</table>


Se si colloca il database di Chat persistente con il database back-end, è possibile utilizzare una singola istanza di SQL Server per uno o per tutti i database o, in alternativa, utilizzare un'istanza di SQL Server separata per ogni database, con la limitazione seguente:

  - Ogni istanza di SQL Server può contenere un singolo database back-end e un singolo database di Chat persistente.

Per informazioni dettagliate sulla collocazione di tutti i ruoli server e database, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md) nella documentazione relativa alla supportabilità.

## Topologie di server Chat persistente

server Chat persistente supporta le topologie seguenti:

  - Lync Server 2013 Enterprise Edition server Chat persistenteFront End Server (server singolo)

  - Lync Server 2013 Enterprise Edition server Chat persistenteFront End Server (più server)

  - Lync Server 2013server Standard Edition con SQL Server Express

  - Lync Server 2013server Standard Edition e server Chat persistente in un server separato con server Standard Edition come server dell'hop successivo.

È possibile aggiungere server Chat persistente alla distribuzione di Lync Server 2013 tramite Generatore di topologie. È possibile aggiungere un pool di server Chat persistente con singolo server o più server alla topologia.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dopo aver creato un pool di server Chat persistente con un singolo server tramite Generatore di topologie, non è possibile aggiungere ulteriori server al pool.</td>
</tr>
</tbody>
</table>


## Topologia a server singolo

La configurazione minima e la distribuzione più semplice di server Chat persistente prevede una topologia server Chat persistenteFront End Server a server singolo. In questa distribuzione è richiesto un singolo server che esegue server Chat persistente (ed esegue facoltativamente il servizio di conformità, se la conformità è abilitata), un server che ospita entrambi i database di SQL Server e, se è richiesta la conformità, il database di SQL Server per archiviare i dati di conformità.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Non è possibile aggiungere ulteriori server a un pool di server Chat persistente avviato come distribuzione a server singolo in Generatore di topologie. È consigliabile utilizzare la topologia con pool di più server, anche se si utilizza un singolo server, in modo da poter aggiungere ulteriori server in seguito all'occorrenza.</td>
</tr>
</tbody>
</table>


Nella figura seguente sono illustrati tutti i componenti obbligatori e facoltativi di una topologia per un singolo server Chat persistenteFront End Server con conformità.

**Singolo server di Chat persistente**

![Topologia a un solo server con Compliance Service](images/Gg398500.9168fa52-61e0-4d17-a14d-45fd32e81456(OCS.15).jpg "Topologia a un solo server con Compliance Service")

## Topologia a più server

Per offrire capacità e affidabilità maggiori, è possibile distribuire una topologia a più server, descritta in [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md). La topologia a più server può includere fino a quattro computer attivi che eseguono server Chat persistente (le configurazioni per la disponibilità elevata e il ripristino di emergenza consentiranno fino a otto computer, ma solo quattro possono essere attivi e i rimanenti quattro saranno in standby). Ogni server può supportare fino a 20.000 utenti simultanei, per un totale di 80.000 utenti simultanei connessi a un pool di server Chat persistente con 4 server. Una topologia a più server è analoga a una topologia a server singolo, con la differenza che più server ospitano server Chat persistente e possono offrire maggiore scalabilità. Più computer che eseguono server Chat persistente devono risiedere nello stesso dominio di Servizi di dominio Active Directory di Lync Server e del servizio di conformità.

Nella figura seguente vengono illustrati tutti i componenti di una topologia a più server con più computer che eseguono server Chat persistente, il servizio di conformità facoltativo e un database di conformità distinto.

**Più server di Chat persistente**

![Topologia a più server](images/Gg398500.19aea898-28df-4d9b-903c-f72ef062d919(OCS.15).jpg "Topologia a più server")

Le topologie a più server consentono di creare pool delle funzionalità dei server. In un pool di server i servizi Chat persistente comunicano e condividono dati. La cronologia delle chat originariamente pubblicata in un solo servizio Chat persistente, ad esempio, è disponibile da qualsiasi servizio Chat persistente nel sistema. Un file caricato mediante un servizio Chat persistente è infatti accessibile da qualsiasi servizio Chat persistente. Gli utenti possono essere connessi a diversi server Chat persistenteFront End Server e conversare e comunicare tra loro.

La porta predefinita TCP 8011 connette un server a un pool di server e viene utilizzata dal servizio Chat persistente per le comunicazioni tra i server o per scopi amministrativi.

