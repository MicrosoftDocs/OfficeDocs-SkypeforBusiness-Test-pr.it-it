---
title: Uninstall-CsDatabase
TOCTitle: Uninstall-CsDatabase
ms:assetid: bd08ac1c-cfcd-4cf8-b082-7d2e83a2837e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412922(v=OCS.15)
ms:contentKeyID: 49301805
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uninstall-CsDatabase

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina il database di Lync Server specificato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Uninstall-CsDatabase -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> [-SqlInstanceName <String>] [-SqlServerFqdn <Fqdn>] <COMMON PARAMETERS>

    Uninstall-CsDatabase -CentralManagementDatabase <SwitchParameter> -SqlServerFqdn <Fqdn> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Detach <SwitchParameter>] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 elimina l'archivio di gestione centrale dal computer atl-sql-001.litwareinc.com.

    Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn atl-sql-001.litwareinc.com 

## ESEMPIO 2

Nell'esempio 2 viene eliminato dal computer atl-sql-001.litwareinc.com il database User. Se si utilizza il parametro DatabaseType, vengono eliminati tutti gli archivi correlati al database specificato.

    Uninstall-CsDatabase -DatabaseType User -SqlServerFqdn atl-sql-001.litwareinc.com 

## Descrizione dettagliata

In Lync Server vengono utilizzati diffusamente database di SQL Server quali l'archivio di gestione centrale e il database di archiviazione. Questi database vengono configurati contestualmente all'installazione di Lync Server o di un ruolo di Lync Server che richiede un database back-end. Dopo che i database sono stati installati, di rado è necessario disinstallarli.

È tuttavia possibile che in un determinato momento sia necessario disinstallare un database di Lync Server, ad esempio se si verifica un errore hardware oppure un problema di connettività di rete che rende inutilizzabile un database esistente. Indipendentemente dal motivo, il cmdlet **Uninstall-CsDatabase** consente di rimuovere o scollegare qualsiasi database di SQL Server utilizzato da Lync Server.

Utenti autorizzati a eseguire il cmdlet: per eseguire localmente il cmdlet **Uninstall-CsDatabase** è necessario essere membri del dominio ed essere un amministratore di SQL Server e un amministratore locale nel computer in cui è installato SQL Server. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Uninstall-CsDatabase"}

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
<td><p>Se presente, disinstalla l'archivio di gestione centrale. Non è possibile utilizzare entrambi i parametri CentralManagementDatabase e DatabaseType nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>Database da eliminare. I valori validi sono:</p>
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
<p>User</p>
<p>Per eliminare l'archivio di gestione centrale, utilizzare il parametro CentralManagementDatabase.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer o del cluster di SQL Server in cui si trova il database, ad esempio -SqlServer atl-sql-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Detach</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, scollega il database specificato. Una volta scollegato il database, tutti i blocchi a livello di file imposti da SQL Server vengono rimossi. Ciò consente di accedere direttamente ai file di database, ad esempio per copiare i file in un altro computer.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, forza la rimozione del database anche se il database è attualmente in uso.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio -Report &quot;C:\Logs\UninstallDatabase.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza del database contenente il database da rimuovere. Un'istanza del database è un insieme di processi in esecuzione che consente di accedere ai file di database.</p></td>
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

Nessuno. Il cmdlet **Uninstall-CsDatabase** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Uninstall-CsDatabase** non restituisce valori o oggetti.

## Vedere anche

#### Ulteriori risorse

[Install-CsDatabase](install-csdatabase.md)

