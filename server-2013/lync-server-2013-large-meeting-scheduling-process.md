---
title: Processo di pianificazione delle riunioni di grandi dimensioni
TOCTitle: Processo di pianificazione delle riunioni di grandi dimensioni
ms:assetid: de267458-885f-4176-a8d7-1a218e67640e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205334(v=OCS.15)
ms:contentKeyID: 49302194
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di pianificazione delle riunioni di grandi dimensioni

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Dato che nel pool dedicato per le riunioni di grandi dimensioni è supportata una sola riunione di grandi dimensioni alla volta, è consigliabile implementare un processo per la pianificazione di questo tipo di riunioni in modo da evitare conflitti. Lo scopo di tale processo di pianificazione è agevolare la configurazione delle riunioni di grandi dimensioni. Questa funzionalità non è disponibile direttamente in Lync Server o nei client di Lync Server. Un metodo per implementare un processo di questo tipo consiste nell'utilizzare il sistema di gestione dei ticket del team di supporto tecnico dell'organizzazione, se disponibile.

Per gli organizzatori di riunioni di grandi dimensioni, la pianificazione include l'esecuzione dei passaggi seguenti:

1.  L'organizzatore della riunione o il delegato stabilisce data e ora, durata e dimensioni di una riunione prossima, oltre all'elenco dei relatori. Se le dimensioni previste per la riunione superano i 250 utenti oppure per assicurare un'esperienza utente ottimale per una riunione con meno di 250 utenti, l'organizzatore o il delegato invia una richiesta per una riunione di grandi dimensioni.

2.  Il personale addetto della pianificazione verifica se la data e l'ora richieste sono disponibili. Dato che nel pool dedicato è supportata una sola riunione di grandi dimensioni alla volta, il personale addetto alla pianificazione deve controllare il calendario di questo tipo di riunioni per stabilire se ne è già presente un'altra pianificata per la data e l'ora richieste. Se l'intervallo di tempo richiesto risulta disponibile, la richiesta di riunione viene approvata.

3.  Se la richiesta viene approvata, il personale addetto alla pianificazione (con le credenziali per il pool dedicato) utilizza il componente aggiuntivo per riunioni online per Lync 2013 con Outlook per impostare una riunione nel pool dedicato. L'URL da utilizzare per partecipare alla riunione viene fornito al richiedente nell'ambito della notifica dell'approvazione.

4.  L'organizzatore della riunione o il delegato utilizza Outlook per pianificare la riunione aggiungendo l'URL per partecipare alla riunione nell'invito. L'organizzatore della riunione o il delegato specifica quindi gli utenti da invitare e invia l'invito alla riunione.
    
    Nella figura seguente sono illustrati una richiesta e un flusso di lavoro di approvazione tipici per la pianificazione di riunioni di grandi dimensioni.
    
    ![Flusso di lavoro per la pianificazione di una conferenza](images/JJ205334.5d8b1f62-1dc3-47bf-bf8f-be2d8899ab9d(OCS.15).jpg "Flusso di lavoro per la pianificazione di una conferenza")

