---
title: Set-CsMonitoringServer
TOCTitle: Set-CsMonitoringServer
ms:assetid: 2c6d6660-7e41-4c56-9e04-27c3d1ea3b95
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425776(v=OCS.15)
ms:contentKeyID: 49300038
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMonitoringServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di configurare nuovi percorsi per il pacchetto rapporti e/o il database di Monitoring Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsMonitoringServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MonitoringDatabase <String>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di configurare un nuovo URL per il pacchetto rapporti di Monitoring Server.

    Set-CsMonitoringServer -Identity "MonitoringServer:atl-cs-001.litwareinc.com" -ReportingUrl "https://atl-cs-001.litwareinc.com/reports"

## Descrizione dettagliata

Monitoring Server dispone di due importanti funzionalità. Innanzitutto, consente di conservare le informazioni su come e con che frequenza VoIP aziendale viene utilizzato all'interno dell'organizzazione. Queste informazioni vengono monitorate utilizzando la registrazione dei dettagli delle chiamate (CDR) che fornisce dettagli. quali la persona che ha chiamato, la persona chiamata e la durata della conversazione. La conversazione non viene registrata. Inoltre, è possibile utilizzare Monitoring Server per monitorare i dati sulla qualità percepita dagli utenti (QoE) per le chiamate di VoIP aziendale. Come suggerito dal nome, i dati sulla qualità percepita dagli utenti (QoE) forniscono informazioni sulla qualità di una chiamata, valutando elementi quali il numero di pacchetti persi, la degradazione della chiamata, la velocità in bit sulla rete e l'instabilità.

Quando si installa Monitoring Server, è necessario specificare il percorso del database SQL Server utilizzato per memorizzare i dati CDR e QoE. Facoltativamente, è anche possibile installare SQL Server Reporting Services e il pacchetto rapporti di Monitoring Server; questi due componenti consentono di accedere a un sito Web che genera i rapporti di monitoraggio standard.

In generale, dopo aver installato e configurato Monitoring Server, non sarà necessario modificare il percorso del database di back-end o dell'URL dei rapporti. Tuttavia, se si desidera modificare il percorso di uno o entrambi questi elementi, è possibile utilizzare il cmdlet **Set-CsMonitoringServer**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsMonitoringServer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMonitoringServer"}

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
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Percorso di installazione del server Monitoring Server da modificare. Ad esempio: -Identity &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;. Per ottenere l'identità di tutti i server Monitoring Server, utilizzare il comando seguente:</p>
<p>Get-CsService –MonitoringServer | Select-Object Identity.</p>
<p>Si noti che è possibile non utilizzare il prefisso &quot;MonitoringServer:&quot; quando si specifica un Monitoring Server. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso di installazione del nuovo database di Monitoring Server. Ad esempio: -MonitoringDatabase &quot;MonitoringDatabase:atl-sql-001.litwareinc.com&quot;. Accertarsi di utilizzare il percorso di installazione del database e non il nome del percorso di SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL per i rapporti di Monitoring Server. Si noti che questi rapporti non risulteranno disponibili se non si installano SQL Server Reporting Services e il pacchetto rapporti di Monitoring Server.</p></td>
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

Nessuno. Il cmdlet **Set-CsMonitoringServer** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsMonitoringServer** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayMonitoringServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

