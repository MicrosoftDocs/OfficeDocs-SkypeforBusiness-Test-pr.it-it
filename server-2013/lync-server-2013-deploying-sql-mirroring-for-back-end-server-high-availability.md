---
title: 'Lync Server 2013: Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end'
TOCTitle: Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end
ms:assetid: 70224520-b5c8-4940-a08e-7fb9b1adde8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204992(v=OCS.15)
ms:contentKeyID: 49300932
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-08_

Per distribuire il mirroring SQL, i server devono eseguire almeno SQL Server 2008 R2. Questa versione deve essere eseguita da tutti i server coinvolti: il server primario, mirror, e di controllo. Per informazioni dettagliate vedere [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x410).

In generale, la configurazione del mirroring SQL tra due server di back-end con un server di controllo richiede che:

  - La versione di SQL Server del server primario supporti il mirroring SQL.

  - I server primario, mirror e di controllo (se distribuito) abbiano la stessa versione di SQL Server.

  - Il server primario e mirror abbiano la stessa edizione di SQL Server. Il server di controllo può avere un'edizione diversa.

Per le best practice SQL in termini di versioni SQL supportate per un ruolo di controllo, vedere "Server di controllo del mirroring del database" in MSDN Library all'indirizzo [http://go.microsoft.com/fwlink/?linkid=247345\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=247345%26clcid=0x410).

Per la distribuzione del mirroring SQL è possibile utilizzare Generatore di topologie. Si seleziona un'opzione per il mirroring del database in Generatore di topologie, e il Generatore di topologie configura il mirroring (e, se lo si desidera, un'istanza di controllo) quando si pubblica la topologia. Il server di controllo viene rimosso o configurato contemporaneamente alla rimozione o configurazione del mirror. Non esiste un comando separato che consente di distribuire o rimuovere unicamente un server di controllo.

Per configurare il mirroring del server, è prima necessario configurare correttamente le autorizzazioni del database SQL. Per informazioni dettagliate, vedere "Configurare gli account di accesso per il mirroring del database o i gruppi di disponibilità AlwaysOn (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268454\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268454%26clcid=0x410).

Con il mirroring SQL, la modalità di recupero del database è impostata sempre su **Completa** . Ciò significa che è necessario monitorare le dimensioni del log delle transizioni ed eseguire regolarmente il backup dei log più grandi, per evitare che la memoria del disco dei server di back-end si riempia. La frequenza dei backup dei log delle transizioni dipende dal tasso di crescita dei log, che a sua volta dipende dalle transazioni del database relative alle attività degli utenti nel pool Front End. Per pianificare correttamente, è consigliabile determinare il tasso di crescita stimato del log delle transazioni per il carico di lavoro della distribuzione di Lync. I seguenti articoli contengono informazioni aggiuntive sul backup SQL e la gestione dei log:

  - Modelli di recupero del database: "Modelli di recupero (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268446\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268446%26clcid=0x410)

  - Panoramica del backup: "Panoramica del backup (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268449\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268449%26clcid=0x410)

  - Backup del log delle transazioni: "Backup di un log delle transazioni (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268452\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268452%26clcid=0x410)

Nel mirroring SQL è possibile configurare la topologia per il mirroring al momento della creazione dei pool, o in seguito.

> [!IMPORTANT]  
> L'utilizzo di Generatore di topologie o dei cmdlet per la configurazione e la rimozione del mirroring SQL è supportata unicamente quando i server primario, mirror e di controllo (se desiderato) appartengono allo stesso dominio. Per configurare il mirroring SQL tra server su domini diversi, vedere la documentazione relativa a SQL Server.

> [!IMPORTANT]  
> Quando si apportano modifiche a una relazione di mirroring di un database di back end, è necessario riavviare tutti i Front End Server nel pool.<br />Per apportare una modifica nel mirroring, ad esempio per modificare la località di un mirror, è necessario utilizzare Generatore di topologie per eseguire i tre passaggi successivi:<ol>
> <li><p>Rimuovere il mirroring dal server mirror meno recente.</p></li>
> 
> <li><p>Aggiungere il mirroring al nuovo server mirror.</p></li>
> 
> 
> <li><p>Pubblicare la topologia.</p></li></ol>



