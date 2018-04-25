---
title: Utilizzo di categorie per l'amministrazione del server Chat persistente
TOCTitle: Utilizzo di categorie per l'amministrazione del server Chat persistente
ms:assetid: dfcb3ad1-da90-467e-b08c-f4e68673b7b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398988(v=OCS.15)
ms:contentKeyID: 49302221
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di categorie per l'amministrazione del server Chat persistente

 

_**Ultima modifica dell'argomento:** 2013-10-01_

La distribuzione di server Chat persistente può ospitare molte chat di Chat persistente contemporaneamente. Le chat room possono essere organizzate in un set di categorie nel server. Ogni chat room appartiene a una sola categoria ed eredita alcune impostazioni da tale categoria. In questo modo viene creata una struttura utile per identificare le conversazioni in base alle esigenze aziendali e per facilitare l'amministrazione delegata e la gestione semplificata.


> [!NOTE]
> Anche se nei computer che eseguono Chat persistente sono disponibili molte funzionalità di gestione delle chat room (client Lync) per l'utente, gli amministratori di Chat persistente (con il ruolo <STRONG>cspersistentchatadministrator</STRONG>) devono utilizzare il Pannello di controllo di Lync Server o i cmdlet di Windows PowerShell per creare o gestire le categorie.



Gli amministratori di Chat persistente utilizzano il Pannello di controllo di Lync Server o i cmdlet di Windows PowerShell per creare e gestire le categorie, nonché per progettare l'accesso per le chat room per gli utenti nella loro organizzazione.

I responsabili della gestione delle chat room Chat persistente, che hanno la possibilità di gestire una o più chat room, possono utilizzare il client Lync per avviare un'applicazione Web di gestione delle chat room per creare e gestire le chat room oppure i clienti possono creare soluzioni personalizzate e flussi di lavoro da richiamare. Gli amministratori di Chat persistente possono inoltre utilizzare il Pannello di controllo di Lync Server o i cmdlet Windows PowerShell per creare e gestire le chat room.


> [!NOTE]
> Una chat room di Chat persistente non può avere lo stesso nome di una categoria di Chat persistente.



I responsabili delle chat room possono apportare modifiche a tutte le proprietà delle chat room, con l'eccezione della modifica della categoria. Non è possibile impedire loro di eseguire le azioni seguenti:

  - Disabilitare una chat room

  - Modificare il nome di una chat room

  - Modificare la descrizione di una chat room

  - Modificare il tipo di chat room (auditorium o normale)

  - Modificare la privacy di una chat room (aperta, chiusa o segreta)

  - Aggiungere o rimuovere membri

  - Aggiungere o rimuovere responsabili di chat room

  - Aggiungere o rimuovere componenti aggiuntivi

  - Modificare impostazioni come gli inviti (a seconda di quanto consentito dalla categoria)

## Amministrazione delegata

La creazione e gestione di chat room Chat persistente è molto più semplice con l'utilizzo corretto delle categorie. Un amministratore di Chat persistente può definire **AllowedMembers** e **Creators** per ogni categoria, nonché definire le impostazioni e i comportamenti predefiniti che verranno applicati a tutte le chat room create nella categoria. Gli amministratori di Chat persistente creano e gestiscono le categorie tramite il Pannello di controllo di Lync Server o cmdlet di Windows PowerShell.

Gli utenti, le unità organizzative e i gruppi di utenti identificati come creatori della categoria sono gli unici autorizzati a creare chat room nella categoria. Dopo la creazione della categoria, essi potranno scegliere utenti, unità organizzative e gruppi di utenti dall'elenco **AllowedMembers** della categoria come responsabili di chat room e membri per la gestione e la partecipazione.

Le chat room create in una categoria sono soggette ai criteri e alle impostazioni applicati dalla categoria, ad esempio i membri autorizzati, gli utenti che possono gestire la chat room, se sono consentiti caricamenti di file, se è previsto l'invio di inviti e così via.

