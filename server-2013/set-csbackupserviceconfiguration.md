---
title: Set-CsBackupServiceConfiguration
TOCTitle: Set-CsBackupServiceConfiguration
ms:assetid: 72ed064e-5f67-481f-802a-74846cecb189
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205006(v=OCS.15)
ms:contentKeyID: 49300964
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBackupServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni di configurazione del servizio di backup per Lync Server 2013. Tali impostazioni includono il numero massimo di chiamate contemporanee di Windows Communication Framework che possono essere effettuate al servizio di backup, nonché l'intervallo di sincronizzazione del servizio. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsBackupServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsBackupServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AuthorizedLocalAccounts <String>] [-AuthorizedUniversalGroups <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxBatchesPerCmsSync <Int32>] [-MaxBatchesPerUserStoreSync <Int32>] [-MaxConcurrentCalls <Int32>] [-MaxDataConfPackageSizeKB <Int32>] [-SyncInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 assegna il gruppo di sicurezza di Active Directory denominato Schema Admins alla proprietà AuthorizedUniversalGroup per la raccolta globale di impostazioni del servizio di backup.

    Set-CsBackupServiceConfiguration -Identity "global" -AuthorizedUniversalGroup "Schema Admins"

## Esempio 2

Nell'esempio 2 la proprietà MaxConcurrentCalls della raccolta globale di impostazioni del servizio di backup viene configurata su 12.

    Set-CsBackupServiceConfiguration -Identity "global" -MaxConcurrentCalls 12

## Esempio 3

Nell'esempio 3 viene modificata la proprietà SyncInterval della raccolta globale di impostazioni del servizio di backup. In questo esempio il valore di SyncInterval viene impostato su 10 minuti (00 ore: 10 minuti: 00 secondi).

    Set-CsBackupServiceConfiguration -Identity "global" -SyncInterval "00:10:00"

## Descrizione dettagliata

Le impostazioni di configurazione del servizio di backup vengono utilizzate per gestire i backup dei pool in Lync Server 2013. Si noti che Lync Server supporta solo una singola raccolta globale di impostazioni di configurazione di backup. Questo significa tra l'altro che il backup di tutti i pool deve essere eseguito utilizzando la stessa pianificazione di sincronizzazione e che gli utenti e i gruppi autorizzati a eseguire il backup del pool A sono autorizzati a eseguire il backup anche dei pool B, C, D ed E.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBackupServiceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsBackupServiceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>AuthorizedLocalAccounts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nomi degli utenti locali o dei gruppi locali autorizzati a eseguire il servizio di backup. Il valore predefinito corrisponde a Servizio di rete.</p></td>
</tr>
<tr class="even">
<td><p><em>AuthorizedUniversalGroups</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nomi dei gruppi universali autorizzati a eseguire il servizio di backup. Il valore predefinito corrisponde a Schema Admins.</p></td>
</tr>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione del servizio di backup. Poiché è possibile avere esclusivamente una singola istanza globale di queste impostazioni, non è necessario specificare un parametro Identity quando si esegue la chiamata al cmdlet <strong>Set-CsBackupServiceConfiguration</strong>. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBatchesPerCmsSync</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero massimo di batch che il modulo di backup di CMS esporterà durante ogni ciclo di esportazione. Il valore predefinito è 500.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxBatchesPerUserStoreSync</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero massimo di batch che il modulo di backup dell'archivio utenti esporterà durante ogni ciclo di esportazione. Il valore predefinito è 500.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxConcurrentCalls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero massimo di chiamate di Windows Communication Foundation (WCF) che possono essere effettuate contemporaneamente al servizio di backup. Il valore predefinito è 10.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxDataConfPackageSizeKB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Dimensione massima, in kilobyte, del pacchetto di dati che il modulo per conferenze dati esporterà durante ogni ciclo di esportazione. Il valore predefinito è 102400.</p></td>
</tr>
<tr class="odd">
<td><p><em>SyncInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica per quanto tempo il servizio deve attendere prima di sincronizzare un pool con il relativo pool di backup. Il valore predefinito è 2 minuti, ovvero 00:02:00 (00 ore, 02 minuti e 00 secondi). Il parametro SyncInterval può essere impostato su qualsiasi valore compreso tra 5 secondi (00:00:05) e 3 ore (03:00:00) inclusi.</p></td>
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

Il cmdlet **Set-CsBackupServiceConfiguration** accetta istanze inviate tramite pipe dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsBackupServiceConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