> [!NOTE]
> È necessario creare una condivisione file in cui scrivere i file mirror e concedere l'accesso in lettura/scrittura al servizio in vengono eseguiti SQL Server e SQL Agent. Se il servizio SQL Server viene eseguito all'interno del Servizio di rete, è possibile aggiungere &lt;Dominio&gt;\\&lt;NOMESERVERSQL&gt;$ dell'SQL Server principale e dell'SQL Server mirror alle autorizzazioni di condivisione. Il simbolo $ è importante per indicare che si tratta di un account computer.



## Per configurare il mirroring SQL durante la creazione di un pool in Generatore di topologie

1.  Nella pagina **Definisci archivio SQL** , fare clic su **Nuovo** accanto alla casella **Archivio SQL** .

2.  Nella pagina **Definisci nuovo archivio SQL** , specificare l'archivio primario, selezionare **L'istanza SQL è in relazione di mirroring** , specificare il numero di porta del mirroring SQL (il valore predefinito è 5022), quindi fare clic su **OK** .

3.  Nella pagina **Definisci archivio SQL** , selezionare **Abilita archivio mirroring SQL** .

4.  Nella pagina **Definisci nuovo archivio SQL** , specificare l'archivio SQL da utilizzare come mirror. Selezionare **L'istanza SQL è in relazione di mirroring** , specificare il numero di porta (il valore predefinito è 5022), quindi fare clic su **OK** .

5.  Se si desidera un'istanza di controllo per il mirror, effettuare le operazioni seguenti:
    
    1.  Selezionare **Usa controllo del mirroring di SQL Server per abilitare il failover automatico** .
    
    2.  Nella pagina **Definisci archivio SQL** , selezionare **Usa controllo del mirroring di SQL Server per abilitare il failover automatico** e specificare l'archivio SQL da utilizzare per il controllo.
    
    3.  Specificare il numero di porta (il valore predefinito è 7022) e fare clic su **OK**

6.  Al termine della definizione del pool Front End e degli altri ruoli all'interno della topologia, utilizzare Generatore di topologie per pubblicare la topologia. Dopo aver pubblicato la topologia, se nel pool Front End che ospita archivio di gestione centrale è attivo il mirroring SQL, comparirà un'opzione per creare i database dell'archivio SQL primario e mirror.
    
    Fare clic su **Impostazioni** e digitare il percorso da utilizzare come condivisione file per il backup del mirroring.
    
    Fare clic su **OK** e **Avanti** per creare i database e pubblicare la topologia. I server di mirroring e di controllo (se specificato) saranno così distribuiti.

È possibile utilizzare Generatore di topologie per modificare le proprietà di un pool esistente e abilitare il mirroring SQL.

## Per aggiungere il mirroring SQL a un pool Front End esistente in Generatore di topologie

1.  In Generatore di topologie, fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

2.  Selezionare **Abilita mirroring dell'archivio SQL** , quindi fare clic su **Nuovo** accanto a **Mirroring dell'archivio SQL** .

3.  Specificare l'archivio SQL che si desidera utilizzare come mirror.

4.  Selezionare **L'istanza SQL è in relazione di mirroring** , specificare il numero di porta per il mirroring SQL (il valore predefinito è 5022), quindi fare clic su **OK** .

5.  Per configurare un'istanza di controllo, selezionare **Usa controllo del mirroring di SQL Server per abilitare il failover automatico** e fare clic su **Nuovo** .

6.  Specificare l'archivio SQL che si desidera utilizzare come istanza di controllo.

7.  Selezionare **L'istanza SQL è in relazione di mirroring** , specificare il numero di porta per il mirroring SQL (il valore predefinito è 7022), quindi fare clic su **OK** .

8.  Fare clic su **OK** .

9.  Pubblicare la topologia. Verrà richiesto di installare il database.
    
    Durante il processo di pubblicazione della topologia, verrà richiesto di definire un percorso di condivisione file. Gli SQL Server che partecipano al mirroring devono disporre dell'accesso in lettura/scrittura a questa condivisione file affinché sia possibile stabilire il mirror.

A questo punto è necessario installare il database prima di passare alla procedura successiva.

