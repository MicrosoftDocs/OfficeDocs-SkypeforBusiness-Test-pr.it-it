---
title: 'Lync Server 2013: Nuove funzionalità del server Chat persistente'
TOCTitle: Nuove funzionalità del server Chat persistente
ms:assetid: c3ec6f33-6261-4bf5-aa31-baa8ab2a87d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412965(v=OCS.15)
ms:contentKeyID: 49301911
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuove funzionalità del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

Il server Chat persistente di Lync Server 2013 consente di partecipare a conversazioni per più partecipanti basate su un argomento che permangono nel tempo. Il server Chat persistente consente all'organizzazione di eseguire le operazioni seguenti:

  - Migliorare le comunicazioni tra team interfunzionali e distribuiti in zone geografiche diverse

  - Ampliare la condivisione delle informazioni e la partecipazione

  - Migliorare le comunicazioni con l'organizzazione estesa

  - Ridurre il sovraccarico di informazioni

  - Migliorare la consapevolezza delle informazioni

  - Migliorare la diffusione di informazioni e conoscenze importanti

Il server Chat persistente di Lync Server 2013 non è disponibile in Microsoft Office 365. Per il momento è disponibile solo per i clienti di Lync 2013 locale.

In Lync 2013 la funzionalità Chat persistente è integrata nel client Lync 2013. Gli utenti pertanto hanno accesso alle funzionalità di messaggistica istantanea/presenza, audio/video, conferenze e Chat persistente nel client Lync 2013. Per ulteriori informazioni sul client Lync 2013, vedere <http://go.microsoft.com/fwlink/p/?linkid=270877>.

In questo argomento vengono descritte le differenze a livello di funzionalità tra la nuova versione del server Chat persistente di Lync Server 2013 e la versione precedente ( Microsoft Lync Server 2010, Group Chat), che includono:

  - Disponibilità di un'interfaccia amministrativa nel Pannello di controllo di Lync Server ed eliminazione dello strumento di amministrazione Group Chat

  - Integrazione delle impostazioni di configurazione del server Chat persistente in Generatore di topologie con l'eliminazione dello strumento di configurazione Group Chat

  - Semplificazione della migrazione e aggiornamento dalle versioni precedenti del server Chat persistente

  - Soluzioni di ripristino di emergenza e disponibilità elevata

