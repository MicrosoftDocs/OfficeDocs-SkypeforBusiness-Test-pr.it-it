---
title: Creare o modificare una nuova regola dei criteri delle versioni client
TOCTitle: Creare o modificare una nuova regola dei criteri delle versioni client
ms:assetid: 6f879d99-8401-41e0-a562-195c890d63ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898478(v=OCS.15)
ms:contentKeyID: 52062184
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una nuova regola dei criteri delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-01-21_

Le regole dei criteri delle versioni client definiscono le azioni che dovrebbero essere eseguite quando gli utenti tentano di eseguire l'accesso con specifici client o versioni client. È possibile creare o modificare singole regole per un set di criteri delle versioni client dal Pannello di controllo di Lync Server 2013.

> [!IMPORTANT]  
> Le regole sono elencate in ordine di priorità. Se ad esempio si dispone di una regola che consente ai client che eseguono la versione 1.5 di connettersi, seguita da una regola che blocca i client che eseguono una versione precedente alla 2.0, la prima regola ha la precedenza e i client che eseguono la versione 1.5 possono connettersi.

## Per creare o modificare le regole dei criteri delle versioni client con il Pannello di controllo di Lync Server

1.  [Creare o modificare un nuovo criterio delle versioni client](lync-server-2013-create-or-modify-a-new-client-version-policy.md) con il Pannello di controllo di Lync Server.

2.  Nella pagina **Modifica criteri versione client** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Nuova** per creare una nuova regola versione client.
    
      - Fare clic su uno dei tipi di client definiti nell'elenco e quindi su **Mostra dettagli**.
    

    > [!NOTE]
    > È possibile utilizzare i caratteri jolly per indicare il tipo di client.



3.  In **Agente utente** selezionare un tipo di client.

4.  In **Numero di versione** eseguire le operazioni seguenti:
    
      - In **Versione principale** digitare il numero corrispondente alla versione principale del client.
    
      - In **Versione secondaria** digitare il numero corrispondente alla versione secondaria del client.
    
      - In **Build** digitare il numero corrispondente alla versione principale e secondaria del client.
    
      - In **Aggiornamento** digitare il numero corrispondente alla versione aggiornata del client.
    

    > [!NOTE]
    > È possibile utilizzare i caratteri jolly per indicare il numero di versione client.



5.  Per specificare l'operazione corrispondente per la versione client specificata nei passaggi precedenti, in **Operazione di confronto** fare clic su una delle opzioni seguenti:
    
      - **Corrispondente a**
    
      - **Diverso da**
    
      - **Più recente di**
    
      - **Più recente di o corrispondente a**
    
      - **Meno recente di**
    
      - **Meno recente di o corrispondente a**

6.  Per specificare l'azione da eseguire quando i criteri dei passaggi precedenti vengono soddisfatti, fare clic su una delle opzioni seguenti in **Azione**:
    
      - Per consentire al client di accedere, fare clic su **Consenti**.
    
      - Per consentire al client di eseguire l'accesso e ricevere aggiornamenti da Windows Server Update Service o da Microsoft Update, fare clic su **Consenti e aggiorna**. Questa azione è disponibile solo quando è selezionato l'agente utente **OC**.
        

        > [!NOTE]
        > La selezione di questa azione comporta la visualizzazione di una notifica al successivo accesso degli utenti a Lync 2013. Tale notifica comunica la disponibilità di un aggiornamento, anche se non sono stati ancora rilasciati aggiornamenti per Windows Server Update Service o per Microsoft Update. Per evitare confusione, scegliere questa azione solo dopo che gli aggiornamenti vengono resi disponibili.

    
      - Per consentire al client di accedere e visualizzare un messaggio sulla posizione nella quale scaricare un'altra versione client, fare clic su **Consenti con URL**. L'URL verrà specificato più avanti in questa procedura.
    
      - Per impedire al client di accedere, fare clic su **Blocca**.
    
      - Per impedire al client di eseguire l'accesso e consentirgli di ricevere aggiornamenti da Windows Server Update Service o da Microsoft Update, fare clic su **Blocca e aggiorna**. Questa azione è disponibile solo quando è selezionato l'agente utente **OC**.
    
      - Per impedire al client di accedere e visualizzare un messaggio sulla posizione dalla quale scaricare un'altra versione client, fare clic su **Blocca con URL**. L'URL verrà specificato più avanti in questa procedura.

7.  (Facoltativo) Se si seleziona **Consenti con URL** o su **Blocca con URL** nel passaggio precedente, digitare l'URL di download del client da includere nel messaggio in **URL**.

8.  Fare clic su **OK** e quindi su **Commit**.

