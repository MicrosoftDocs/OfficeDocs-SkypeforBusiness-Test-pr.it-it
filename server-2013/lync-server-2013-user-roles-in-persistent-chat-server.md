---
title: Ruoli utente nel server chat persistente
TOCTitle: Ruoli utente nel server chat persistente
ms:assetid: 343a0563-9ca5-4ad0-b4f3-a72f1d7f1a81
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ676774(v=OCS.15)
ms:contentKeyID: 49887515
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ruoli utente nel server chat persistente

 

_**Ultima modifica dell'argomento:** 2015-03-19_

Il server Chat persistente introduce il concetto di membri consentiti/non consentiti, che si applica alle categorie di Chat persistente e consente di controllare l'accesso alle chat di una categoria specifica.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il concetto di membri consentiti/non consentiti di una categoria non equivale a quello del ruolo <strong>Membro</strong>, che si applica a una chat di Chat persistente.<br />
Le ricerche visualizzano tutte le chat room aperte e chiuse per le quali l'utente che esegue la ricerca si trova nell'elenco dei membri consentiti/non consentiti. Le chat segrete non vengono visualizzate, a meno che l'utente che esegue la ricerca non ne sia membro. L'utente può eseguire la ricerca solo delle chat di cui è già membro o di quelle per le quali può richiedere l'appartenenza.</td>
</tr>
</tbody>
</table>


L'aspetto principale del concetto di membri consentiti/non consentiti sono gli ethical wall. Ad esempio è frequente negli istituti bancari e finanziari la presenza di vincoli etici che impediscono ai commercianti e agli analisti di condividere le comunicazioni quando implementano criteri e convenzioni. Per ovviare a questo problema, un amministratore può creare le categorie in modo che una categoria consenta la creazione e l'uso delle chat ai commercianti e un'altra agli analisti. Questo vincolo, se progettato nel sistema, non consente di aggiungere un utente come membro della chat se la categoria principale lo impedisce.

Di seguito sono illustrati i tre ruoli utente del server Chat persistente:

  - **Creatore:** utenti dotati delle autorizzazioni necessarie per la creazione di chat room. Tali utenti sono inclusi nell'elenco Creatori di determinate categorie: possono creare chat room in tali categorie, assegnare l'appartenenza in base alla categoria e affidare la gestione delle chat room a responsabili. L'utente che crea una chat room viene aggiunto automaticamente all'elenco dei responsabili della chat.
    

    > [!NOTE]
    > Agli utenti con ruolo di Creatore vengono semplicemente concessi i diritti per la creazione di chat room. La promozione automatica al ruolo di Responsabile consente al Creatore di assegnare appartenenze, specificare responsabili ed eseguire altre operazioni per i servizi chat creati.

    
    Questo ruolo ha lo scopo di controllare chi crea le chat room nell'organizzazione, in particolare se si vuole gestire in modo centralizzato la creazione di chat room per applicare criteri e convenzioni e delegare la gestione delle chat room ad altri utenti dell'organizzazione.

  - **Responsabile:** utenti che gestiscono le proprietà di una chat room. I responsabili delle chat room possono modificare l'elenco dei membri (aggiungere o rimuovere membri) e l'elenco dei responsabili delle chat room (aggiungere e rimuovere responsabili). I responsabili delle chat room possono inoltre aggiungere se stessi all'elenco dei membri o dei relatori (per le chat in modalità auditorium) per poter partecipare alla chat room. Possono inoltre disabilitare le chat room (gli amministratori possono eseguire la ricerca delle chat room disabilitate ed eliminarle in modo permanente). I responsabili possono modificare tutte le proprietà di una chat room, ad eccezione della categoria. Solo l'amministratore di Chat persistente può modificare la categoria dopo la creazione della chat room.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se il responsabile è anche Creatore per un'altra categoria, potrà cambiare la categoria in una categoria per la quale è autorizzato a creare chat.</td>
    </tr>
    </tbody>
    </table>


  - **Membro:** utenti che sono membri di una chat room. Tali utenti possono vedere le chat room (anche se sono segrete) nella directory, sottoscriverle (comprese le opzioni dei metadati quali messaggi non letti, filtri proprio nome e filtri basati sulle parole chiave) e partecipare (possono inserire messaggi, a meno che non si tratti di una chat in modalità auditorium in cui solo i relatori possono inserire messaggi, ottenere contenuto ed effettuare ricerche). Gli utenti che non sono membri della chat room possono cercare la chat room se sono inclusi nell'elenco Membri consentiti della categoria ma, per partecipare alle chat room e accedere al contenuto, devono richiedere l’accesso. Non è prevista la possibilità di effettuare richieste di accesso o di ricevere approvazioni all'interno del sistema. Queste operazioni vengono eseguite esternamente tramite posta elettronica, telefono o altre modalità di contatto).

  - **Relatore:** utenti che possono inserire messaggi in una chat in modalità auditorium.

Di seguito sono indicati i ruoli amministratore per il server Chat persistente:

  - Amministratore di **Chat persistente (CsPersistentChatAdministrator):** si tratta di un nuovo ruolo RBAC (Role-Based Access Control) che consente di amministrare e gestire il server Chat persistente. Gli utenti o i gruppi di sicurezza designati come CsPersistentChatAdministrator possono amministrare il server Chat persistente usando i cmdlet di Windows PowerShell in remoto, ovvero da un computer diverso dal server Chat persistente. Il server Chat persistente verifica che Chat persistente sia membro del gruppo locale Amministratori locali RTC nel Front End Server del server Chat persistente.
    
    Il ruolo CsPersistentChatAdministrator consente di gestire le chat room (modificare tutte le proprietà inclusi l'appartenenza, i responsabili, le categorie e contrassegnare le chat come disabilitate), nonché creare e gestire le categorie di chat room che stabiliscono chi può creare le chat room e chi può accedervi. Gli amministratori possono inoltre contrassegnare le chat room come disabilitate e cancellare le chat room che non sono più attive. Gli amministratori non sono soggetti alle limitazioni previste per i ruoli Creatore o Membri consentiti. Possono infatti creare qualsiasi tipo di chat room e aggiungere se stessi come membro di qualsiasi chat room. Possono inoltre modificare e gestire la configurazione Chat persistente (proprietà del pool, impostazioni globali e configurazione della conformità), nonché pianificare e implementare la migrazione da una distribuzione precedente di Group Chat Server a Lync Server 2013server Chat persistente.

  - **Amministratore Lync:** amministratore generale dell'organizzazione per Lync Server 2013 per la distribuzione.

  - **Operations Manager:** utente responsabile della gestione delle operazioni quotidiane.

  - **Sviluppatori e partner di terze parti:** gli sviluppatori di terze parti estendono il sistema, in particolare offrendo una soluzione di ethical wall per le conversazioni di gruppo, strumenti e supporto per la conformità, client web/mobile e un framework per lo sviluppo dei bot.

