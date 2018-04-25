---
title: Remove-CsBackupServiceConfiguration
TOCTitle: Remove-CsBackupServiceConfiguration
ms:assetid: 56bbf0a2-20cf-4f1e-b305-3521659eb909
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204903(v=OCS.15)
ms:contentKeyID: 49300621
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBackupServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Reimposta sui valori predefiniti le proprietà delle impostazioni di configurazione del servizio di backup per Lync Server 2013. Tali impostazioni includono il numero massimo di chiamate contemporanee di Windows Communication Framework che possono essere effettuate al servizio di backup, nonché l'intervallo di sincronizzazione del servizio di backup. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsBackupServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 vengono ridefinite le impostazioni di configurazione del servizio di backup per Lync Server 2013. Si noti che, nonostante Lync Server 2013 utilizzi solo una raccolta globale di impostazioni di backup, è comunque necessario includere il parametro Identity. In caso contrario, il cmdlet **Remove-CsBackupServiceConfiguration** chiederà di specificare l'identità prima di continuare.

    Remove-CsBackupServiceConfiguration -Identity "global"

## Descrizione dettagliata

Le impostazioni di configurazione del servizio di backup vengono utilizzate per gestire i backup dei pool in Lync Server 2013. Si noti che Lync Server supporta solo una raccolta globale di impostazioni di configurazione del backup. Questo significa tra l'altro che il backup di tutti i pool deve essere eseguito utilizzando la stessa pianificazione di sincronizzazione e che gli utenti e i gruppi autorizzati a eseguire il backup del pool A sono autorizzati a eseguire il backup anche dei pool B, C, D ed E.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBackupServiceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsBackupServiceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identità univoca delle impostazioni di configurazione del servizio di backup. Anche se è possibile disporre di una sola istanza globale di tali impostazioni, è comunque necessario specificare un'identità nella chiamata al cmdlet <strong>Remove-CsBackupServiceConfiguration</strong>:</p>
<p>-Identity global</p></td>
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

Il cmdlet **Remove-CsBackupServiceConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsBackupServiceConfiguration** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

