---
title: "Lync Server 2013: Definizione dei requisiti dell'organizzazione per il server Chat persistente"
TOCTitle: Definizione dei requisiti dell'organizzazione per il server Chat persistente
ms:assetid: 568674fb-c08a-4170-ac38-e2f8428c69e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398372(v=OCS.15)
ms:contentKeyID: 49300616
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti dell'organizzazione per il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-15_

Prima di distribuire un server Chat persistente per l'organizzazione, per ottimizzare la distribuzione è fondamentale considerare le domande chiave seguenti:

  - Chi (profili utente) deve essere abilitato per il server Chat persistente? Il server Chat persistente viene abilitato da criteri che possono essere impostati a livello globale, di sito, di pool o di utente.

  - Quanti utenti (scala) devono essere abilitati per il server Chat persistente? Il server Chat persistente supporta 150.000 utenti di cui è stato eseguito il provisioning (abilitati tramite criteri) e un massimo di 80.000 utenti del server Chat persistente simultanei. Un unico server Chat persistente può supportare 20.000 utenti e un unico pool di server Chat persistente può avere fino a quattro server attivi, per un totale di 80.000 utenti connessi simultaneamente.

  - Si intende eseguire la migrazione da una versione precedente di Group Chat Server o distribuire il server Chat persistente per la prima volta?

  - Ci sono requisiti di conformità da rispettare? Il server Chat persistente supporta la conformità. Il servizio Conformità viene eseguito nel Front End Server del server Chat persistente, mentre in precedenza per la distribuzione di Group Chat Server era richiesto un computer separato. La conformità è facoltativa e, se scelta, richiede un database di conformità che deve essere configurato per l'archiviazione di dati ed eventi di conformità. È necessario anche configurare una scheda che riceva i dati dal database di conformità e li converta in un altro formato, ad esempio in file XML o in archivi ospitati da Exchange.

  - In che modo si vogliono controllare ambiti, limiti etici e accesso? È possibile definire **Categorie** per definire i limiti e scegliere gli utenti a cui è consentito trovarsi nelle chat create in ognuna di queste categorie.

  - In che modo si vuole controllare chi può creare chat? È possibile configurare **Creatori**, appropriati a seconda della categoria, che possono creare chat. I creatori possono impostare altri membri come **Responsabili di chat room** per la gestione ordinaria delle chat (aggiunta o rimozione di membri), in base all'ambito dei **Membri consentiti/Membri non consentiti** configurati dalla categoria.

  - In che modo si vogliono creare le chat? Il server Chat persistente offre una funzionalità basata sul Web per la creazione e la gestione delle chat. Questa funzionalità può essere avviata dal client Lync 2013. È possibile scegliere di definire una soluzione personalizzata (usando server Chat persistente Software Development Kit (SDK)) in cui implementare i requisiti e i flussi di lavoro aziendali, e configurare il server Chat persistente in modo da indirizzare gli utenti a tale soluzione.

  - Di che tipo di componenti aggiuntivi si vuole effettuare il provisioning? I **componenti aggiuntivi** rendono più efficiente l'uso delle chat, sfruttando il riquadro di estensibilità del client Lync 2013 per fornire contesto pertinente alla chat. È possibile scegliere i componenti aggiuntivi generici che si ritengono più utili, ad esempio il sito Web aziendale, i documenti di collaborazione interni e così via. I responsabili di chat room, se vogliono, possono scegliere uno dei componenti aggiuntivi registrati e associarlo alla propria chat.

  - Quali sono i requisiti di disponibilità elevata e di ripristino di emergenza? Il server Chat persistente supporta il mirroring SQL Server e il clustering SQL Server per la disponibilità elevata e fino a otto server (quattro attivi e quattro in standby) in un pool esteso con log shipping SQL Server per il ripristino di emergenza.

  - Ci sono requisiti normativi da rispettare? Se la società si trova in un paese o in un'area geografica in cui i dati devono essere conservati all'interno del paese, potrebbe essere necessario distribuire più pool di server Chat persistente, uno per ciascuna area geografica specifica. Le chat room, le categorie e i componenti aggiuntivi non si estendono su più pool, ma appartengono a un solo pool di server Chat persistente. È possibile gestire l'insieme di categorie, componenti aggiuntivi e chat room per ogni pool di server Chat persistente. È possibile configurare gli utenti in modo che possano accedere alle chat room di uno o più pool, utilizzando l'ambito AllowedMembers della categoria o l'ambito dei membri della chat room, a seconda di come sono progettate le categorie.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Più pool di server Chat persistente non implicano una scala maggiore: in tutti i pool di server Chat persistente sono ancora possibili solo 80.000 utenti connessi simultaneamente. Il motivo principale per cui vengono supportati più pool di server Chat persistente è supportare i problemi legati alla regolamentazione.</td>
    </tr>
    </tbody>
    </table>

