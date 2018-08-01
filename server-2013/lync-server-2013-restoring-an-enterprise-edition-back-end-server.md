---
title: Ripristino di un Server Enterprise back-end
TOCTitle: Ripristino di un Server Enterprise back-end
ms:assetid: 1450eb4e-3315-4d02-8f02-6e1791fb1550
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202163(v=OCS.15)
ms:contentKeyID: 52062097
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un Server Enterprise back-end

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Utilizzare la procedura descritta in questo argomento nei due casi seguenti:

  - Si verificano errori sia nel database primario che nel database mirror di un server back-end Enterprise Edition con mirroring.

  - Si verificano errori in un server back-end Enterprise Edition senza mirroring.

Se si dispone di un server back-end Enterprise Edition con mirroring e si verificano errori solo nel database primario o mirror, vedere [Ripristino di un server back-end Enterprise Edition con mirroring - Principale](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md) per ripristinare il database primario e [Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring](lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md) per ripristinare il database mirror.

Se si verificano errori nell'archivio di gestione centrale, vedere [Ripristino del server che ospita l'archivio di gestione centrale](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md). Se si verificano errori in un server membro di Enterprise Edition che non corrisponde al server back-end, vedere [Ripristino di un server membro Enterprise Edition](lync-server-2013-restoring-an-enterprise-edition-member-server.md).

> [!TIP]  
> È consigliabile creare una copia dell'immagine del sistema prima di avviare il ripristino. È possibile utilizzare questa immagine come punto di rollback, in caso di problemi durante il ripristino. Potrebbe essere utile creare la copia dell'immagine dopo avere installato il sistema operativo e SQL Server, quindi ripristinare o registrare nuovamente i certificati.

## Per ripristinare un server back-end Enterprise Edition

1.  Partire con un server pulito o nuovo che disponga dello stesso nome di dominio completo (FQDN) del computer che presenta problemi, installare il sistema operativo e quindi ripristinare o registrare di nuovo i certificati.
    

    > [!NOTE]
    > Per eseguire questo passaggio, attenersi alle procedure di distribuzione del server utilizzate dall'organizzazione.



2.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere al server che si sta ripristinando.

3.  Installare SQL Server 2012 o SQL Server 2008 R2 mantenendo gli stessi nomi delle istanze utilizzati prima dell'errore.
    

    > [!NOTE]
    > A seconda della distribuzione, il server back-end può includere più database collocati o separati. Per installare SQL Server, eseguire la stessa procedura utilizzata originariamente per distribuire il server, inclusi gli account di accesso e le autorizzazioni di SQL Server.



4.  Dopo aver installato SQL Server, eseguire le operazioni seguenti:
    
    1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
    2.  Fare clic su **Scarica topologia dalla distribuzione esistente** e quindi su **OK**.
    
    3.  Selezionare la topologia e quindi fare clic su **Salva**. Fare clic su **Sì** per confermare la selezione.
    
    4.  Fare clic con il pulsante destro del mouse sul nodo **Lync Server 2013** e quindi scegliere **Pubblica topologia**.
    
    5.  Eseguire la procedura guidata **Pubblicare la topologia**. Nella pagina **Creare database** selezionare i database che si desidera ricreare.
        

        > [!NOTE]
        > Nella pagina <STRONG>Creare database</STRONG> vengono visualizzati solo i database autonomi.

    
    6.  Se si sta ripristinando un server back-end con mirroring, continuare a seguire la procedura guidata finché non viene visualizzata la pagina **Creare database mirror**. Selezionare il database da installare e completare la procedura.
    
    7.  Eseguire il resto della procedura guidata e quindi fare clic su **Fine**.
    
    > [!TIP]  
    > Invece di eseguire Generatore di topologie, è possibile utilizzare il cmdlet <strong>Install-CsDatabase</strong> per creare ogni database e il cmdlet <strong>Install-CsMirrorDatabase</strong> per configurare il mirroring. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell.

5.  Ripristinare i dati degli utenti eseguendo le operazioni seguenti:
    
    1.  Copiare ExportedUserData.zip da $Backup\\ in una directory locale.
    
    2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.
    
    3.  Prima di ripristinare i dati utente, è necessario arrestare i servizi di Lync. A tale scopo, digitare:
        
            Stop-CsWindowsService
    
    4.  Per ripristinare i dati degli utenti, nella riga di comando digitare quanto segue:
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        Ad esempio:
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    5.  Riavviare i servizi di Lync digitando:
        
            Start-CsWindowsService

6.  Se Response Group è stato distribuito nel pool, ripristinare i dati di configurazione di Response Group. Per ulteriori informazioni, vedere [Ripristino delle impostazioni di Response Group](lync-server-2013-restoring-response-group-settings.md).

7.  Se si sta ripristinando un server back-end che includeva il database di archiviazione o di monitoraggio, ripristinare i dati di archiviazione o monitoraggio mediante uno strumento di SQL Server, ad esempio SQL Server Management Studio. Per ulteriori informazioni, vedere [Ripristino dei dati di monitoraggio o archiviazione](lync-server-2013-restoring-monitoring-or-archiving-data.md).

