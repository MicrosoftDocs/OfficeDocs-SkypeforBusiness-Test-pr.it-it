---
title: 'Lync Server 2013: Ruoli del server'
TOCTitle: Ruoli del server
ms:assetid: 7137fc06-fca2-4e5f-9db5-10c7c29a788c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398536(v=OCS.15)
ms:contentKeyID: 49300936
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ruoli del server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

Ogni server che esegue Lync Server esegue uno o più *ruoli del server* . Un ruolo del server è un insieme definito di funzionalità di Lync Server rese disponibili da tale server. Non è necessario distribuire nella rete tutti i ruoli del server disponibili. Installare solo i ruoli del server che contengono le funzionalità desiderate.

Anche se non si ha familiarità con i ruoli del server in Lync Server, Strumento di pianificazione può offrire indicazioni riguardo alla soluzione migliore per i server che è necessario distribuire, in base alle caratteristiche desiderate. Questa sezione contiene una breve panoramica dei ruoli del server e delle caratteristiche generali che offrono:

  - Server Standard Edition

  - Front End Server e server back-end

  - server perimetrale

  - Mediation Server

  - Server Director

  - Front End Server Chat persistente

  - Archivio di Chat persistente (server back-end di Chat persistente)

  - Archivio di Conformità chat persistente (server back-end di Conformità chat persistente)

Per la maggior parte dei ruoli del server, ai fini di scalabilità e disponibilità elevata è possibile distribuire *pool* di più server che eseguono tutti lo stesso ruolo del server. Ogni server in un pool deve eseguire uno o più ruoli del server identici. Per alcuni tipi di pool in Lync Server, è necessario distribuire un servizio di bilanciamento del carico per suddividere il traffico tra i diversi server nel pool. Lync Server supporta sia il bilanciamento del carico hardware che il bilanciamento del carico DNS (Domain Name System).

## Server Standard Edition

Il server Standard Edition è progettato per piccole imprese e per progetti pilota di grandi imprese. Consente l'esecuzione di molte delle caratteristiche di Lync Server, inclusi i database necessari, in un singolo server. Questo server offre funzionalità di Lync Server a un costo inferiore, ma non offre un'effettiva soluzione a disponibilità elevata.

Il server Standard Edition consente di utilizzare messaggistica istantanea, presenza, conferenze e VoIP aziendale, eseguiti tutti in un unico server.

Per una soluzione a disponibilità elevata, utilizzare Lync Server Enterprise Edition.

## Front End Server e server back-end

In Lync Server Enterprise Edition, Front End Server è il ruolo del server di base ed esegue molte funzioni di base di Lync Server. Front End Server, insieme ai server back-end che forniscono il database, è l'unico ruolo del server che deve essere presente in qualsiasi distribuzione di Lync Server Enterprise Edition.

Un *pool Front End* è un insieme di server Front End Server, configurati in modo identico, che funzionano insieme per offrire servizi per un gruppo comune di utenti. Un pool di server multipli che eseguono lo stesso ruolo garantisce funzionalità di scalabilità e failover.

Front End Server include le funzionalità seguenti:

  - Autenticazione utente e registrazione utenti

  - Scambio di informazioni sulla presenza e schede contatto

  - Espansione dei servizi Rubrica e delle liste di distribuzione

  - Funzionalità di messaggistica istantanea, incluse conferenze di messaggistica istantanea con più partecipanti

  - Web conferencing, conferenza PSTN con accesso esterno e conferenza A/V (se distribuita)

  - Hosting di applicazioni, sia per applicazioni incluse in Lync Server, ad esempio Operatore Conferenza e applicazione Response Group, sia per applicazioni di terze parti

  - Facoltativamente, il monitoraggio, per raccogliere informazioni sull'utilizzo informazioni in forma di registrazione dettagli chiamata (CDR) e registrazione errori di chiamata. Queste informazioni forniscono metriche sulla qualità dei supporti multimediali (audio e video) che attraversano la rete, per chiamate e conferenze A/V di VoIP aziendale.

  - Componenti Web per il supporto di attività basate sul Web come Utilità di pianificazione Web e Join Launcher.

  - Facoltativamente, l'archiviazione consente di archiviare le comunicazioni di messaggistica istantanea e il contenuto delle riunioni per motivi di conformità. Per informazioni dettagliate, vedere [Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md) nella documentazione relativa alla pianificazione.
    
    In Lync Server 2010 e nelle versioni precedenti, monitoraggio e archiviazione sono ruoli server distinti, non collocati sul Front End Server.

  - Facoltativamente, se la chat persistente è abilitata, Servizi Web della chat persistente per la gestione delle chat room e Servizi Web della chat persistente per l'upload e il download dei file.

I Front End Pool rappresentano inoltre il principale percorso di archiviazione per i dati di utenti e conferenze. Le informazioni relative a ciascun utente sono replicate tra i tre Front End Server nel pool, e il backup è eseguito nei server back-end.

Un pool Front End nella distribuzione esegue anche il *server di gestione centrale* , che gestisce e distribuisce dati di configurazione di base in tutti i server che eseguono Lync Server. server di gestione centrale offre inoltre Lync Server Management Shell e funzionalità di trasferimento file.

