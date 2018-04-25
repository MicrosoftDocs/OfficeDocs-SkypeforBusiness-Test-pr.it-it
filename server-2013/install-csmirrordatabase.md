---
title: Install-CsMirrorDatabase
TOCTitle: Install-CsMirrorDatabase
ms:assetid: 6e3acdfb-39da-4aa4-b125-1ea542971da3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204986(v=OCS.15)
ms:contentKeyID: 49300912
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Install-CsMirrorDatabase

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Associa un database mirror a un database di Lync Server 2013. Un database mirror consente di disporre contemporaneamente di due copie di uno stesso database che risiedono ognuna in un server diverso. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Install-CsMirrorDatabase -ConfiguredDatabases <SwitchParameter> -SqlServerFqdn <Fqdn> [-ForDefaultInstance <SwitchParameter>] [-ForInstance <String>] <COMMON PARAMETERS>

    Install-CsMirrorDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileShare <String> [-Confirm [<SwitchParameter>]] [-DatabasePathMap <Hashtable>] [-DropExistingDatabasesOnMirror <SwitchParameter>] [-ExcludeDatabaseList <String[]>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 installa qualsiasi database predefinito. Il parametro ConfiguredDatabases indica al cmdlet **Install-CsMirrorDatabase** di usare la topologia corrente per determinare quali database installare.

    Install-CsMirrorDatabase -ConfiguredDatabases -FileShare "\\atl-fs-001\DbBackup" -SqlServerFqdn "atl-primary-001.litwareinc.com" -DropExisitingDatabasesOnMirror

## Descrizione dettagliata

I database mirror consentono di disporre contemporaneamente di due copie di uno stesso database. Quando vengono scritti dati nel database A, una copia degli stessi dati viene scritta anche nel relativo database mirror. In questo modo è possibile sostituire immediatamente il database A qualora risulti non disponibile. Il "failover" nel database mirror viene eseguito con un disagio minimo per gli utenti e con una perdita minima di dati. Dopo aver installato i database primari, è possibile installare e configurare i database mirror usando il cmdlet **Install-CsMirrorDatabase**.

Per impostazione predefinita, il cmdlet **Install-CsMirrorDatabase** installa e configura database mirror di tutti i database di Lync Server contenuti nel server specificato. È tuttavia possibile usare i parametri DatabaseType ed ExcludeDatabaseList per specificare i database mirror che si desidera o non si desidera installare. DatabaseType consente di specificare solo i database da installare, mentre ExcludeDatabaseList consente di specificare i database da non installare.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Install-CsMirrorDatabase"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Install-CsMirrorDatabase** non sono disponibili in Pannello di controllo di Lync Server.

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
<td><p><em>ConfiguredDatabases</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Legge le informazioni dalla topologia di Lync Server e installa i database mirror necessari nel computer SQL Server o nel cluster SQL Server specificato.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>Tipo di database mirror da installare. I valori consentiti sono:</p>
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
<tr class="odd">
<td><p><em>FileShare</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso UNC della cartella condivisa del database. La condivisione di file viene usata per esportare i database dal server SQL primario e importarli nel mirror.</p>
<p>Una volta stabilito il mirroring, la cartella condivisa e il relativo contenuto possono essere eliminati. La cartella deve essere eliminata anche qualora si decida di disabilitare il mirroring.</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer SQL Server principale, ad esempio:</p>
<p>-SqlServerFqdn atl-sql-001.litwareinc.com</p></td>
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
<td><p><em>DropExistingDatabasesOnMirror</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro elimina le eventuali copie esistenti dei database con mirroring dal server che funziona come mirror prima che vengano copiati nuovi dati nel server.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeDatabaseList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco di database che non devono essere inclusi nel database mirror. Per specificare più database, separarli con virgole, ad esempio:</p>
<p>-ExcludeDatabaseList &quot;RTCCAB&quot;,&quot;RTCPROV&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ForDefaultInstance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene specificato, indica al cmdlet <strong>Install-CsMirrorDatabase</strong> di agire soltanto sull'istanza predefinita di SQL Server. Non è possibile utilizzare ForDefaultInstance e ForInstance nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ForInstance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se questo parametro viene specificato, indica al cmdlet <strong>Install-CsMirrorDatabase</strong> di agire soltanto sull'istanza specificata di SQL Server. Non è possibile utilizzare ForInstance e ForDefaultInstance nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -</p>
<p>Report &quot;C:\Logs\InstallDatabaseMirror.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'istanza del database in cui il database deve essere installato. Un'istanza del database è semplicemente un set di processi in esecuzione che forniscono accesso ai file di database. Se questo parametro viene omesso, il cmdlet <strong>Install-CsMirrorDatabase</strong> utilizzerà l'istanza predefinita di SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Install-CsMirrorDatabase** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