Quando si configura il mirroring SQL, è necessario tenere a mente alcuni punti:

  - Se esiste già un endpoint del mirroring, sarà riutilizzato insieme alle porte definite qui, e saranno ignorate quelle specificate nella topologia.

  - Le porte già allocate ad altre applicazioni sullo stesso server, comprese quelle allocate ad altre istanze di SQL, non devono essere utilizzate per le nuove istanze di SQL installate. Pertanto, se si ha più di una istanza SQL installata sullo stesso server, queste devono utilizzare porte differenti per il mirroring. Per ulteriori dettagli, vedere:
    
      - "Specificare un indirizzo di rete del server (Mirroring del database)" in MSDN Library all'indirizzo [http://go.microsoft.com/fwlink/?linkid=247346\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=247346%26clcid=0x410)
    
      - "Endpoint del mirroring del database (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=247347\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=247347%26clcid=0x410)

## Utilizzo dei cmdlet di Lync Server Management Shell per la configurazione del mirroring SQL

Il modo più semplice per configurare il mirroring consiste nell'utilizzo di Generatore di topologie, ma è anche possibile utilizzare i cmdlet.

1.  Aprire una finestra di Lync Server Management Shell ed eseguire il cmdlet seguente:
    
        Install-CsMirrorDatabase [-ConfiguredDatabases] [-ForInstance] [-ForDefaultInstance] [-DatabaseType <Application | Archiving | CentralMgmt | Monitoring | User | BIStaging | PersistentChat | PersistentChatCompliance >] -FileShare <fileshare> -SqlServerFqdn <primarySqlserverFqdn> [-SqlInstanceName] [-DatabasePathMap] [-ExcludeDatabaseList] [-DropExistingDatabasesOnMirror] -Verbose 
    
    Ad esempio:
    
        Install-CsMirrorDatabase -ConfiguredDatabases -FileShare \\PRIMARYBE\csdatabackup -SqlServerFqdn primaryBE.contoso.com -DropExistingDatabasesOnMirror -Verbose 
    
    Verrà visualizzato quanto segue:
    
        Database Name:rtcxds 
                Data File:D:\CsData\BackendStore\rtc\DbPath\rtcxds.mdf 
                 Log File:D:\CsData\BackendStore\rtc\LogPath\rtcxds.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:rtcshared 
                Data File:D:\CsData\BackendStore\rtc\DbPath\rtcshared.mdf 
                 Log File:D:\CsData\BackendStore\rtc\LogPath\rtcshared.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:rtcab 
                Data File:D:\CsData\ABSStore\rtc\DbPath\rtcab.mdf 
                 Log File:D:\CsData\ABSStore\rtc\LogPath\rtcab.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:rgsconfig 
                Data File:D:\CsData\ApplicationStore\rtc\DbPath\rgsconfig.mdf 
                 Log File:D:\CsData\ApplicationStore\rtc\LogPath\rgsconfig.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:rgsdyn 
                Data File:D:\CsData\ApplicationStore\rtc\DbPath\rgsdyn.mdf 
                 Log File:D:\CsData\ApplicationStore\rtc\LogPath\rgsdyn.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:cpsdyn 
                Data File:D:\CsData\ApplicationStore\rtc\DbPath\cpsdyn.mdf 
                 Log File:D:\CsData\ApplicationStore\rtc\LogPath\cpsdyn.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:xds 
                Data File:D:\CsData\CentralMgmtStore\rtc\DbPath\xds.mdf 
                 Log File:D:\CsData\CentralMgmtStore\rtc\LogPath\xds.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$ 
            Database Name:lis 
                Data File:D:\CsData\CentralMgmtStore\rtc\DbPath\lis.mdf 
                 Log File:D:\CsData\CentralMgmtStore\rtc\LogPath\lis.ldf 
              Primary SQL: e04-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\e04-ocs$ 
               Mirror SQL: K16-ocs.los_a.lsipt.local\rtc 
                  Account: LOS_A\K16-ocs$ 
             Witness SQL : AB14-lct.los_a.lsipt.local\rtc 
                  Account: LOS_A\AB14-lct$
        [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): 

