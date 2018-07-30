---
title: 'Lync Server 2013: Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente'
TOCTitle: Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente
ms:assetid: 1e8d5245-cd58-4aad-9a1c-35b24189bc40
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204731(v=OCS.15)
ms:contentKeyID: 49299884
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la sezione **Configurazione di Chat persistente** della pagina **Chat persistente** per configurare le impostazioni di Chat persistente globalmente nel caso siano applicabili a tutti i pool di server Chat persistente o a un pool di server Chat persistente specifico.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per configurare le opzioni di Chat persistente globalmente

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator o CsAdministrator, accedere a un qualsiasi computer nella distribuzione interna.

2.  Fare clic sul pulsante **Start** e scegliere Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).
    
    > [!IMPORTANT]  
    > È inoltre possibile usare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.

3.  Sulla barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Configurazione Chat persistente**.

4.  Nella pagina **Configurazione di Chat persistente** fare clic su **Nuovo** e quindi su **Configurazione sito**.
    
    > [!IMPORTANT]  
    > Scegliere questa opzione per applicare la configurazione all'intero pool di server Chat persistente distribuito nel sito. Fare clic su <strong>Configurazione pool</strong> per applicare la configurazione a un pool di server Chat persistente specifico.

5.  In **Seleziona un sito** selezionare il sito da configurare per la configurazione del sito del server Chat persistente.

6.  In **Nuova configurazione Chat persistente** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per le nuove impostazioni di configurazione. Per impostazione predefinita, il nome del sito esiste già.
    
      - In **Cronologia chat predefinita** definire il numero di messaggi chat che verranno elaborati per ogni chat room alla prima richiesta. Per impostazione predefinita, il numero è 30. Si tratta dell'impostazione globale predefinita e gli amministratori possono disabilitare la cronologia chat per categoria.
        
        > [!IMPORTANT]  
        > Il server Chat persistente memorizzerà nella cache questi messaggi, pertanto se si aumenta il numero verranno memorizzati più messaggi. È sempre possibile accedere al contenuto cronologico in base alla ricerca. Il numero predefinito determina semplicemente il numero massimo di messaggi visualizzati inizialmente alla connessione a una chat room.    
      - In **Dimensioni massime file (KB)** selezionare le dimensioni file massime di ogni cronologia chat. Per impostazione predefinita, il numero è 20 MB (20.000 KB). Si tratta delle dimensioni massime per un file caricabile in qualsiasi chat room nel sistema (per cui i caricamenti sono abilitati attraverso la relativa impostazione **Categoria** ).
        
        > [!IMPORTANT]  
        > Questa impostazione è abilitata nel server per le applicazioni personalizzate o i client Group Chat precedenti che usano Office Communications Server 2007 R2Group Chat Server o Lync Server 2010, Group Chat possono pubblicare file in una chat room. Il client Lync 2013 non dispone della funzionalità di download o caricamento file, pertanto in presenza di una distribuzione di Lync 2013 pura o di un client Lync 2013, non è possibile pubblicare file in una chat room di server Chat persistente.    
      - In **Limite di aggiornamento partecipanti** selezionare il limite per gli aggiornamenti dei partecipanti. server Chat persistente invia le informazioni dell'elenco partecipanti (chi è connesso a una chat room) a tutti i partecipanti finché il numero degli utenti connessi non raggiunge questo numero. Per impostazione predefinita, il numero è 75. Questo limite indica il numero massimo di partecipanti in una determinata chat room oltre a cui il server Chat persistente smette di inviare gli aggiornamenti dell'elenco partecipanti ai client connessi.
    
      - (Facoltativo.) In **URL gestione chat** selezionare l'URL di gestione della chat room. Si tratta dell'URL di una gestione chat room personalizzata basata sul Web. Se non è necessario personalizzare la gestione della chat room e si usa l'impostazione predefinita, non immettere alcun URL. Dopo essere stato impostato, l'URL viene applicato come URL di gestione chat room interna ed esterna.
        
        Se si desidera personalizzare la creazione della chat room e si include il flusso di lavoro aziendale, è possibile creare una soluzione di gestione chat room personalizzata utilizzando il Software Development Kit (SDK) del server Chat persistente , ospitarlo e immettere qui l'URL. Questo URL viene inviato al client in modo che quando un utente tenta di visualizzare o creare una chat room, viene indirizzato alla soluzione di gestione personalizzata.

