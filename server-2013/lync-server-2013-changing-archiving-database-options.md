---
title: Modifica delle opzioni del database di archiviazione in Lync Server 2013
TOCTitle: Modifica delle opzioni del database di archiviazione in Lync Server 2013
ms:assetid: 3775f09d-65b0-48bc-8a4d-d97bd0c3423c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204814(v=OCS.15)
ms:contentKeyID: 49300175
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica delle opzioni del database di archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Se Archiviazione viene distribuita usando l'archivio SQL Server come archivio di archiviazione degli utenti, è possibile apportare le modifiche seguenti all’archivio di database:

  - Usare un database SQL Server diverso come archivio di archiviazione. Questo database include il database di Archiviazione principale e tutti i database che vengono usati per il mirroring di SQL Server.

  - Passare all'integrazione di Microsoft Exchange per archiviare i file e i dati di archiviazione nei server di Exchange 2013. Se tutti gli utenti sono disponibili nei server di Exchange 2013 e si vuole usare l'archivio di Microsoft Exchange per tutti gli utenti della distribuzione, è necessario rimuovere i database dell'archivio SQL Server dalla topologia.

Per apportare una di queste modifiche, è necessario eseguire il Generatore di topologie, apportare le modifiche, quindi pubblicare nuovamente la topologia. A questo scopo, è possibile usare il Generatore di topologie. Non specificare le informazioni **Archivio SQL Server archiviazione** o **Abilita mirroring dell'archivio SQL Server**, a meno che non siano presenti utenti Lync che non sono disponibili nei server di Exchange 2013.

## Per modificare l'opzione del database di archiviazione

1.  In un computer che esegue Lync Server 2013 o in cui sono installati gli strumenti di amministrazione di Lync Server accedere usando un account che sia membro del gruppo Utenti locale (o un account con diritti utente equivalenti).
    

    > [!NOTE]
    > È possibile definire una topologia usando un account membro del gruppo Utenti locale. Tuttavia per pubblicare una topologia, operazione necessaria per aggiungere un componente alla topologia, è necessario usare un account membro del gruppo <STRONG>Domain Admins</STRONG> e del gruppo <STRONG>RTCUniversalServerAdmins</STRONG> che dispone delle autorizzazioni di controllo completo (ovvero lettura, scrittura e modifica) sulla condivisione file in uso per l'archivio file Lync Server 2013 (ciò significa che il Generatore di topologie può configurare gli elenchi di controllo di accesso discrezionali (DACL) richiesti. In alternativa, è possibile usare un account con diritti equivalenti.



2.  Avviare il Generatore di topologie.

3.  Nell'albero della console accedere al pool Front End in cui è stata distribuita Archiviazione e fare clic sul nome del pool Front End in cui si vuole modificare le opzioni di database.

4.  Nel menu **Azione** fare clic su **Modifica proprietà**.

5.  Nella finestra di dialogo **Modifica proprietà** fare clic su **Generale**.

6.  Scorrere verso il basso fino ad **Archiviazione**.

7.  In **Archiviazione** seguire questa procedura:
    
      - Per passare a un archivio SQL Server esistente diverso, nella casella di riepilogo a discesa in **Archivio SQL Server archiviazione** seguire la procedura seguente:
        
          - Per usare un archivio SQL Server esistente, nella casella di riepilogo a discesa fare clic sul nome dell'archivio SQL Server che si vuole usare.
        
          - Per specificare un nuovo archivio SQL Server, fare clic su **Nuovo**, quindi nella finestra di dialogo **Definire un nuovo archivio SQL Server** seguire questa procedura:
            
              - Per usare un archivio SQL Server esistente, nella casella di riepilogo a discesa fare clic sul nome dell'archivio SQL Server che si vuole usare.
            
              - Per specificare un nuovo archivio SQL Server, fare clic su **Nuovo**, quindi nella finestra di dialogo **Definire un nuovo archivio SQL Server** seguire questa procedura:
                
                  - In **FQDN SQL Server** specificare l'FQDN del server in cui si vuole creare il nuovo archivio SQL Server.
                
                  - Fare clic su **Istanza predefinita** per usare l'istanza predefinita oppure su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza che si vuole usare.
                
                  - Se l'istanza di SQL Server specificata si trova in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring**, quindi in **Numero porta di mirroring** specificare il numero di porta.
    
      - Per aggiungere l'archivio SQL Server per il mirroring o passare a un archivio SQL Server esistente diverso per il mirroring dell'archivio SQL Server, selezionare **Abilita mirroring dell'archivio SQL Server**, quindi procedere come segue:
        
          - Per usare un archivio SQL Server esistente per il mirroring, nella casella di riepilogo discesa **Mirror archivio SQL Server archiviazione** fare clic sul nome dell'archivio SQL Server che si vuole usare per il mirroring.
        
          - Per specificare un nuovo archivio SQL Server per il mirroring, fare clic su **Nuovo**, quindi nella finestra di dialogo **Definire un nuovo archivio SQL Server** seguire una delle procedure seguenti:
            
            1.  In **FQDN SQL Server** specificare l'FQDN del server SQL Server in cui si vuole creare il nuovo archivio SQL Server.
            
            2.  Fare clic su **Istanza predefinita** per usare l'istanza predefinita oppure su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza che si vuole usare.
            
            3.  Se l'istanza di SQL Server specificata si trova in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring**, quindi in **Numero porta di mirroring** specificare il numero di porta.
        
          - Se si abilita il mirroring di SQL Server e si vuole aggiungere o modificare un controllo del mirroring di SQL Server (una terza istanza di SQL Server separata in grado di rilevare lo stato del server SQL Server principale e di eseguire il mirroring delle istanze), selezionare la casella di controllo **Usa controllo del mirroring di SQL Server per abilitare il failover automatico**, quindi seguire una delle procedure seguenti:
            
            1.  In **FQDN SQL Server** specificare l'FQDN del server in cui si vuole creare il nuovo controllo del mirroring di SQL Server.
            
            2.  Fare clic su **Istanza predefinita** per usare l'istanza predefinita oppure su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza che si vuole usare per il controllo di mirroring.
            
            3.  Se l'istanza di SQL Server specificata si trova in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring**, quindi in **Numero porta di mirroring** specificare il numero di porta.
    
      - Per passare all'integrazione di Microsoft Exchange per archiviare i file e i dati di archiviazione nei server di Exchange 2013 (se tutti gli utenti della distribuzione sono disponibili nei server di Exchange 2013), eliminare tutte le informazioni relative ai database di Archiviazione.
    
    > [!important]  
    > Se sono presenti utenti Lync non disponibili nei server di Exchange 2013, non eliminare le informazioni dell'archivio SQL Server.

8.  Per salvare la configurazione, fare clic su **OK**.
    
    > [!important]  
    > Le modifiche apportate nel Generatore di topologie diventano effettive solo dopo la pubblicazione della nuova topologia. Per informazioni dettagliate, vedere <a href="lync-server-2013-publishing-the-updated-topology-to-add-archiving-databases.md">Pubblicazione della topologia aggiornata per l'aggiunta dei database di archiviazione</a> nella documentazione relativa alla distribuzione.
