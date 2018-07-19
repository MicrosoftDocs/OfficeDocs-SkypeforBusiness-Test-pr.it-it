---
title: Ripristino del server che ospita l'archivio di gestione centrale
TOCTitle: Ripristino del server che ospita l'archivio di gestione centrale
ms:assetid: 3bd6c82c-07fb-4798-b8f9-e7c78a5a83d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202172(v=OCS.15)
ms:contentKeyID: 52062132
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino del server che ospita l'archivio di gestione centrale

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In una distribuzione di Lync Server è presente un singolo archivio di gestione centrale, di cui viene replicata una copia in ogni server che esegue un ruolo del server di Lync Server. In questo argomento viene descritto come ripristinare un server back-end o un server Standard Edition che ospita l'archivio di gestione centrale.

Per trovare il pool in cui è posizionato il server di gestione centrale, aprire Generatore di topologie, fare clic su **Lync Server** ed esaminare il riquadro di destra al di sotto di **Server di gestione centrale**.

Se il server back-end che ospita l'archivio di gestione centrale si trova in una configurazione con mirroring e il database mirror è ancora funzionante, è consigliabile eseguire un backup del mirror ancora funzionante e quindi eseguire un ripristino completo sia nel database primario che nel database mirror con tale backup, seguendo la procedura di ripristino indicata di seguito. Ciò è necessario perché per il ripristino del back-end sono richieste la modifica e la pubblicazione della topologia e queste operazioni possono essere eseguite solo se il database primario che ospita l'archivio di gestione centrale è operativo. Si noti inoltre che i ruoli di database primario e mirror non sono interscambiabili se non è possibile pubblicare la topologia.


> [!NOTE]
> Se si è verificato un errore del server back-end o del server Standard Edition che non ospita l'archivio di gestione centrale, vedere <A href="lync-server-2013-restoring-an-enterprise-edition-back-end-server.md">Ripristino di un Server Enterprise back-end</A> o <A href="lync-server-2013-restoring-a-standard-edition-server.md">Ripristino di un server Standard Edition</A>. Se un server back-end che ospita l'archivio di gestione centrale si trova in una configurazione con mirroring e solo il mirror è in errore, vedere <A href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md">Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring</A>. Se si è verificato un errore di qualsiasi altro server, vedere <A href="lync-server-2013-restoring-an-enterprise-edition-member-server.md">Ripristino di un server membro Enterprise Edition</A>.



<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È consigliabile acquisire una copia dell'immagine del sistema prima di avviare il ripristino, per poterla utilizzare come punto di ripristino dello stato precedente in caso di problemi durante le operazioni di ripristino. È possibile acquisire la copia dell'immagine dopo l'installazione del sistema operativo e di SQL Server e ripristinare o registrare di nuovo i certificati.</td>
</tr>
</tbody>
</table>


## Per ripristinare l'archivio di gestione centrale

1.  Iniziare con un server pulito o nuovo con lo stesso nome di dominio completo (FQDN) del computer in cui si è verificato l'errore, installare il sistema operativo e quindi ripristinare o registrare di nuovo i certificati.
    

    > [!NOTE]
    > Seguire le procedure di distribuzione dei server dell'organizzazione per eseguire questa operazione.



2.  Eseguire l'accesso al server da ripristinare utilizzando un account utente membro del gruppo RTCUniversalServerAdmins e del gruppo Administrators locale.

3.  Se si desidera ripristinare un server Standard Edition, ripristinare l'Archivio file copiando l'Archivio file appropriato da $Backup nel percorso dell'Archivio file nel server e quindi condividere la cartella.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il percorso e il nome file dell'Archivio file ripristinato devono corrispondere esattamente a quelli dell'Archivio file di cui è stato eseguito il backup in modo che i componenti che utilizzano i file possano accedervi.</td>
    </tr>
    </tbody>
    </table>


4.  Eseguire una delle operazioni seguenti:
    
      - Se si installa un server Standard Edition, passare alla cartella o al supporto di installazione di Lync Server e quindi avviare la Distribuzione guidata di Lync Server contenuta in \\setup\\amd64\\Setup.exe. Nella Distribuzione guidata fare clic su **Prepara primo Server Standard** e seguire le istruzioni per installare l'archivio di gestione centrale.
    
      - Se si installa un server back-end Enterprise Edition, installare SQL Server 2012 o SQL Server 2008 R2 mantenendo gli stessi nomi delle istanze utilizzati prima dell'errore.
        

        > [!NOTE]
        > A seconda del server che si desidera ripristinare e della distribuzione, è possibile che il server includa più database collocati o separati. Seguire la stessa procedura di installazione di SQL Server utilizzata in origine per la distribuzione del server, inclusi le autorizzazioni e gli account di accesso di SQL Server.



5.  Da un Front End Server, Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

6.  Ricreare l'archivio di gestione centrale. Nella riga di comando digitare:
    
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn <FQDN> -SqlInstanceName <instance name> -Verbose
    
    Ad esempio:
    
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn Server01.contoso.com -SqlInstanceName cms -Verbose

