---
title: Get-CsReportingConfiguration
TOCTitle: Get-CsReportingConfiguration
ms:assetid: e777a154-354a-49da-8140-79f80416bc49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205356(v=OCS.15)
ms:contentKeyID: 49302297
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsReportingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione dei rapporti in uso nell'organizzazione. Le impostazioni di configurazione dei rapporti consentono di specificare l'URL utilizzato per accedere ai rapporti di monitoraggio di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsReportingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsReportingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni per tutte le impostazioni di configurazione della creazione di rapporti attualmente in uso nell'organizzazione.

    Get-CsReportingConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per una sola raccolta di impostazioni di configurazione della creazione di rapporti: le impostazioni con identità "Service:MonitoringDatabase:atl-sql-001.litwareinc.com".

    Get-CsReportingConfiguration -Identity "Service:MonitoringDatabase:atl-sql-001.litwareinc.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni per tutte le impostazioni di configurazione della creazione di rapporti la cui identità termina con ".litwareinc.com". A tal fine, il comando utilizza il parametro Filter e il valore di filtro "\*.litwareinc.com".

    Get-CsReportingConfiguration -Filter "*.litwareinc.com"

## Esempio 4

Nell'esempio 4 vengono restituite informazioni per tutte le impostazioni di configurazione della creazione di rapporti che includono il valore di stringa "\_ARCHINST" in qualsiasi punto del loro URL dei rapporti. A tale fine, il comando utilizza innanzitutto il cmdlet **Get-CsReportingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione dei rapporti attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo le impostazioni in cui ReportingUrl include (-like) il valore di stringa "\_ARCHINST".

    Get-CsReportingConfiguration | Where-Object {$_.ReportingUrl -like "*_ARCHINST*"}

## Descrizione dettagliata

Le impostazioni di configurazione dei rapporti vengono utilizzate per specificare la home page dei rapporti di monitoraggio di Lync Server. Se non si utilizzano i rapporti di monitoraggio, non è necessario modificare le impostazioni di configurazione dei rapporti.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsReportingConfiguration

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsReportingConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare le impostazioni di configurazione della creazione di rapporti da restituire. Ad esempio, con questa sintassi vengono restituite tutte le impostazioni configurate nell'ambito del servizio:</p>
<p>-Filter &quot;service:*&quot;</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità servizio del database di monitoraggio associato alle impostazioni di configurazione della creazione di rapporti. Ad esempio:</p>
<p>-Identity &quot;Service:MonitoringDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>Se non si include né il parametro Identity né il parametro Filter nel comando, il cmdlet <strong>Get-CsReportingConfiguration</strong> restituirà tutte le impostazioni di configurazione della creazione di rapporti in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della creazione di rapporti dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsReportingConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsReportingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Reporting.ReportingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsReportingConfiguration](new-csreportingconfiguration.md)  
[Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)  
[Set-CsReportingConfiguration](set-csreportingconfiguration.md)