I server back-end sono server di database che eseguono Microsoft SQL Server, che fornisce servizi di database per il pool Front End. I server back-end assumono il ruolo di archivi per il back up dei dati utente e di conferenza del pool, e rappresentano gli archivi principali per altri database, tra cui il database dei Response Group. È possibile che sia presente un solo server back-end, ma per il failover è consigliabile una soluzione che utilizzi il mirroring di SQL Server. Nei server back-end non viene eseguito alcun software Lync Server.

> [!important]  
> È consigliabile collocare i database di Lync Server in un percorso diverso rispetto agli altri database. In caso contrario, disponibilità e prestazioni potrebbero risentirne.

Le informazioni archiviate nei database del server back-end includono informazioni sulla presenza, elenchi di contatti degli utenti, dati sulle conferenze, ad esempio dati persistenti sullo stato di tutte le conferenze correnti, e dati di pianificazione delle conferenze.

## server perimetrale

Il server perimetrale consente agli utenti di comunicare e collaborare con utenti che si trovano all'esterno dei firewall dell'organizzazione. Questi utenti esterni possono comprendere gli utenti stessi dell'organizzazione impegnati fuori sede, utenti di organizzazioni partner federate e utenti esterni invitati a partecipare a conferenze ospitate nella distribuzione di Lync Server. Il server perimetrale consente inoltre servizi di connettività di messaggistica istantanea pubblica come Windows Live, AOL, Yahoo\! e Google Talk.

> [!important]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


La distribuzione del server perimetrale attiva inoltre i servizi di mobilità, che supportano le funzionalità di Lync nei dispositivi mobili. Gli utenti possono utilizzare dispositivi mobili Apple iOS, Android, Windows Phone o Nokia supportati per eseguire attività quali l'invio e la ricezione di messaggi istantanei, la visualizzazione dei contatti e la visualizzazione della presenza. I dispositivi mobili inoltre supportano alcune funzionalità VoIP aziendale tra cui la possibilità di partecipare a una conferenza mediante clic del mouse, la chiamata tramite ufficio, il numero unico, la segreteria telefonica e le chiamate senza risposta. La funzionalità per dispositivi mobili inoltre supporta le *notifiche push* per i dispositivi mobili che non supportano le applicazioni eseguite in background. Una notifica push è una notifica inviata a un dispositivo mobile relativamente a un evento che si verifica mentre un'applicazione per dispositivi mobili non è attiva.

I server perimetrali includono inoltre un proxy XMPP (Extensible Messaging and Presence Protocol) pienamente integrato, con gateway XMPP incluso sui Front End Server. È possibile configurare questi componenti XMPP per abilitare gli utenti di Lync Server 2013 all'aggiunta di contatti da partner basati su XMPP (ad esempio, Google Talk) e constire l'utilizzo di messaggistica istantanea e presenza.

Per informazioni dettagliate, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) nella documentazione relativa alla pianificazione.

## Mediation Server

Mediation Server è un componente necessario per l'implementazione di VoIP aziendale e conferenze telefoniche con accesso esterno. Mediation Server traduce i segnali e, in alcune configurazioni, i contenuti multimediali tra l'infrastruttura interna di Lync Server interna e un gateway PSTN (Public Switched Telephone Network), IP-PBX o trunk SIP (Session Initiation Protocol). È possibile eseguire Mediation Server collocato sullo stesso server del Front End Server, o separato in un pool Mediation Server indipendente.

Per informazioni dettagliate, vedere [Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md) nella documentazione relativa alla pianificazione.

## Server Director

I server Director possono autenticare le richieste degli utenti di Lync Server, ma non possono includere account utente, né fornire servizi di presenza o di conferenza. I server Director sono particolarmente utili per potenziare la protezione nelle distribuzioni che consentono l'accesso utente esterno, in cui possono autenticare le richieste prima di inviarle in server interni. In caso di attacchi Denial of Service (DoS), gli attacchi terminano al Director e non raggiungono i Front End Server. Per informazioni dettagliate, vedere [Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md) nella documentazione relativa alla pianificazione.

## Ruoli server Chat persistente

Chat persistente consente di partecipare a conversazioni tra più partecipanti basate su argomenti, e permanenti nel tempo. I servizi di Chat persistente sono eseguiti dal Front End Server di Chat persistente. Il server back-end di Chat persistente salva i dati della cronologia delle chat e le informazioni relative a categorie e chat room. Il server back-end di Conformità chat persistente, facoltativo, può archiviare il contenuto della chat e gli eventi di conformità ai fini della conformità stessa.

I server che eseguono Lync ServerStandard Edition sono inoltre in grado di eseguire Chat persistente collocata sullo stesso server. Non è possibile collocare il Front End Server di Chat persistente con Enterprise EditionFront End Server.

Per informazioni dettagliate, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md).

## Vedere anche

#### Concetti

[Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md)  

#### Ulteriori risorse

[Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md)  
[Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md)  
[Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md)  
[Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md)