7.  Fare clic su **Commit** .

## Per configurare le opzioni di Chat persistente per un pool di server Chat persistente specifico

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator o CsAdministrator, accedere a un qualsiasi computer nella distribuzione interna.

2.  Dal menu **Start** selezionare il Pannello di controllo di Lync Server o aprire una finestra del browser, quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).
    
    > [!IMPORTANT]  
    > È inoltre possibile usare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.

3.  Sulla barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Configurazione Chat persistente**.

4.  Nella pagina **Configurazione di Chat persistente** fare clic su **Nuovo** e quindi su **Configurazione pool**.

5.  In **Seleziona una servizio** selezionare il servizio associato al pool di server Chat persistente a configurare.

6.  In **Nuova configurazione Chat persistente** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per le nuove impostazioni di configurazione. Per impostazione predefinita, il nome del pool esiste già.
    
      - In **Cronologia chat predefinita** definire il numero di messaggi chat che verranno elaborati per ogni chat room alla prima richiesta. Per impostazione predefinita, il numero è 30. Si tratta dell'impostazione globale predefinita e gli amministratori possono disabilitare la cronologia chat per categoria.
        
        > [!IMPORTANT]  
        > Il server Chat persistente memorizzerà nella cache questi messaggi, pertanto se si aumenta il numero verranno memorizzati più messaggi. È sempre possibile accedere al contenuto cronologico in base alla ricerca. Il numero predefinito determina semplicemente il numero massimo di messaggi visualizzati inizialmente alla connessione a una chat room.    
      - In **Dimensioni massime file (KB)** selezionare le dimensioni file massime di ogni cronologia chat. Per impostazione predefinita, il numero è 20 MB (20.000 KB). Si tratta delle dimensioni massime per un file caricabile in qualsiasi chat room nel sistema (per cui i caricamenti sono abilitati attraverso la relativa impostazione **Categoria** ).
        
        > [!IMPORTANT]  
        > Questa impostazione è abilitata nel server per le applicazioni personalizzate o i client Group Chat precedenti che usano Office Communications Server 2007 R2Group Chat Server o Lync Server 2010, Group Chat possono pubblicare file in una chat room. Il client Lync 2013 non dispone della funzionalità di download o caricamento file, pertanto in presenza di una distribuzione di Lync 2013 pura o di un client Lync 2013, non è possibile pubblicare file in una chat room di server Chat persistente.    
      - In **Limite di aggiornamento partecipanti** selezionare il limite per gli aggiornamenti dei partecipanti. server Chat persistente invia le informazioni dell'elenco partecipanti (chi è connesso a una chat room) a tutti i partecipanti finché il numero degli utenti connessi non raggiunge questo numero. Per impostazione predefinita, il numero è 75. Questo limite indica il numero massimo di partecipanti in una determinata chat room oltre a cui il server Chat persistente smette di inviare gli aggiornamenti dell'elenco partecipanti ai client connessi.
    
      - In **URL gestione chat** selezionare l'URL di gestione della chat room. Si tratta dell'URL di una distribuzione di gestione chat room basata sul Web. Se non è necessario personalizzare la gestione della chat room e si usa l'impostazione predefinita, non immettere alcun URL.
        
        Se si desidera personalizzare la creazione della chat room e si include il flusso di lavoro aziendale, è possibile creare una soluzione di gestione chat room personalizzata utilizzando il Software Development Kit (SDK) del server Chat persistente , ospitarlo e immettere qui l'URL. Questo URL viene inviato al client in modo che quando un utente tenta di visualizzare o creare una chat room, viene indirizzato alla soluzione di gestione personalizzata.

7.  Fare clic su **Commit** .

