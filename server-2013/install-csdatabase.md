---
title: Install-CsDatabase
TOCTitle: Install-CsDatabase
ms:assetid: e91c1800-35f6-40ef-840d-7a518bddcae6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399044(v=OCS.15)
ms:contentKeyID: 49302352
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsDatabase

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Installa uno o più database di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Install-CsDatabase -LocalDatabases <SwitchParameter> [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsDatabase -CentralManagementDatabase <SwitchParameter> -SqlServerFqdn <Fqdn> [-Backup <SwitchParameter>] [-Collocated <SwitchParameter>] [-SqlInstanceName <String>] <COMMON PARAMETERS>

    Install-CsDatabase -ConfiguredDatabases <SwitchParameter> -SqlServerFqdn <Fqdn> [-ExcludeCollocatedStores <SwitchParameter>] [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> [-Collocated <SwitchParameter>] [-SqlInstanceName <String>] [-SqlServerFqdn <Fqdn>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Clean <SwitchParameter>] [-Confirm [<SwitchParameter>]] [-DatabasePathMap <Hashtable>] [-DatabasePaths <String[]>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-NoReindex <SwitchParameter>] [-Report <String>] [-SkipPrepareCheck <SwitchParameter>] [-Update <SwitchParameter>] [-UseDefaultSqlPaths <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Install-CsDatabase** legge nella topologia di Lync Server e quindi installa tutti i database necessari nel pool atl-sql-001.litwareinc.com.

    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn atl-sql-001.litwareinc.com -DatabasePaths "E:\CSLog","F:\CSLog","G:\CSDB"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 installa l'archivio di gestione centrale nel pool atl-sql-001.litwareinc.com. Il database verrà installato nell'istanza RTC e utilizzerà la cartella G:\\CSDB.

    Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName rtc -DatabasePaths "G:\CSDB"

## Descrizione dettagliata

In Lync Server viene fatto un ampio uso dei database SQL Server, dall'archivio di gestione centrale al database di archiviazione. Come norma generale, tali database vengono impostati al momento dell'installazione di Lync Server o quando si installa un ruolo di Lync Server (quale ad esempio Monitoring Server) che richiede un back-end del database. Dopo l'installazione, di solito non è necessario reinstallare o spostare questi database.

In rare occasioni potrebbe tuttavia essere necessario installare manualmente un database di Lync Server, ad esempio perché un database deve essere spostato in un altro server o perché si è verificato un problema di impostazione che ha impedito l'installazione del database. Il cmdlet **Install-CsDatabase** consente di installare qualsiasi database SQL Server utilizzato da Lync Server.

Quando si esegue il cmdlet **Install-CsDatabase**, fondamentalmente è possibile gestire la configurazione del database da installare in tre modi diversi:

Opzione 1 - Eseguire il cmdlet senza includere un parametro che specifichi i percorsi di database. Quando si esegue il cmdlet **Install-CsDatabase** senza il parametro DatabasePath o UseDefaultSqlPath, viene utilizzato un algoritmo predefinito per scegliere il percorso di archiviazione dei file di dati e dei log di database. Si noti che tale algoritmo predefinito funziona con un server SQL Server autonomo e non con un cluster di SQL Server. Per poter installare un database in un cluster di SQL Server, è necessario includere nel comando il parametro DatabasePath o UseDefaultSqlPath.

Opzione 2 - Eseguire il cmdlet con il parametro DatabasePath. Quando si esegue il cmdlet **Install-CsDatabase** con il parametro DatabasePath, non viene utilizzato l'algoritmo predefinito per scegliere il percorso di archiviazione dei file di dati e dei log di database. Tale percorso può invece essere selezionato dagli amministratori. Per installare i file di dati e i log di SQL Server nello stesso percorso, è sufficiente specificare il percorso della cartella in cui devono essere archiviati questi dati. Ad esempio:

\-DatabasePath C:\\SqlData

Per archiviare i file di dati e i file di log in due percorsi diversi, specificare il percorso dell'una e dell'altra cartella utilizzando una virgola come carattere di separazione. Prestare attenzione a non inserire uno spazio prima o dopo la virgola:

\-DatabasePath C:\\SqlLogs,D:\\SqlData

I file di log verranno sempre archiviati nel primo percorso specificato, mentre i file di dati verranno archiviati nel secondo.

Nel back-end di un pool alcuni file di log potrebbero essere archiviati da soli in un'unità disco. Se il back-end del pool dispone di un'unica unità, i file verranno distribuiti come indicato di seguito:

Unità 1 - Log Rtcdyn, log Rtc, altri log, altri dati.

Se si dispone di due unità, i file verranno distribuiti come indicato di seguito:

Unità 1 - Log Rtcdyn, log Rtc.

Unità 2 - Altri log, altri dati.

Con tre unità:

Unità 1 - Log Rtcdyn.

Unità 2 - Log Rtc.

Unità 3 - Altri log, altri dati.

E con quattro unità:

Unità 1 - Log Rtcdyn.

Unità 2 - Log Rtc.

Unità 3 - Altri log.

Unità 4 - Altri dati.

Opzione 3 - Eseguire il cmdlet con il parametro UseDefaultSqlPaths. Quando si esegue il cmdlet **Install-CsDatabase** con il parametro UseDefaultSqlPaths, non viene utilizzato l'algoritmo predefinito per scegliere i percorsi di archiviazione dei file di dati e dei log di database. Tali file vengono invece archiviati nei percorsi predefiniti di SQL Server, configurati preventivamente da un amministratore di SQL Server. I file di dati verranno perciò archiviati nel percorso dei file di dati predefinito di SQL Server, mentre i file di log verranno archiviati nel percorso dei file di log predefinito di SQL Server.

Prima di eseguire il cmdlet **Install-CsDatabase**, è consigliabile verificare che il gruppo RTCUniversalServerAdmins non sia stato assegnato come proprietario del database. Se tale gruppo risulta elencato come proprietario, potrebbe essere eliminato alla chiamata del cmdlet **Install-CsDatabase**.

Utenti autorizzati a eseguire il cmdlet: per eseguire il cmdlet **Install-CsDatabase** in locale, è necessario essere membri del dominio, membri del gruppo RTCUniversalReadOnlyAdmins, amministratori di SQL Server e amministratori locali nel computer in cui è installato SQL Server. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Install-CsDatabase"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CentralManagementDatabase</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene incluso, il cmdlet <strong>Install-CsDatabase</strong> utilizzerà il parametro SqlServerFqdn per installare l'archivio di gestione centrale nel computer specificato. Tale parametro di solito viene utilizzato esclusivamente dallo Generatore di topologie e generalmente viene chiamato solo una volta, durante l'impostazione iniziale.</p></td>
</tr>
<tr class="even">
<td><p><em>ConfiguredDatabases</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Legge le informazioni della topologia di Lync Server e installa i database necessari nel computer SQL Server o nel cluster di SQL Server specificato. Gli amministratori che devono chiamare il cmdlet <strong>Install-CsDatabase</strong> utilizzeranno quasi sempre questo parametro al momento di specificare i database da installare.</p></td>
</tr>
<tr class="odd">
<td><p><em>DatabaseType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>Consente di installare un database specifico in un computer SQL Server o cluster di SQL Server specifico. Come norma generale, gli amministratori non dovrebbero eseguire il cmdlet <strong>Install-CsDatabase</strong> con il parametro DatabaseType, a meno che non siano state fornite istruzioni in merito dal personale di supporto Microsoft. Dovrebbero invece utilizzare di solito il parametro ConfiguredDatabases. Con il parametro DatabaseType è necessario conoscere il tipo e il percorso esatti di ciascun database utilizzato nella topologia. Tale parametro inoltre è richiesto soltanto se l'esecuzione del comando del cmdlet <strong>Install-CsDatabase</strong> con il parametro ConfiguredDatabases ha esito negativo.</p>
<p>I valori validi per DatabaseType sono i seguenti:</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Edge</p>
<p>Lyss</p>
<p>Monitoring</p>
<p>PersistentChat</p>
<p>PersistentChatCompliance</p>
<p>Provision</p>
<p>Registrar</p>
<p>User</p></td>
</tr>
<tr class="even">
<td><p><em>LocalDatabases</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene incluso, il cmdlet <strong>Install-CsDatabase</strong> leggerà nella topologia di Lync Server e installerà i database e gli archivi come necessario nel computer locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer in cui deve essere installato il database. Ad esempio: -SqlServerFqdn atl-sql-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Backup</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando viene utilizzato, esegue il backup del database del server di gestione centrale all'istanza di SQL Server specificata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Clean</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene incluso, il cmdlet <strong>Install-CsDatabase</strong> eliminerà e reinstallerà i database come necessario. Se questo parametro non viene incluso, il cmdlet <strong>Install-CsDatabase</strong> non sovrascriverà alcun database esistente. Non è possibile utilizzare Clean e Update nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Collocated</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro è presente, gli ulteriori ruoli del database verranno collocati nell'archivio di gestione centrale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabasePathMap</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.Hashtable</p></td>
<td><p>Consente di specificare percorsi di cartelle personalizzati per i file di dati e i file di log. In caso di più percorsi è necessario separarli con un punto e virgola (;). Ad esempio:</p>
<p>-DatabasePathMap @{&quot;Archiving:DbPath&quot;=&quot;\\atl-sql-001.litwareinc.com\db&quot;;&quot;Archiving:LogPath&quot;=&quot;\\atl-sql-002.litwareinc.com\logs&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>DatabasePaths</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente di specificare le unità e le cartelle in cui possono essere archiviati i file di log e i file di dati come, ad esempio, -DatabasePaths &quot;D:\Logs&quot;,&quot;E:\Data&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeCollocatedStores</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, non verrà visualizzato un messaggio di avviso indicante che eventuali archivi di database presenti devono essere installati nel computer locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, viene forzata l'installazione del nuovo database anche se un database esistente dello stesso tipo è attualmente in uso.</p></td>
</tr>
<tr class="even">
<td><p><em>ForDefaultInstance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene specificato, indica al cmdlet <strong>Install-CsDatabase</strong> di agire soltanto sull'istanza predefinita di SQL Server. Non è possibile utilizzare ForDefaultInstance e ForInstance nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ForInstance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se questo parametro viene specificato, indica al cmdlet <strong>Install-CsDatabase</strong> di agire soltanto sull'istanza specificata di SQL Server. Non è possibile utilizzare ForInstance e ForDefaultInstance nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (FQDN) di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Install-CsDatabase</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro dovrà puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, sarà possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>NoReindex</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce che i file di indice vengano ricompilati quando viene aggiornato un database. Questo parametro può essere utilizzato esclusivamente con il parametro Update.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\InstallDatabases.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, indica al cmdlet <strong>Install-CsDatabase</strong> di non eseguire le relative verifiche di preparazione iniziali.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'istanza del database in cui il database deve essere installato. Un'istanza del database è semplicemente un set di processi in esecuzione che forniscono accesso ai file di database. Se questo parametro viene omesso, il cmdlet <strong>Install-CsDatabase</strong> utilizzerà l'istanza predefinita di SQL Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Update</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, consente l'aggiornamento del database esistente. Non è possibile utilizzare Update e Clean nello stesso comando.</p>
<p>Non è possibile utilizzare il parametro Update con i database con mirroring. Il comando avrà esito negativo perché i database mirror non possono essere eliminati e ricreati. Per utilizzare il parametro Update con i database con mirroring, è necessario innanzitutto dissociare i database con mirroring utilizzando il cmdlet <a href="uninstall-csmirrordatabase.md">Uninstall-CsMirrorDatabase</a>. A questo punto è possibile eseguire Install-CsDatabase e il parametro Update.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultSqlPaths</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene specificato, indica a SQL Server di selezionare l'unità in cui archiviare i file di dati e i file di log.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Install-CsDatabase** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Install-CsDatabase** non restituisce valori o oggetti.

## Vedere anche

#### Ulteriori risorse

[Uninstall-CsDatabase](uninstall-csdatabase.md)