Per ulteriori informazioni sull'ultima versione del server Chat persistente, vedere quanto segue:

  - La Guida di Chat persistente all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=270945>, che include un elenco dettagliato delle funzionalità di Chat persistente, nonché informazioni sul funzionamento e sull'utilizzo di tali funzionalità durante l'esecuzione del server Chat persistente.

  - Gli argomenti [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione, [Distribuzione del server Chat persistente in Lync Server 2013](lync-server-2013-deploying-persistent-chat-server.md) nella documentazione relativa alla distribuzione, [Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md) nella documentazione relativa alla migrazione e [Gestione del server chat persistente di Lync Server 2013](managing-lync-server-2013-persistent-chat-server.md) nella documentazione relativa alle operazioni, che forniscono tutti istruzioni per la configurazione del server Chat persistente.

  - Il file Documentation.msi del server Chat persistente (file di Windows Installer), che consente di accedere a documentazione offline completa sul server Chat persistente.

## Modifiche principali della topologia per il server Chat persistente

Vengono elencate di seguito le modifiche generali per il server Chat persistente:

Il server Chat persistente è ora un ruolo del server. In Microsoft Lync Server 2010Group Chat Server invece è un'applicazione attendibile di terze parti per Microsoft Lync Server 2010. È possibile aggiungere Chat persistente a una topologia di Lync Server 2013 utilizzando Generatore di topologie. In Lync Server 2013 la funzionalità del server Chat persistente viene implementata utilizzando tre nuovi ruoli del server:

  - **PersistentChatService :** questo è il ruolo front-end per Chat persistente. Nelle distribuzioni Standard Edition il ruolo del servizio server Chat persistente è collocato nel server Standard Edition distribuito da Bootstrapper, come qualsiasi altro ruolo di Lync Server. Nelle distribuzioni Enterprise Edition il ruolo del servizio Chat persistente viene distribuito in computer autonomi da Bootstrapper, come qualsiasi altro ruolo di Lync Server.

  - **PersistentChatStore :** server back-end che corrisponde al database del contenuto di Chat persistente, in cui viene archiviato tutto il contenuto delle chat.

  - **PersistentChatComplianceStore :** ruolo back-end che corrisponde al database di Conformità Chat persistente, in cui vengono archiviati tutti gli eventi di conformità.

Questi ruoli del server Chat persistente sono facoltativi e vengono installati solo dai clienti che desiderano usufruire delle funzionalità del server Chat persistente complete. Il ruolo **PersistentChatComplianceStore** è necessario solo se si sceglie di distribuire Conformità Chat persistente.

Il ruolo **PersistentChatService** esegue due servizi:

  - Servizio Chat persistente

  - Servizio Conformità Chat persistente

L'esecuzione di questi servizi in ogni server Chat persistente consente di usufruire della disponibilità elevata di questi servizi in un pool di server Chat persistente multiserver.

Per supportare il caricamento e il download di file in chat room di Chat persistente, il server Chat persistente include un servizio Web. Nelle versioni precedenti questo servizio è collocato nel Front End Server del server Chat persistente e richiede l'installazione di Internet Information Services (IIS) come prerequisito. Nel server Chat persistente di Lync Server 2013 il servizio Web di caricamento/download dei file è collocato con il Front End Server di Lync Server 2013, pertanto Internet Information Services (IIS) non è più un prerequisito per il server Chat persistente. Il servizio Web di caricamento/download dei file è identificato come **PersistentChat** in Gestione Internet Information Services (IIS).

> [!IMPORTANT]  
> Il ruolo <strong>PersistentChatService</strong> può essere eseguito nello stesso server di Lync Server 2013Front End Server solo se il Front End Server è di tipo Standard EditionFront End Server. Il ruolo <strong>PersistentChatService</strong> non può essere eseguito separatamente da Lync Server 2013Front End Server. Può essere installato solo nel contesto di una distribuzione di Lync Server 2013.

Nel server Chat persistente il servizio di ricerca è stato eliminato. In Lync Server 2010, Group Chat il servizio di ricerca viene eseguito in ogni Front End Server di Group Chat Server ed esegue il routing in uno dei Channel Server. Lync Server 2013 si basa sul routing utilizzando oggetti contatto, in cui ogni pool di server Chat persistente è rappresentato da un oggetto contatto utilizzato dai Lync ServerFront End Server per identificare e instradare le richieste a un pool di server Chat persistente appropriato e a uno dei computer che eseguono il server Chat persistente nel pool.

In Lync Server 2013 sono state apportate modifiche al servizio Conformità:

  - In Lync Server 2010 il servizio Conformità viene eseguito in modalità autonoma (non collocato) e solo in un singolo server. Il servizio Conformità ora viene eseguito in tutti i Front End Server del server Chat persistente, insieme al servizio Chat persistente e offre pertanto la disponibilità elevata in un pool di server Chat persistente multiserver. È possibile configurare un singolo adattatore conformità per estrarre i dati dal database di conformità in uno degli altri sistemi (file XML, archivi ospitati da Exchange e così via). Il server Chat persistente include un adattatore XML.

  - La coda di Accodamento messaggi (noto anche come MSMQ) condivisa dal servizio Chat persistente e dal servizio Conformità in ogni Front End Server del server Chat persistente è ora una coda privata condivisa solo dai due servizi. Tutti i servizi di conformità scrivono nello stesso database back-end di conformità. Leggono inoltre i dati da tale database per inviarli alla propria istanza dell'adattatore. Il server back-end di conformità è rappresentato da un nuovo ruolo server back-end.
    
    > [!IMPORTANT]  
    > Analogamente alle versioni precedenti, tutti i dati di conformità vengono elaborati solo una volta. I dati possono essere elaborati da qualsiasi istanza dell'adattatore richiamata dal servizio di conformità in esecuzione nei diversi computer server Chat persistente di Lync Server 2013. Nel server Chat persistente i dati possono essere elaborati da qualsiasi istanza dell'adattatore.    

    > [!NOTE]
    > Per informazioni sull'installazione di Accodamento messaggi, vedere <A href="lync-server-2013-install-operating-systems-and-prerequisite-software-on-servers.md">Installare i sistemi operativi e il software prerequisito nei server per Lync Server 2013</A> nella documentazione relativa alla distribuzione.



In Lync Server 2013 sono stati apportati miglioramenti sia alla disponibilità elevata che al ripristino di emergenza:

  - Miglioramenti della disponibilità elevata: viene utilizzato il mirroring di SQL Server per fornire la disponibilità elevata per il database del contenuto del server Chat persistente e per il database di conformità Chat persistente in un data center (in loco).

  - Miglioramenti del ripristino di emergenza: il server Chat persistente supporta un'architettura di pool estesi che consente di estendere un singolo pool di server Chat persistente su due siti, ovvero un singolo pool logico della topologia con server del pool posizionati fisicamente in due siti. Viene utilizzata la funzionalità Log Shipping di SQL Server per il ripristino di emergenza intersito.

Per ulteriori informazioni sulla disponibilità elevata e sul ripristino di emergenza, vedere [Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md) nella documentazione relativa alla distribuzione.

## Modifiche principali dell'amministrazione e della gestione per il server Chat persistente

In Lync Server 2013 l'amministrazione e la gestione del server Chat persistente sono state semplificate grazie alle modifiche seguenti:

  - Amministrazione e gestione unificate. In Lync Server 2013 è più semplice gestire e amministrare il server Chat persistente utilizzando strumenti già noti agli amministratori di Lync. Il server Chat persistente include un'interfaccia utente amministrativa integrata con il Pannello di controllo di Lync Server, in modo da risolvere i problemi di prestazioni con le versioni precedenti dell'interfaccia utente di Group Chat Server. Nel server Chat persistente è inclusa inoltre una raccolta di cmdlet di Windows PowerShell per amministrare e gestire le categorie del server Chat persistente, le chat room del server Chat persistente (inclusa l'eliminazione di chat room e di contenuto obsoleto) e i componenti aggiuntivi.

  - Modello di amministrazione semplificato. In Lync Server 2013 è stato modificato e semplificato il modello del server Chat persistente con l'implementazione dei requisiti principali seguenti segnalati dai clienti:
    
      - Rimozione delle gerarchie annidate complesse di ambiti e categorie.
    
      - Supporto per la definizione di elenchi di membri non consentiti oltre agli elenchi di membri consentiti (ambiti) per i clienti MindAlign correnti che pianificano la migrazione al server Chat persistente.

## Differenze nei ruoli utente rispetto alle versioni di Group Chat Server precedenti

In Lync Server 2010, Group Chat sono inclusi un ruolo amministratore utenti, un ruolo amministratore chat room e un ruolo amministratore Lync Server per la gestione dei componenti aggiuntivi. Nel server Chat persistente è disponibile solo un ruolo amministratore di Chat persistente simile agli altri ruoli del controllo di accesso basato sui ruoli (RBAC) di Lync Server. Chiunque sia membro di questo ruolo RBAC può gestire le chat room, i componenti aggiuntivi e le categorie (e quindi accedere a tali categorie), nonché la configurazione del pool di server Chat persistente.

## Differenze nelle categorie di chat room rispetto alle versioni di Group Chat Server precedenti

Le categorie di chat room non possono più essere annidate e la categoria radice non può più essere modificata. Gli elenchi AllowedMembers/DeniedMembers equivalgono agli ambiti delle versioni legacy di Group Chat Server, con la differenza che gli ambiti non supportano la specifica di un elenco di membri non consentiti. Gli ambiti non possono più essere sostituiti, poiché non sono presenti categorie annidate. Un amministratore di Chat persistente in Lync Server 2013 può creare e gestire categorie di chat room. Nella creazione e nella gestione delle categorie di chat room un amministratore di Chat persistente può configurare entità (gruppi/contenitori/utenti di Active Directory) che possono essere membri/creatori di chat room di una categoria specifica. Un amministratore di Chat persistente può inoltre aggiungere membri non consentiti (DeniedMembers) a una categoria come esclusioni esplicite per l'elenco di membri consentiti. I membri non consentiti (DeniedMembers) hanno la precedenza sui membri inclusi nell'elenco dei membri consentiti (AllowedMembers).

## Differenze nelle proprietà di chat room rispetto alle versioni di Group Chat Server precedenti

Nel server Chat persistente di Lync Server 2013 è presente in nuovo concetto di chat room aperte. Tutti i membri consentiti possono partecipare alla chat room, senza appartenenza esclusiva.

Sono state eliminate le proprietà di chat room seguenti incluse nelle versioni precedenti del server Chat persistente:

  - Argomento: una chat room ora è associata solo a una descrizione.

  - Creazione dell'elenco di nuovi membri: nel server Chat persistente tutte le chat room iniziano senza membri (e possono ingrandirsi fino a includere tutti i membri consentiti).

  - Caricamento file: nelle versioni precedenti questa impostazione viene definita per specificare se nelle chat room sono consentiti i caricamenti/download di file. Ora questa impostazione viene specificata solo a livello di categoria e si applica a tutte le chat room della categoria.

  - Cronologia chat: nelle versioni precedenti questa impostazione viene definita per specificare se nelle chat room è abilitata la cronologia di chat, mentre ora questa impostazione viene specificata solo a livello di categoria e si applica a tutte le chat room della categoria.

  - Inviti: una chat room eredita sempre le impostazioni degli inviti della categoria. Questa impostazione può essere disattivata nella chat room. In una chat room non è possibile attivare gli inviti se nella categoria sono stati precedentemente disattivati.

## Differenze nei criteri rispetto alle versioni di Group Chat Server precedenti

Nel server Chat persistente sono abilitati nuovi criteri di Lync con Chat persistente, in base alle impostazioni utente/pool/sito/globali. Nel client Lync 2013 l'ambiente Chat persistente è disponibile solo per gli utenti abilitati per Chat persistente in base ai criteri (direttamente oppure tramite impostazione di pool/sito/globale).

Nelle versioni di Group Chat Server precedenti non sono presenti criteri integrati nei criteri di Lync Server. È possibile definire per singolo utente e per singola categoria/chat room il ruolo di amministratore utenti o amministratore chat room oppure utilizzare la funzionalità **Can Upload Files** per singolo utente per abilitare il caricamento dei file. La funzione del server Chat persistente**Caricamento file** è disponibile solo per categoria.

## Registrazione

La registrazione per il server Chat persistente e System Center Operations Manager è integrata nella registrazione traccia di Lync Server 2013.

## Vedere anche

#### Ulteriori risorse

[Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md)

