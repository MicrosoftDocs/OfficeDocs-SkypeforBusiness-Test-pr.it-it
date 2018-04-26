---
title: Remove-CsReportingConfiguration
TOCTitle: Remove-CsReportingConfiguration
ms:assetid: 17cc1865-4bd9-4630-9947-2c432d1203b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204711(v=OCS.15)
ms:contentKeyID: 49299809
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsReportingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione dei rapporti. Le impostazioni di configurazione dei rapporti vengono utilizzate per specificare l'URL per le installazioni dei rapporti di monitoraggio di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsReportingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 vengono rimosse le impostazioni di configurazione dei rapporti con identità (Identity) service:MonitoringDatabase:atl-sql-002.litwareinc.com.

    Remove-CsReportingConfiguration -Identity "service:MonitoringDatabase:atl-sql-002.litwareinc.com"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione dei rapporti attualmente in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsReportingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione dei rapporti. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsReportingConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsReportingConfiguration | Remove-CsReportingConfiguration

## Esempio 3

Il comando riportato nell'esempio 3 elimina tutte le impostazioni di configurazione dei rapporti in cui l'URL dei rapporti è impostato su https://atl-sql-002.litwareinc.com/lync\_reports. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsReportingConfiguration** per restituire tutte le impostazioni di configurazione dei rapporti attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà ReportingURL è uguale a https://atl-sql-002.litwareinc.com/lync\_reports. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsReportingConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsReportingConfiguration | Where-Object {$_.ReportingUrl -eq "https://atl-sql-002.litwareinc.com/lync_reports" | Remove-CsReportingConfiguration

## Descrizione dettagliata

Le impostazioni di configurazione dei rapporti vengono utilizzate per specificare la home page dei rapporti di monitoraggio di Lync Server. Se non si utilizzano i rapporti di monitoraggio, non è necessario modificare le impostazioni di configurazione dei rapporti.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsReportingConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsReportingConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità del servizio del database di monitoraggio di cui devono essere rimosse le impostazioni di configurazione dei rapporti, ad esempio:</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsReportingConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsReportingConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsReportingConfiguration](get-csreportingconfiguration.md)  
[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Set-CsReportingConfiguration](set-csreportingconfiguration.md)

