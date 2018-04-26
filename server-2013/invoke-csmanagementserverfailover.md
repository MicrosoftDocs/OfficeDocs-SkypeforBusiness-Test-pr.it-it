---
title: Invoke-CsManagementServerFailover
TOCTitle: Invoke-CsManagementServerFailover
ms:assetid: 060ab02a-1267-4b35-bc2b-6a4a35616be0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204647(v=OCS.15)
ms:contentKeyID: 49299559
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsManagementServerFailover

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Richiama il processo mediante il quale viene eseguito il failover dell'archivio di gestione centrale di Lync Server 2013. Quando viene eseguito il failover dell'archivio di gestione centrale, il database primario viene sostituito da un database mirror preassegnato o da un database di backup specificato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsManagementServerFailover -BackupSqlServerFqdn <Fqdn> -Force <SwitchParameter> [-BackupMirrorSqlInstanceName <String>] [-BackupMirrorSqlServerFqdn <Fqdn>] [-BackupSqlInstanceName <String>] <COMMON PARAMETERS>

    Invoke-CsManagementServerFailover [-Restore <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 esegue il failover dell'archivio di gestione centrale per Lync Server 2013. In questo caso l'archivio di gestione esistente verrà sostituito dall'istanza del database RTC presente nel computer redmond-cs-001.litwareinc.com.

    Invoke-CsManagementServerFailover -BackupSqlServerFqdn "redmond-cs-001.litwareinc.com" - BackupSqlInstanceName "RTC" -Force

## Descrizione dettagliata

Il cmdlet **Invoke-CsManagementServerFailover** consente agli amministratori di eseguire il "failover" del server di gestione centrale. Il cmdlet **Invoke-CsManagementServerFailover** offre due metodi diversi per il failover del server di gestione centrale: 1) è possibile eseguire il failover a un'istanza di backup di SQL Server specificata o 2) è possibile eseguire il failover a un database mirror preassegnato. Per il failover a un'istanza di backup specificata, utilizzare i parametri BackupSqlServerFqdn e BackupSqlInstanceName. Per il failover al database mirror, utilizzare i parametri BackupMirrorSqlServerFqdn e BackupMirrorSqlInstanceName.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsManagementServerFailover"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsManagementServerFailover** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>BackupSqlServerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del computer che ospita il database di backup di SQL Server. Questo parametro è obbligatorio se si esegue il cmdlet <strong>Invoke-CsManagementServerFailover</strong> in modalità di ripristino di emergenza.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando. Questo parametro è obbligatorio se si esegue il cmdlet <strong>Invoke-CsManagementServerFailover</strong> in modalità di ripristino di emergenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupMirrorSqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Istanza di SQL Server del database mirror.</p></td>
</tr>
<tr class="even">
<td><p><em>BackupMirrorSqlServerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del computer che ospita il database mirror di SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupSqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Istanza di SQL Server del database di backup.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio: -Report &quot;C:\Logs\CMSFailover.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Restore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, ripristina il database server di gestione centrale esistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Invoke-CsManagementServerFailover** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Invoke-CsDatabaseFailover](invoke-csdatabasefailover.md)