7.  Impostare il punto di controllo di Servizi di dominio Active Directory per l'archivio di gestione centrale. Nella riga di comando digitare:
    
        Set-CsConfigurationStoreLocation -SqlServerFqdn <FQDN> -SqlInstanceName <instance name> -Verbose
    
    Ad esempio:
    
        Set-CsConfigurationStoreLocation -SqlServerFqdn Server01.contoso.com -SqlInstanceName cms -Verbose
    

    > [!NOTE]
    > Se si perde il punto di connessione, è possibile eseguire di nuovo questo cmdlet.



8.  Importare i dati dell'archivio di gestione centrale da $Backup. Nella riga di comando digitare:
    
        Import-CsConfiguration -FileName <CMS backup file name>
    
    Ad esempio:
    
        Import-CsConfiguration -FileName "C:\Config.zip"

9.  Abilitare le modifiche che sono state apportate. Nella riga di comando digitare:
    
        Enable-CsTopology
    

    > [!NOTE]
    > Dopo aver abilitato la topologia, è possibile trovare il relativo documento nel database.



10. Seguire questo passaggio per eseguire il ripristino di un server back-endEnterprise Edition anch'esso ospitato nell'archivio di gestione centrale oppure se è necessario ricreare un mirror dell'archivio di gestione centrale. In caso contrario, procedere al passaggio 11.
    
    Installare i database autonomi eseguendo le operazioni seguenti:
    
    1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
    2.  Fare clic su **Scarica topologia dalla distribuzione esistente** e quindi su **OK**.
    
    3.  Selezionare la topologia e quindi fare clic su **Salva**. Fare clic su **Sì** per confermare la selezione.
    
    4.  Fare clic con il pulsante destro del mouse sul nodo **Lync Server 2013** e quindi scegliere **Installa database**.
    
    5.  Seguire le istruzioni della procedura guidata **Installa database**. Se si ripristina un database diverso dall'archivio di gestione centrale nel server, nella pagina **Creare database** selezionare i database che si desidera ricreare.
        

        > [!NOTE]
        > Nella pagina <STRONG>Creare database</STRONG> verranno visualizzati solo i database autonomi. I database collocati vengono creati quando si esegue la Distribuzione guidata di Lync Server.

    
    6.  Per eseguire il ripristino di un server back-end con mirroring, continuare con il resto della procedura guidata fino a quando non viene visualizzata la richiesta Creare database mirror. Selezionare il database che si desidera installare e completare il processo.
    
    7.  Seguire il resto della procedura guidata e quindi fare clic su **Fine**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Anziché eseguire Generatore di topologie, è possibile utilizzare il cmdlet <strong>Install-CsDatabase</strong> per creare ogni database e il cmdlet <strong>Install-CsMirrorDatabase</strong> per configurare il mirroring. Per informazioni dettagliate, vedere <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Install-CsDatabase">Install-CsDatabase</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Install-CsMirrorDatabase">Install-CsMirrorDatabase</a>..</td>
    </tr>
    </tbody>
    </table>


11. Se si ripristina un server Standard Edition, passare alla cartella o al supporto di installazione di Lync Server e avviare la Distribuzione guidata di Lync Server contenuta in \\setup\\amd64\\Setup.exe. Utilizzare la Distribuzione guidata di Lync Server per eseguire le operazioni seguenti:
    
    1.  Eseguire **Passaggio 1: Installazione dell'archivio di configurazione locale** per installare i file della configurazione locale.
    
    2.  Eseguire **Passaggio 2: Installazione o rimozione componenti di Lync Server** per installare i ruoli del server di Lync Server.
    
    3.  Eseguire **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** per assegnare i certificati.
    
    4.  Eseguire **Passaggio 4: Avvio servizi** per avviare i servizi nel server.
    
    Per informazioni dettagliate sull'esecuzione della Distribuzione guidata, vedere la documentazione relativa alla distribuzione per il ruolo del server da ripristinare.

12. Ripristinare i dati utente eseguendo le operazioni seguenti:
    
    1.  Copiare ExportedUserData.zip da $Backup\\ in una directory locale.
    
    2.  Prima di ripristinare i dati utente, è necessario arrestare i servizi di Lync. A tale scopo, digitare:
        
            Stop-CsWindowsService
    
    3.  Per ripristinare i dati utente, nella riga di comando digitare:
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        Ad esempio:
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    4.  Riavviare i servizi di Lync digitando:
        
            Start-CsWindowsService

13. Ripristinare i dati di Informazioni percorso nell'archivio di gestione centrale. Nella riga di comando digitare:
    
        Import-CsLisConfiguration -FileName <LIS backup file name>
    
    Ad esempio:
    
        Import-CsLisConfiguration -FileName "D:\E911Config.zip"

14. Se è stato distribuito Response Group nel pool o nel server Standard Edition, ripristinare i dati di configurazione di Response Group. Per ulteriori informazioni, vedere [Ripristino delle impostazioni di Response Group](lync-server-2013-restoring-response-group-settings.md).

15. Per ripristinare un server back-end che include i database di archiviazione o di monitoraggio, ripristinare i dati di archiviazione o di monitoraggio utilizzando uno strumento di gestione di SQL Server, ad esempio SQL Server Management Studio. Per informazioni dettagliate, vedere [Ripristino dei dati di monitoraggio o archiviazione](lync-server-2013-restoring-monitoring-or-archiving-data.md).