2.  Verificare che:
    
      - La Porta 5022 sia accessibile attraverso il firewall se Windows Firewall è abilitato sel server SQL primario e04-ocs.los\_a.lsipt.local\\rtc.
    
      - La Porta 5022 sia accessibile attraverso il firewall se Windows Firewall è abilitato sel server SQL mirror K16-ocs.los\_a.lsipt.local\\rtc.
    
      - La Porta 7022 sia accessibile attraverso il firewall se Windows Firewall è abilitato sel server SQL di controllo AB14-lct.los\_a.lsipt.local\\rtc.
    
      - Gli account che eseguono SQL Server su tutti i server SQL primari e mirror siano dotati di autorizzazioni di lettura e scrittura per la condivisione file \\\\E04-OCS\\csdatabackup
    
      - Verificare che il provider della Strumentazione gestione Windows (WMI) sia eseguito su tutti questi server. Il cmdlet si serve di questo provider per trovare le informazioni sull'account relative ai servizi di SQL Server eseguiti su tutti i server primari, mirror e di controllo.
    
      - Verificare che l'account sul quale è eseguito il cmdlet abbia le autorizzazioni necessarie per creare le cartelle per i dati e i file dei log per tutti i server mirror.
    
      - Si noti che l'account utente utilizzato dall'istanza SQL per la propria esecuzione deve essere dotato di autorizzazioni di lettura e scrittura per la condivisione file. Se la condivisione file si trova su un server diverso e l'istanza SQL esegue un account di sistema locale, è necessario concedere autorizzazioni per la condivisione file al server che ospita l'istanza SQL.

3.  Digitare A e premere INVIO.
    
    Sarà configurato il mirroring.

**Install-CsMirrorDatabase** installa il mirror e configura il mirroring per tutti i database presenti nell'archivio SQL primario. Se si desidera configurare il mirroring soltanto per database specifici, è possibile utilizzare l'opzione –DatabaseType. Se si desidera configurare il mirroring per tutti i database, ad eccezione di alcuni, è possibile utilizzare l'opzione -ExcludeDatabaseList, insieme a un elenco dei nomi dei database da escludere, separati da una virgola.

Ad esempio, se si aggiunge l'opzione seguente a **Install-CsMirrorDatabase**, si eseguirà il mirroring per tutti i database ad eccezione di rtcab e rtcxds.

`-ExcludeDatabaseList rtcab,rtcxds`

Ad esempio, se si aggiunge l'opzione seguente a **Install-CsMirrorDatabase**, si eseguirà il mirroring unicamente per i database rtcab e rtcxds.

`-DatabaseType User`

## Rimozione o modifica del mirroring SQL

Per rimuovere il mirroring SQL da un pool in Generatore di topologie, è prima necessario utilizzare un cmdlet per la rimozione del mirror in SQL Server. È quindi possibile utilizzare Generatore di topologie per rimuovere il mirror dalla topologia. Per rimuovere il mirror in SQL Server, utilizzare il cmdlet seguente:

    Uninstall-CsMirrorDatabase -SqlServerFqdn <SQLServer FQDN> [-SqlInstanceName <SQLServer instance name>] -DatabaseType <Application | Archiving | CentralMgmt | Monitoring | User | BIStaging | PersistentChat | PersistentChatCompliance> [-DropExistingDatabasesOnMirror] [-Verbose]

Ad esempio, per rimuovere il mirroring ed eliminare i database degli utenti, digitare:

    Uninstall-CsMirrorDatabase -SqlServerFqdn primaryBE.contoso.com -SqlInstanceName rtc -Verbose -DatabaseType User -DropExistingDatabasesOnMirror

L'opzione `-DropExistingDatabasesOnMirror` causa l'eliminazione dal mirror dei database coinvolti.

Per rimuovere quindi il mirroring dalla topologia, procedere come segue:

1.  In Generatore di topologie, fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

2.  Deselezionare **Abilita archivio mirroring SQL** e fare clic su **OK** .

3.  Pubblicare la topologia.

## Rimozione di un Server di controllo del mirroring

Utilizzare questa procedura se si ha bisogno di rimuovere il Server di controllo da una configurazione del mirroring di server back-end.

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul pool e scegliere **Modifica proprietà** .

2.  Deselezionare **Usa controllo del mirroring di SQL Server per abilitare il failover automatico** e fare clic su **OK** .

3.  Pubblicare la topologia.
    
    Dopo la pubblicazione della topologia, in Generatore di topologie comparirà un messaggio che include quanto segue
    
        Run the Uninstall-CsMirrorDatabase cmdlet to remove databases that are paired with following primary databases.
    
    Non seguire questo passaggio, e non digitare `Uninstall-CsMirrorDatabase` poiché in questo modo si disinstallerebbe l'intera configurazione del mirroring.

4.  Per rimuovere il server di controllo del mirroring da una configurazione SQL Server, seguire le istruzioni in "Rimuovere il server di controllo del mirroring da una sessione di mirroring del database (SQL Server)" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268456\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268456%26clcid=0x410).

