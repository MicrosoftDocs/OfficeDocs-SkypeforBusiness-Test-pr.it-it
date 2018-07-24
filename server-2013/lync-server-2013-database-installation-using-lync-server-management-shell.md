---
title: 'Lync Server 2013: Installazione di database mediante Lync Server Management Shell'
TOCTitle: Installazione di database mediante Lync Server Management Shell
ms:assetid: c90a6449-4dd5-4b18-b21c-ea2c2a64dc3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398832(v=OCS.15)
ms:contentKeyID: 49301970
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione di database mediante Lync Server Management Shell in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

La separazione dei ruoli e delle responsabilità tra gli amministratori dei server e gli amministratori di SQL Server può causare ritardi nell'implementazione. In Lync Server 2013 viene utilizzato il controllo dell'accesso basato sui ruoli per attenuare queste difficoltà. In alcuni casi, l'amministratore di SQL Server deve gestire l'installazione dei database nel server basato su SQL Server al di fuori del controllo dell'accesso basato sui ruoli. Lync Server 2013 Management Shell consente all'amministratore di SQL Server di eseguire cmdlet di Windows PowerShell progettati per configurare i database con i file di dati e di log appropriati. Per informazioni dettagliate, vedere [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nella procedura che segue si presuppone che siano stati installati almeno OCSCore.msi di Lync Server 2013, SQL Server Native Client (sqlncli.msi) Microsoft SQL Server 2012 Management Objects, Microsoft SQL Server 2012 CLR Types e Microsoft SQL Server 2012 ADOMD.NET. OCSCore.msi si trova nel supporto di installazione nella directory \Setup\AMD64\Setup. Gli altri componenti si trovano in \Setup\amd64. Si presuppone inoltre che siano state completate le operazioni per la preparazione di Active Directory per Lync Server 2013.</td>
</tr>
</tbody>
</table>


**Install-CsDatabase** è il cmdlet di Windows PowerShell utilizzato per installare i database. Il cmdlet **Install-CsDatabase** include un numero elevato di parametri, di cui solo alcuni verranno descritti in questa sezione. Per informazioni dettagliate sui parametri possibili, vedere la documentazione relativa a Lync Server 2013 Management Shell.


> [!WARNING]
> Per evitare problemi di prestazioni e possibili timeout, utilizzare sempre nomi di dominio completi (FQDN) per fare riferimento ai server basati su SQL Server ed evitare riferimenti solo ai nomi host. Specificare ad esempio sqlbe01.contoso.net e non SQLBE01.



Per l'installazione dei database, **Install-CsDatabase** utilizza tre metodi principali per posizionare i database sul server basato su SQL Server preparato:

  - Eseguire **Install-CsDatabase** senza DatabasePaths o UseDefaultSqlPath. Il cmdlet utilizza un algoritmo predefinito per determinare la posizione migliore per i file di log e di dati. Tale algoritmo funziona solo con le implementazioni di SQL Server autonome.

  - Eseguire **Install-CsDatabase** con il parametro DatabasePaths. L'algoritmo predefinito per ottimizzare le posizioni dei file di log e di dati non viene utilizzato se è definito il parametro DatabasePaths. Tale parametro consente di definire le posizioni in cui verranno distribuiti i file di log e di dati.

  - Eseguire **Install-CsDatabase** con UseDefaultSqlPaths. Questa opzione non utilizza l'algoritmo predefinito per ottimizzare le posizioni dei file di log e di dati. Tali file vengono distribuiti in base ai valori predefiniti impostati dall'amministratore di SQL Server. Questi percorsi in genere vengono impostati per consentire in anticipo l'amministrazione automatica dei file di log e di dati su SQL Server e non sono associati all'installazione di Lync Server 2013.

  - È inoltre possibile utilizzare il parametro DatabasePathMap per specificare in modo esplicito un percorso per ogni database e il relativo file di log.

## Per utilizzare i cmdlet di Windows PowerShell per configurare l' archivio di gestione centrale di SQL Server

1.  Su un computer qualsiasi accedere con le credenziali amministrative per la creazione dei database sul server basato su SQL Server. Per informazioni dettagliate, vedere [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).

2.  Aprire Lync Server 2013 Management Shell. Se il criterio di esecuzione di Windows PowerShell non è stato modificato, è necessario procedere in tal senso per consentire l'esecuzione degli script di Windows PowerShell. Per informazioni dettagliate, vedere "Analisi del criterio di esecuzione" all'indirizzo <http://go.microsoft.com/fwlink/?linkid=203093>.

3.  Utilizzare il cmdlet di **Install-CsDatabase** per installare l' archivio di gestione centrale.
    
    ```
    Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn <fully qualified domain name of SQL Server> 
    -SqlInstanceName <named instance> -DatabasePaths <logfile path>,<database file path> 
    -Report <path to report file>
    ```
    ```
    Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn sqlbe.contoso.net -SqlInstanceName rtc -DatabasePaths "C:\CSDB-Logs","C:\CSDB-CMS" -Report "C:\Logs\InstallDatabases.html"
    ```

    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il parametro Report è facoltativo ma è utile per documentare il processo di installazione.</td>
    </tr>
    </tbody>
    </table>


4.  **Install-CsDatabase –DatabasePaths** supporta fino a sei parametri di percorso, ognuno dei quali definisce i percorsi per le unità definite nell'articolo relativo al posizionamento dei file di log e dei file di dati di SQL Server. In base alle regole logiche per la configurazione dei database definite in Lync Server 2013, le unità vengono suddivise in bucket di due, quattro o sei. A seconda della configurazione di SQL Server e del numero di bucket, sarà necessario specificare due, quattro o sei percorsi.
    
    Se si dispone di tre unità, il log ha la priorità e i file di dati vengono distribuiti successivamente. Di seguito è riportato un esempio di un server basato su SQL Server configurato con sei unità:
    
        Install-CsDatabase -ConfiguredDatases -SqlServerFqdn sqlbe.contoso.net -DatabasePaths "D:\CSDynLogs","E:\CSRtcLogs","F:\MonCdrArcLogs","G:\MonCdrArchData","H:\AbsAppLog","I:\DynRtcAbsAppData" -Report "C:\Logs\InstallDatabases.html"

5.  Al termine dell'installazione dei database, è possibile chiudere Lync Server 2013 Management Shell o procedere all'installazione dei database configurati di Lync Server 2013 definiti in Generatore di topologie.

## Per utilizzare i cmdlet di Windows PowerShell per configurare i database definiti nella topologia di SQL Server

1.  Per installare i database configurati di Generatore di topologie per Lync Server 2013, è necessario che l'amministratore di Lync Server 2013 pubblichi la topologia. Per informazioni dettagliate, vedere [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md) nella documentazione relativa alla distribuzione.

2.  Eseguire l'accesso a un computer qualsiasi con le credenziali amministrative per la creazione dei database nel server basato su SQL Server. Vedere l'argomento [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Per poter configurare i database basati su SQL Server, verificare che l'account dell'amministratore di SQL Server utilizzato per eseguire i passaggi descritti in questo argomento sia anche un membro del gruppo sysadmins (o equivalente) sul server che esegue SQL Server e che abbia il ruolo server di gestione centrale. Queste informazioni sono estremamente importanti per gli eventuali pool di Lync Server 2013 aggiuntivi che richiedono l'installazione e la configurazione dei database di SQL Server. Se, ad esempio, si distribuisce un secondo pool (pool02) ma il ruolo server di gestione centrale è assegnato a pool01, il gruppo sysadmin di SQL Server (o equivalente) deve disporre delle autorizzazioni su entrambi i database basati su SQL Server.</td>
    </tr>
    </tbody>
    </table>


3.  Aprire Lync Server 2013 Management Shell, se non è già aperto.

4.  Utilizzare il cmdlet di **Install-CsDatabase** per installare i database configurati di Generatore di topologie.
    
    ```
    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn <fully qualified domain name of SQL Server> 
     -DatabasePaths <logfile path>,<database file path> -Report <path to report file>
    ```
    ```
    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn sqlbe.contoso.net 
    -Report "C:\Logs\InstallDatabases.html"
    ```
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il parametro Report è facoltativo ma è utile per documentare il processo di installazione.</td>
    </tr>
    </tbody>
    </table>


5.  Al termine dell'installazione dei database, chiudere Lync Server 2013 Management Shell.

## Per utilizzare i cmdlet di Windows PowerShell per configurare la topologia di SQL Server utilizzando il parametro DatabasePathMap

1.  Per installare database per Lync Server 2013, l'amministratore di Lync Server deve creare i percorsi e distribuire i file di database e i file di log secondo un insieme predefinito di regole.

2.  Eseguire l'accesso a un computer qualsiasi con le credenziali amministrative per la creazione dei database nel server basato su SQL Server. Vedere l'argomento [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Per poter configurare i database basati su SQL Server, verificare che l'account dell'amministratore di SQL Server utilizzato per eseguire i passaggi descritti in questo argomento sia anche un membro del gruppo sysadmins (o equivalente) sul server che esegue SQL Server e che abbia il ruolo server di gestione centrale. Queste informazioni sono estremamente importanti per gli eventuali pool di Lync Server aggiuntivi che richiedono l'installazione e la configurazione dei database di SQL Server. Se, ad esempio, si distribuisce un secondo pool (pool02) ma il ruolo server di gestione centrale è assegnato a pool01, il gruppo sysadmin di SQL Server (o equivalente) deve disporre delle autorizzazioni su entrambi i database basati su SQL Server.</td>
    </tr>
    </tbody>
    </table>


3.  Aprire Lync Server Management Shell, se non è già aperto.

4.  Utilizzare il cmdlet **Install-CsDatabase** con il parametro DatabasePathMap e una tabella hash di PowerShell per installare i database configurati in Generatore di topologie.

5.  Nel codice di esempio i percorsi definiti per i database possono essere determinati in modo granulare utilizzando il parametro -DatabasePathsMap e una tabella hash definita, come indicato di seguito. Nell'esempio vengono utilizzati il percorso "C:\\CSData" per tutti i file di database (con estensione mdf) e il percorso "C:\\CSLogFiles" per tutti i file di log (con estensione ldf). La cartella verrà creata in base alle esigenze da Install-CsDatabase:
    
        $pathmap = @{
        "BackendStore:BlobStore:DbPath"="C:\CsData";"BackendStore:BlobStore:LogPath"="C:\CsLogFiles"
        "BackendStore:RtcSharedDatabase:DbPath"="C:\CsData";"BackendStore:RtcSharedDatabase:LogPath"="C:\CsLogFiles"
        "ABSStore:AbsDatabase:DbPath"="C:\CsData";"ABSStore:AbsDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:RgsConfigDatabase:DbPath"="C:\CsData";"ApplicationStore:RgsConfigDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:RgsDynDatabase:DbPath"="C:\CsData";"ApplicationStore:RgsDynDatabase:LogPath"="C:\CsLogFiles"
        "ApplicationStore:CpsDynDatabase:DbPath"="C:\CsData";"ApplicationStore:CpsDynDatabase:LogPath"="C:\CsLogFiles"
        "ArchivingStore:ArchivingDatabase:DbPath"="C:\CsData";"ArchivingStore:ArchivingDatabase:LogPath"="C:\CsLogFiles"
        "MonitoringStore:MonitoringDatabase:DbPath"="C:\CsData";"MonitoringStore:MonitoringDatabase:LogPath"="C:\CsLogFiles"
        "MonitoringStore:QoEMetricsDatabase:DbPath"="C:\CsData";"MonitoringStore:QoEMetricsDatabase:LogPath"="C:\CsLogFiles"
        }
        Install-CsDatabase -ConfigureDatabases -SqlServerFqdn sqlbe01.contoso.net -DatabasePathsMap $pathmap

6.  Poiché i file di database e di log vengono denominati in modo esplicito con il relativo percorso nel server di database di destinazione, è possibile definire percorsi specifici per i database e i log effettivi di ogni tipo di servizio. Nell'esempio seguente i database di ogni tipo di servizio specifico vengono posizionati su dischi separati e i file di log su altri dischi, ad esempio:
    
      - Tutti i database RTC in "D:\\RTCDatabase"
    
      - Tutti i file di log RTC in "E:\\RTCLogs"
    
      - Tutti i database dell'archivio applicazioni in "F:\\CPSDatabases"
    
      - Tutti i log dell'archivio applicazioni in "G:\\CPSLogs"
    
      - Tutti i database dell'archivio di Response Group in "H:\\RGSDatabases"
    
      - Tutti i log dell'archivio di Response Group in "I:\\RGSLogs"
    
      - Tutti i database dell'archivio rubriche in "J:\\ABSDatabases"
    
      - Tutti i file di log dell'archivio rubriche in "K:\\ABSLogs"
    
      - Tutti i database dell'archivio di archiviazione in "L:\\ArchivingDatabases"
    
      - Tutti i log dell'archivio di archiviazione in "M:\\ArchivingLogs"
    
      - Tutti i database dell'archivio di monitoraggio in "N:\\MonitoringDatabases"
    
      - Tutti i file di log dell'archivio di monitoraggio in "O:\\MonitoringLogfiles"
    
    <!-- end list -->
    
    ``` 
    
    $pathmap = @{
    "BackendStore:BlobStore:DbPath"="D:\RTCDatabase";"BackendStore:BlobStore:LogPath"="E:\RTCLogs"
    "BackendStore:RtcSharedDatabase:DbPath"="D:\RTCDatabase";"BackendStore:RtcSharedDatabase:LogPath"="E:\RTCLogs"
    "ABSStore:AbsDatabase:DbPath"="J:\ABSDatabases";"ABSStore:AbsDatabase:LogPath"="K:\ABSLogs"
    "ApplicationStore:RgsConfigDatabase:DbPath"="H:\RGSDatabases";"ApplicationStore:RgsConfigDatabase:LogPath"="G:\CPSLogs"
    "ApplicationStore:RgsDynDatabase:DbPath"="H:\RGSDatabases";"ApplicationStore:RgsDynDatabase:LogPath"="I:\RGSLogs"
    "ApplicationStore:CpsDynDatabase:DbPath"="F:\CPSDatabases";"ApplicationStore:CpsDynDatabase:LogPath"="G:\CsLogFiles"
    "ArchivingStore:ArchivingDatabase:DbPath"="M:\ArchivingLogs";"ArchivingStore:ArchivingDatabase:LogPath"="N:\MonitoringDatabases"
    "MonitoringStore:MonitoringDatabase:DbPath"="N:\MonitoringDatabases";"MonitoringStore:MonitoringDatabase:LogPath"="O:\MonitoringLogfiles"
    "MonitoringStore:QoEMetricsDatabase:DbPath"="N:\MonitoringDatabases";"MonitoringStore:QoEMetricsDatabase:LogPath"="O:\MonitoringLogfiles"
    }
    
    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn sqlbe01.contoso.net -DatabasePathMap $pathmap
    ```
    
    Utilizzando il parametro -DatabasePathMap, è possibile definire una combinazione di mapping di lettere di unità logiche che offre la soluzione ottimale per i requisiti di posizionamento e di prestazioni di SQL Server.

Se si configurano i file di dati e i file di log dei database utilizzando il metodo **DatabasePathMap**, sarà necessario apportare una leggera modifica al normale processo in Generatore di topologie. In genere si definiscono le opzioni per la topologia, si pubblica la topologia e si sceglie di distribuire i database.

Se è stato utilizzato **DatabasePathMap**, è già stata eseguita la terza parte del processo di Generatore di topologie. Se si dispone di un server di database completamente configurato prima dell'esecuzione di Generatore di topologie, sarà comunque necessario definire tutti i ruoli del server e le opzioni, deselezionando però l'opzione di creazione dei database.

