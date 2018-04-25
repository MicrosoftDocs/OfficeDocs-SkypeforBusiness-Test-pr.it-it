---
title: Aggiunta di database di archiviazione alla topologia di Lync Server 2013
TOCTitle: Aggiunta di database di archiviazione alla topologia di Lync Server 2013
ms:assetid: 089ab32f-1167-4bb8-a283-fdc6c9613072
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204654(v=OCS.15)
ms:contentKeyID: 49299602
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiunta di database di archiviazione alla topologia di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Prima di poter configurare la distribuzione per il supporto dell'archiviazione è necessario incorporare l'archiviazione nella topologia. In questo argomento viene illustrato come utilizzare il Generatore di topologie per aggiungere l'archiviazione alla topologia esistente.


> [!NOTE]
> Se si vuole utilizzare l'integrazione di Microsoft Exchange per archiviare i dati e i file di archiviazione nei server di Exchange 2013 per tutti gli utenti nella distribuzione, non specificare le informazioni <STRONG>Archivio SQL Server archiviazione</STRONG> o <STRONG>Abilita mirroring dell'archivio SQL Server</STRONG>.



## Per aggiungere il supporto del database di archiviazione alla topologia

1.  In un computer che esegue Lync Server 2013 o in cui sono installati gli strumenti di amministrazione di Lync Server, eseguire l'accesso con un account membro del gruppo Users locale o un account con diritti utente equivalenti.
    

    > [!NOTE]
    > È possibile definire una topologia utilizzando un account membro del gruppo Users locale, ma per pubblicare una topologia, operazione necessaria per aggiungere un server alla topologia, è necessario utilizzare un account membro del gruppo <STRONG>Domain Admins</STRONG> e del gruppo <STRONG>RTCUniversalServerAdmins</STRONG> e con autorizzazioni di controllo completo (ovvero, lettura, scrittura e modifica) per la condivisione file utilizzata per l'archivio file di Lync Server 2013, in modo che il Generatore di topologie possa configurare gli elenchi di controllo di accesso discrezionale necessari oppure un account con diritti utente equivalenti.



2.  Avviare il Generatore di topologie.

3.  Nell'albero della console, passare al pool Front End in cui si vuole distribuire l'archiviazione, quindi fare clic sul nome del pool Front End desiderato.

4.  Scegliere **Modifica proprietà** dal menu **Azione**.

5.  Nella finestra di dialogo **Modifica proprietà** fare clic su **Generale**.

6.  Scorrere verso il basso fino ad **Archiviazione**.

7.  Selezionare la casella di controllo **Archiviazione**.

8.  In **Archivio SQL Server archiviazione** eseguire una delle operazioni seguenti:
    
      - Per utilizzare un archivio SQL Server esistente, nell'elenco a discesa fare clic sul nome dell'archivio SQL Server da utilizzare. Se tutti gli utenti sono ospitati in Microsoft Exchange Server 2013 o versione superiore, è possibile archiviare le comunicazioni Lync di tutti gli utenti in Exchange. In questo caso non è necessario configurare l'archivio di archiviazione SQL Server.
    
      - Per specificare un nuovo archivio SQL Server, fare clic su **Nuovo** e quindi nella finestra di dialogo **Definire un nuovo archivio SQL Server** eseguire le operazioni seguenti:
        
          - In **FQDN SQL Server** specificare il nome di dominio completo del server in cui si vuole creare il nuovo archivio SQL Server.
        
          - Fare clic su **Istanza predefinita** per utilizzare l'istanza predefinita oppure fare clic su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza da utilizzare.
        
          - Se l'istanza di SQL Server specificata è in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring** e quindi specificare il numero di porta in **Numero porta di mirroring**.

9.  Se si vuole utilizzare il mirroring dell'archivio SQL Server, selezionare **Abilita mirroring dell'archivio SQL Server** e quindi eseguire le operazioni seguenti:
    
      - Per utilizzare un archivio SQL Server esistente per il mirroring, nell'elenco a discesa **Mirror archivio SQL Server archiviazione** fare clic sul nome dell'archivio SQL Server da utilizzare per il mirroring.
    
      - Per specificare un nuovo archivio SQL Server per il mirroring, fare clic su **Nuovo** e quindi nella finestra di dialogo **Definire un nuovo archivio SQL Server** eseguire una delle operazioni seguenti:
        
        1.  In **FQDN SQL Server** specificare il nome di dominio completo del server SQL Server in cui creare il nuovo archivio SQL Server.
        
        2.  Fare clic su **Istanza predefinita** per utilizzare l'istanza predefinita oppure fare clic su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza da utilizzare.
        
        3.  Se l'istanza di SQL Server specificata è in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring** e quindi specificare il numero di porta in **Numero porta di mirroring**.
    
      - Se si abilita il mirroring di SQL Server e si vuole includere il controllo del mirroring di SQL Server (una terza e distinta istanza di SQL Server in grado di rilevare l'integrità del server SQL Server primario e delle istanze mirror), selezionare la casella di controllo **Usa controllo del mirroring di SQL Server per abilitare il failover automatico** e quindi eseguire una delle operazioni seguenti:
        
        1.  In **FQDN SQL Server** specificare il nome di dominio completo del server in cui si vuole creare il nuovo controllo del mirroring di SQL Server.
        
        2.  Fare clic su **Istanza predefinita** per utilizzare l'istanza predefinita oppure fare clic su **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza da utilizzare per il controllo del mirroring.
        
        3.  Se l'istanza di SQL Server specificata è in una relazione di mirroring, selezionare la casella di controllo **L'istanza SQL è in relazione di mirroring** e quindi specificare il numero di porta in **Numero porta di mirroring**.

10. Per salvare la configurazione fare clic su **OK**.

