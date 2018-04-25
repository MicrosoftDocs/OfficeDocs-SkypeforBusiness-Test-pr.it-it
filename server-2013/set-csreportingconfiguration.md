---
title: Set-CsReportingConfiguration
TOCTitle: Set-CsReportingConfiguration
ms:assetid: 8e7c8e8c-ab68-4f95-a58e-b04a9b2110ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205075(v=OCS.15)
ms:contentKeyID: 49301282
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsReportingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica l'URL dei rapporti per una raccolta esistente di impostazioni di configurazione dei rapporti. Tali impostazioni consentono di specificare l'URL utilizzato per accedere ai rapporti di monitoraggio di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsReportingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsReportingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 modifica l'URL dei rapporti delle impostazioni di configurazione dei rapporti con l'identità service:MonitoringDatabase:atl-sql-002.litwareinc.com. In questo esempio l'URL dei rapporti viene impostato su "https://atl-sql-002.litwareinc.com/lync\_reports".

    Set-CsReportingConfiguration -Identity "service:MonitoringDatabase:atl-sql-002.litwareinc.com" -ReportingURL "https://atl-sql-002.litwareinc.com/lync_reports"

## Descrizione dettagliata

Le impostazioni di configurazione dei rapporti vengono utilizzate per specificare la home page dei rapporti di monitoraggio di Lync Server. Se non si utilizzano i rapporti di monitoraggio, non è necessario modificare le impostazioni di configurazione dei rapporti.

Se non si conosce l'URL della home page dei rapporti di monitoraggio, è possibile determinarlo eseguendo le operazioni seguenti:

1.  Aprire Gestione configurazione Reporting Services di SQL Server per l'istanza di SQL Server in cui è contenuto il database di monitoraggio.

2.  In Gestione configurazione fare clic su **URL Gestione report** e quindi sull'URL dei rapporti di monitoraggio. Se sono visibili due URL, fare clic su quello che utilizza il protocollo HTTPS.

3.  In SQL Server Reporting Services fare clic su **LyncServerReports**.

4.  Nella pagina LyncServerReports fare clic su **Home page rapporti**. Verrà visualizzata la home page dei rapporti di monitoraggio. È quindi possibile copiare l'URL e utilizzarlo insieme ai cmdlet CsReportingConfiguration.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsReportingConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsReportingConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità del servizio del database di monitoraggio di cui vengono modificate le impostazioni di configurazione dei rapporti. Ad esempio:</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL dei rapporti di monitoraggio di Lync Server 2013.</p></td>
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

Il cmdlet **Set-CsReportingConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsReportingConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsReportingConfiguration](get-csreportingconfiguration.md)  
[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)

