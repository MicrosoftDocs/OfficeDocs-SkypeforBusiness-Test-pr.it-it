---
title: Uninstall-CsMirrorDatabase
TOCTitle: Uninstall-CsMirrorDatabase
ms:assetid: a5b14259-6cf6-46b5-ae8d-3b5e4428dfaf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205159(v=OCS.15)
ms:contentKeyID: 49301565
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uninstall-CsMirrorDatabase

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Disinstalla un database mirror di Lync Server 2013 Management Shell. Tale database consente di disporre contemporaneamente di due copie di uno stesso database che risiedono ognuna in un server diverso. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Uninstall-CsMirrorDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] [-Confirm [<SwitchParameter>]] [-DropExistingDatabasesOnMirror <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disinstalla il database utenti dall'istanza RTC di SQL Server nel computer atl-mirror-001.litwareinc.com. Poiché è stato incluso il parametro DropExistingDatabaseOnMirror, il comando eliminerà anche l'effettivo database utenti mirror.

    Uninstall-CsMirrorDatabase -SqlServerFqdn "atl-mirror-001.litwareinc.com" -SqlInstanceName "RTC" -DatabaseType "User" -DropExistingDatabasesOnMirror

## Descrizione dettagliata

I database mirror consentono di disporre contemporaneamente di due copie di uno stesso database. Quando vengono scritti dati nel database A, una copia di tali dati viene scritta anche nel relativo database mirror. In questo modo, se il database A non è più disponibile, è possibile sostituirlo immediatamente eseguendo il "failover" nel database mirror con un disagio minimo per gli utenti e con una perdita minima di dati.

I database mirror possono essere installati e configurati usando il cmdlet [Install-CsMirrorDatabase](install-csmirrordatabase.md). Per rimuovere un database mirror, usare il cmdlet **Uninstall-CsMirrorDatabase**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Uninstall-CsMirrorDatabase"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Uninstall-CsMirrorDatabase** non sono disponibili in Pannello di controllo di Lync Server.

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
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer contenente il database da disinstallare. Ad esempio:</p>
<p>-SqlServerFqdn atl-sql-001.litwareinc.com</p>
<p>Deve essere l'FQDN del computer SQL Server principale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DropExistingDatabasesOnMirror</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, elimina le eventuali copie esistenti dei database con mirroring dal server mirror.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -</p>
<p>Report &quot;C:\Logs\UnInstallDatabaseMirror.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'istanza del database in cui il database deve essere installato. Un'istanza del database è semplicemente un set di processi in esecuzione che forniscono accesso ai file di database. Se questo parametro viene omesso, il cmdlet <strong>Uninstall-CsMirrorDatabase</strong> utilizzerà l'istanza predefinita di SQL Server.</p></td>
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

Nessuno. Il cmdlet **Uninstall-CsMirrorDatabase** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Install-CsMirrorDatabase](install-csmirrordatabase.md)

