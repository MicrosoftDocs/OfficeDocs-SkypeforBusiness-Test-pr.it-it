---
title: Ripristino di un server back-end Enterprise Edition con mirroring - Principale
TOCTitle: Ripristino di un server back-end Enterprise Edition con mirroring - Principale
ms:assetid: bc555b46-70c5-4eee-ae91-e195df238293
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945648(v=OCS.15)
ms:contentKeyID: 52062299
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un server back-end Enterprise Edition con mirroring - Principale

 

_**Ultima modifica dell'argomento:** 2013-02-17_

Se si dispone di un server back-end Enterprise Edition in una configurazione con mirroring e si verifica un errore solo nel database primario, seguire le procedure incluse in questa sezione. Se si verifica un errore sia nel database primario che nel database mirror, vedere [Ripristino di un Server Enterprise back-end](lync-server-2013-restoring-an-enterprise-edition-back-end-server.md). Se si verifica un errore solo nel database mirror, vedere [Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md). Se si verifica un errore nel database che ospita l'archivio di gestione centrale, vedere [Ripristino del server che ospita l'archivio di gestione centrale](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md). Se si verifica un errore in un server membro Enterprise Edition diverso dal server back-end, vedere [Ripristino di un server membro Enterprise Edition](lync-server-2013-restoring-an-enterprise-edition-member-server.md).

È consigliabile creare una copia dell'immagine del sistema prima di avviare il ripristino. È possibile utilizzare questa immagine come punto di rollback, in caso di problemi durante il ripristino. Potrebbe essere utile creare la copia dell'immagine dopo avere installato il sistema operativo e SQL Server, quindi ripristinare o registrare nuovamente i certificati.

In questo argomento il nome di dominio completo (FQDN) del database primario di esempio sarà BE1.contoso.com, quello del database mirror sarà invece BE2.contoso.com.

## Per ripristinare un database primario di server back-end Enterprise Edition

1.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere a un Front End Server.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Forzare il failover di tutti i database configurati sul mirror. Per ogni tipo di database configurato su questo server, digitare il cmdlet seguente:
    
        Invoke-CsDataBaseFailover -PoolFqdn <Pool FQDN> -DatabaseType <Configured Database Type> -NewPrincipal Mirror -Force -Verbose
    
    Ad esempio:
    
        Invoke-CsDataBaseFailover -PoolFqdn pool0.vdomain.com -DatabaseType User -NewPrincipal Mirror -Force -Verbose
    

    > [!WARNING]
    > Se è stato configurato il database back-end per l'utilizzo del mirroring sincronizzato con un'istanza di controllo, il failover è automatico.



4.  Al termine del failover, eseguire quanto segue:
    
      - Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
      - Disabilitare il mirroring sul server back-end: fare clic con il pulsante destro del mouse sul pool in **Pool Enterprise Edition Front End** e scegliere **Modifica proprietà**. Nella scheda **Generale**, in **Associazioni**, deselezionare la casella di controllo **Abilita mirroring dell'archivio SQL Server**. Eseguire questa operazione per il server di archiviazione e Monitoring Server, se necessario. Fare quindi clic su **OK**.
    
      - Fare clic con il pulsante destro del mouse sul nodo Lync Server 2013, scegliere **Topologia** e quindi fare clic su **Pubblica**.
    
      - Impostare il back-end ancora funzionante (BE2.contoso.com) come nuovo archivio SQL. Per eseguire questa operazione, fare clic con il pulsante destro del mouse sul pool in **Pool Enterprise Edition Front End** e scegliere **Modifica proprietà**. Nella scheda **Generale**, in **Associazioni**, digitare il nome FQDN del back-end funzionante nel campo **Archivio SQL Server** (nell'esempio, BE2.contoso.com).
    
      - Fare clic con il pulsante destro del mouse sul nodo Lync Server 2013, scegliere **Topologia** e quindi fare clic su **Pubblica**.
    
      - Riavviare i servizi in modo che ogni server sia in grado di leggere la nuova topologia. In una Lync Server Management Shell eseguire i cmdlet seguenti in ogni Front End Server appartenente a questo pool:
        
            Stop-CsWindowsService
            Start-CsWindowsService

5.  Disinstallare il mirroring. In una Lync Server Management Shell eseguire il cmdlet seguente:
    
        Uninstall-CsMirrorDatabase -DatabaseType User -SqlServerFqdn <MirrorServerFqdn> -SqlInstanceName <SQLInstance> -verbose
    
    Ad esempio:
    
        Uninstall-CsMirrorDatabase -DatabaseType User -SqlServerFqdn DB2.contoso.com -SqlInstanceName rtc -verbose
    
    Eseguire questa operazione per tutti i tipi di database nel server.

6.  Creare un server pulito o nuovo con lo stesso nome FQDN (in questo esempio DB1.contoso.com) del computer in cui si è verificato l'errore, installare il sistema operativo e quindi ripristinare o registrare nuovamente i certificati. Questo server sarà il nuovo mirror.

7.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere al nuovo server.

8.  Installare SQL Server 2012 o SQL Server 2008 R2 mantenendo gli stessi nomi delle istanze utilizzati prima dell'errore.

9.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere a un Front End Server.

10. Utilizzare Generatore di topologie per installare il database mirror. Eseguire i passaggi riportati di seguito:
    
      - Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
      - Abilitare il mirroring sul server back-end. A questo scopo, fare clic con il pulsante destro del mouse sul pool in **Pool Enterprise Edition Front End** e scegliere **Modifica proprietà**. Nella scheda **Generale**, in **Associazioni**, selezionare la casella di controllo **Abilita mirroring dell'archivio SQL Server**. Eseguire inoltre questa operazione per il server di archiviazione e Monitoring Server, se necessario.
        
        Nel campo **Mirror archivio SQL Server** digitare quindi il nome FQDN del nuovo server (in questo esempio BE1.contoso.com). Fare quindi clic su **OK**.
    
      - Fare clic con il pulsante destro del mouse sul nodo Lync Server 2013, scegliere **Topologia** e quindi fare clic su **Installa database**.
    
      - Seguire le istruzioni della procedura guidata**Installa database**. Nella pagina **Creare database** selezionare i database che si desidera ricreare.
    
      - Seguire la procedura guidata fino al prompt **Creare database mirror**. Selezionare il database che si desidera installare e completare il processo.

