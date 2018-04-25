---
title: Pianificazione dei dettagli
TOCTitle: Pianificazione dei dettagli
ms:assetid: 39ca6fff-2c15-4347-9f1f-6c8687a39a49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204823(v=OCS.15)
ms:contentKeyID: 49300235
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dei dettagli

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Dopo avere verificato che nel periodo di tempo richiesto non sono pianificate altre riunioni, il personale di supporto delle riunioni di grandi dimensioni che gestisce le richieste pianifica la riunione nel pool di riunioni di grandi dimensioni. Questa attività viene eseguita nel componente aggiuntivo per riunioni online per Lync, installato insieme al client Lync Server 2013, usando le credenziali di un utente abilitato per Lync Server nel pool di riunioni di grandi dimensioni dedicato.

Per assicurare la migliore esperienza utente, è importante pianificare la riunione di grandi dimensioni con i livelli di diritto di accesso appropriati e impostazioni delle riunioni specifiche per le esigenze dell'organizzatore. È consigliabile configurare le impostazioni di pianificazione seguenti in Opzioni Riunione Lync:

  - Usare una nuova area riunioni per ciascuna riunione di grandi dimensioni anziché riutilizzare l'area riunione dedicata.

  - Specificare il livello di accesso alla riunione come segue:
    
      - Se almeno un invitato è esterno all'organizzazione, impostare il tipo di accesso alla riunione su **Tutti gli utenti (senza restrizioni)**. Ciò consente di evitare di dover gestire una sala d'attesa di dimensioni potenzialmente grandi quando la riunione è in corso.
    
      - Se la riunione prevede solo partecipanti interni, impostare il tipo di accesso su **Tutti gli utenti dell'organizzazione**.
        

        > [!NOTE]
        > Evitare di impostare il tipo di accesso alla riunione su <STRONG>Persone invitate appartenenti alla società</STRONG> perché questa impostazione costringe gli organizzatori ad aggiungere all'elenco degli invitati tutti gli indirizzi di posta elettronica degli utenti e non è possibile invitare un gruppo di distribuzione.<BR>Evitare di impostare il tipo di accesso alla riunione su <STRONG>Solo io, l'organizzatore della riunione</STRONG> perché questa impostazione richiede che ciascun partecipante, inclusi i relatori, stiano in sala d'attesa durante l'esecuzione della riunione. La persona responsabile della riunione di grandi dimensioni deve quindi costantemente monitorare l'elenco della sala d'attesa e ammettere i nuovi utenti che si trovano in sala d'attesa.



  - Selezionare l'opzione **Consenti ai chiamanti di entrare direttamente** per consentire agli utenti che accedono dall'esterno mediante chiamata telefonica di accedere alla riunione automaticamente.

  - Invitare esplicitamente gli utenti seguenti:
    
      - Organizzatore della riunione e delegato (richiedente)
    
      - L'elenco dei relatori fornito da un richiedente della riunione
    

    > [!NOTE]
    > Se il tipo di accesso alla riunione è impostato su <STRONG>Persone scelte dall'utente</STRONG>, è necessario aggiungere esplicitamente come invitato ciascun partecipante di una riunione di grandi dimensioni.



  - Gestire esplicitamente i relatori anziché impostare l'opzione su uno dei valori di promozione automatica. Assicurarsi di aggiungere gli utenti seguenti come relatori:
    
      - Organizzatore della riunione e delegato (richiedente)
    
      - L'elenco dei relatori fornito dai richiedenti di riunioni di grandi dimensioni
    

    > [!NOTE]
    > Grazie alla gestione esplicita dei relatori, è possibile controllare il numero di relatori limitandolo alla quantità necessaria per rendere possibile la realizzazione di una riunione di grandi dimensioni efficace. Se la maggioranza dei partecipanti alla riunione dispone del ruolo di partecipante, si riducono le probabilità che i partecipanti assumano per errore il controllo della presentazione, eliminino una presentazione di PowerPoint, disattivino/attivino l'audio dei relatori o siano causa di altre interruzioni della riunione.



  - Selezionare l'impostazione **Disattiva l'audio di tutti i partecipanti** per fare in modo che durante la riunione venga trasmesso solo l'audio dei relatori.

  - Selezionare l'impostazione **Blocca video partecipanti** per fare in modo che durante la riunione venga trasmesso solo il video dei relatori.

Nella figura che segue sono mostrate le impostazioni consigliate per il componente aggiuntivo per riunioni online per Lync.

![Opzioni per le riunioni in conferenza](images/JJ204823.54e4e70d-06b0-45cd-8d94-bab649cd5dc0(OCS.15).jpg "Opzioni per le riunioni in conferenza")

