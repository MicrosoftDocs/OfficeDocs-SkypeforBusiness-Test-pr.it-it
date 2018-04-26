---
title: Invoke-CsQoEDatabasePurge
TOCTitle: Invoke-CsQoEDatabasePurge
ms:assetid: c4cae63a-b9dd-485b-8d53-2d81d353b7c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205247(v=OCS.15)
ms:contentKeyID: 49301894
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsQoEDatabasePurge

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Cancella manualmente i record dal database QoE (Quality of Experience, qualità percepita dagli utenti). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsQoEDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsQoEDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeQoEDataOlderThanDays <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Tramite il comando illustrato nell'esempio 1 vengono cancellati tutti i record QoE con data anteriore a più di 10 giorni dal database di monitoraggio su atl-sql-001.litwareinc.com.

    Invoke-CsQoEDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeQoEDataOlderThanDays 10

## ESEMPIO 2

Il comando illustrato nell'esempio 2 è una variazione del comando illustrato nell'esempio 1. In questo caso, tuttavia, il parametro Confirm viene aggiunto utilizzando la sintassi seguente:

\-Confirm:$False

Tramite questa sintassi vengono cancellate le richieste di conferma che normalmente vengono visualizzate quando si cancellano i record QoE.

    Invoke-CsQoEDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeQoEDataOlderThanDays 10 -Confirm:$False

## ESEMPIO 3

Nell'esempio 3 vengono cancellati tutti i record QoE con data anteriore a 10 giorni da tutti i database QoE di monitoraggio utilizzati nell'organizzazione. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **Get-CsService** e il parametro MonitoringDatabase per restituire una raccolta di tutti i database di monitoraggio. Questa raccolta viene quindi inviata tramite pipeline al cmdlet **ForEach-Object**. A sua volta, **ForEach-Object** accetta ogni database nella raccolta ed esegue il cmdlet **Invoke-CsQoEDatabasePurge** sul database per eliminare tutti i record QoE con data anteriore a 10 giorni.

    Get-CsService -MonitoringDatabase | Invoke-CsQoEDatabasePurge -PurgeQoEDataOlderThanDays 10 -Confirm:$False

## Descrizione dettagliata

La metrica QoE registra la qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e il livello di "instabilità" (differenze nel ritardo dei pacchetti). Questa metrica viene archiviata in un database separatamente rispetto ad altri dati, ad esempio la registrazione dettagli chiamata, in modo che sia possibile abilitare e disabilitare il servizio QoE in maniera indipendente rispetto ad altre registrazioni di dati.

La registrazione QoE viene archiviata nel database di SQL Server LcsQoEMetrics. Poiché nel tempo è possibile che questo database raggiunga dimensioni elevate, in Lync Server sono disponibili per gli amministratori due modi per eliminare i record meno recenti dal database: 1) è possibile configurare Lync Server in modo che i record QoE meno recenti vengano eliminati automaticamente ogni giorno e/o 2) è possibile utilizzare il cmdlet **Invoke-CsQoEDatabasePurge** in qualsiasi momento per eliminare i record QoE dal database LcsQoEMetrics. A tale scopo, il cmdlet **Invoke-CsQoEDatabasePurge** chiama la stored procedure di SQL Server QoePurgeOutdatedReports.

Quando si chiama il cmdlet **Invoke-CsQoEDatabasePurge**, è necessario specificare la posizione del servizio del database di monitoraggio in cui sono archiviati i record QoE, ad esempio MonitoringDatabase:atl-sql-001.litwareinc.com. È inoltre necessario indicare la durata minima (in giorni) dei record da eliminare. Se ad esempio si specifica una durata minima di 10 giorni, verranno eliminati dal database tutti i record QoE creati da più di 10 giorni.

Questi record verranno eliminati anche se per il database specificato è stata disabilitata l'eliminazione, ovvero se nelle impostazioni di configurazione di QoE la proprietà EnablePurging è stata impostata su False. La proprietà EnablePurging controlla solo l'eliminazione automatica dei record di archiviazione e non ha effetto sul cmdlet **Invoke-CsQoEDatabasePurge**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsQoEDatabasePurge"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsQoEDatabasePurge** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identità del servizio del database di monitoraggio di cui cancellare i record. È possibile recuperare le identità per i database di monitoraggio eseguendo questo comando:</p>
<p>Get-CsService –MonitoringDatabase</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e SqlServerFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeQoEDataOlderThanDays</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica l'età (in giorni) dei record QoE da cancellare dal database; tutti i record con data anteriore a questo valore verranno cancellati.</p>
<p>PurgeQoEDataOlderThanHours può essere impostato su qualsiasi valore intero compreso tra 1 e 2147483647 incluso.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del computer in cui è contenuto il database QoE, ad esempio:</p>
<p>-SqlServerFqdn &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e SqlServerFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza di SQL Server per il database QoE, ad esempio:</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe se si eseguisse il comando senza eseguirlo effettivamente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Invoke-CsQoEDatabasePurge** accetta le istanze da pipeline della classe Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase\#Decorated.

## Tipi restituiti

Il cmdlet **Invoke-CsQoEDatabasePurge** restituisce istanze della classe Microsoft.Rtc.Management.Purge.QoEDataPurgeStatistics.

## Vedere anche

#### Ulteriori risorse

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)

