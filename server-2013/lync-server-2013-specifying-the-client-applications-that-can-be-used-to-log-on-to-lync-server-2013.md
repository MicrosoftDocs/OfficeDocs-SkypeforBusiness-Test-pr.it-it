---
title: Specificazione delle applicazioni client utilizzabili per accedere a Lync Server 2013
TOCTitle: Specificazione delle applicazioni client utilizzabili per accedere a Lync Server 2013
ms:assetid: d256a581-9a48-4d1a-82cc-2e1f520d7d2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182591(v=OCS.15)
ms:contentKeyID: 49302064
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Specificazione delle applicazioni client utilizzabili per accedere a Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-12-11_

Lync Server 2013 consente di specificare la versione dei client supportati nell'ambiente. Quando due client che eseguono versioni diverse interagiscono, le funzionalità disponibili per uno dei due client possono essere limitate dalle funzionalità dell'altro client. Per un utilizzo ottimale delle funzionalità incluse in Lync Server 2013 e per migliorare l'esperienza utente globale, è possibile utilizzare il filtro delle versioni client per limitare le versioni client utilizzate nell'ambiente Lync Server 2013. Grazie a tale filtro è inoltre possibile ridurre i costi associati al supporto di più versioni client.

Oltre a creare un criterio globale, è possibile creare criteri di versione client per un determinato servizio o sito o criteri con ambito di utente che possono essere assegnati a singoli utenti. I criteri di versione client con ambito di utente possono essere assegnati a singoli utenti del gruppo **Users** in Pannello di controllo di Lync Server.


> [!NOTE]
> Poiché gli utenti anonimi non sono associati ad alcun utente, sito o servizio, sono interessati solo dai criteri a livello globale.



> [!important]  
> I filtri sono elencati in ordine di priorità. Se ad esempio si dispone di un filtro che consente ai client che eseguono la versione 1.5 di connettersi, seguito da un filtro che blocca i client che eseguono una versione precedente alla 2.0, il primo filtro ha la precedenza e i client che eseguono la versione 1.5 possono connettersi.

## Per modificare i criteri versione client predefiniti

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client**.
    

    > [!NOTE]
    > Per impostazione predefinita, la scheda <STRONG>Criteri versione client</STRONG> è selezionata.



4.  Nella pagina **Criteri versione client** fare doppio clic sul criterio **Globale** nell'elenco.

5.  In **Modifica criteri versione client** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Nuova** per creare una nuova regola versione client.
    
      - Fare clic su uno dei tipi di client definiti nell'elenco e quindi su **Mostra dettagli**.
    

    > [!NOTE]
    > È possibile utilizzare i caratteri jolly per indicare il tipo di client.



6.  In **Agente utente** selezionare un tipo di client.

7.  In **Numero di versione** eseguire le operazioni seguenti:
    
      - In **Versione principale** digitare il numero corrispondente alla versione principale del client.
    
      - In **Versione secondaria** digitare il numero corrispondente alla versione secondaria del client.
    
      - In **Build** digitare il numero corrispondente alla versione principale e secondaria del client.
    
      - In **Aggiornamento** digitare il numero corrispondente alla versione aggiornata del client.
    

    > [!NOTE]
    > È possibile utilizzare i caratteri jolly per indicare il numero di versione client.



8.  Per specificare l'operazione corrispondente per la versione client specificata nei passaggi precedenti, in **Operazione di confronto** fare clic su una delle opzioni seguenti:
    
      - **Corrispondente a**
    
      - **Diverso da**
    
      - **Più recente di**
    
      - **Più recente di o corrispondente a**
    
      - **Meno recente di**
    
      - **Meno recente di o corrispondente a**

9.  Per specificare l'azione da eseguire quando i criteri dei passaggi precedenti vengono soddisfatti, fare clic su una delle opzioni seguenti in **Azione**:
    
      - Per consentire al client di accedere, fare clic su **Consenti**.
    
      - Per consentire al client di eseguire l'accesso e ricevere aggiornamenti da Windows Server Update Service o da Microsoft Update, fare clic su **Consenti e aggiorna**. Questa azione è disponibile solo quando è selezionato l'agente utente **OC**.
        

        > [!NOTE]
        > La selezione di questa azione comporta la visualizzazione di una notifica al successivo accesso degli utenti a Lync 2013. Tale notifica comunica la disponibilità di un aggiornamento, anche se non sono stati ancora rilasciati aggiornamenti per Windows Server Update Service o per Microsoft Update. Per evitare confusione, scegliere questa azione solo dopo che gli aggiornamenti vengono resi disponibili.

    
      - Per consentire al client di accedere e visualizzare un messaggio sulla posizione dalla quale scaricare un'altra versione client, fare clic su **Consenti con URL**. L'URL verrà specificato nelle fasi successive di questa procedura.
    
      - Per impedire al client di accedere, fare clic su **Blocca**.
    
      - Per impedire al client di eseguire l'accesso e consentirgli di ricevere aggiornamenti da Windows Server Update Service o da Microsoft Update, fare clic su **Blocca e aggiorna**. Questa azione è disponibile solo quando è selezionato l'agente utente **OC**.
    
      - Per impedire al client di accedere e visualizzare un messaggio sulla posizione dalla quale scaricare un'altra versione client, fare clic su **Blocca con URL**. L'URL verrà specificato nelle fasi successive di questa procedura.

10. (Facoltativo) Se si è fatto clic su **Consenti con URL** o su **Blocca con URL** al passaggio precedente, digitare l'URL di download del client da includere nel messaggio in **URL**.

11. Fare clic su **OK** e quindi su **Commit**.

## Vedere anche

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

