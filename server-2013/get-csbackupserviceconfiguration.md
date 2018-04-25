---
title: Get-CsBackupServiceConfiguration
TOCTitle: Get-CsBackupServiceConfiguration
ms:assetid: 8e81a76c-4019-490d-9cd5-895cc2cc0863
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205087(v=OCS.15)
ms:contentKeyID: 49301285
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBackupServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni di configurazione del servizio di backup per Lync Server 2013. Tali impostazioni includono il numero massimo di chiamate contemporanee di Windows Communication Framework che possono essere effettuate al servizio di backup, nonché l'intervallo di sincronizzazione del servizio. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsBackupServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsBackupServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 recupera le informazioni di configurazione del servizio di backup per Lync Server 2013. Poiché vi è un solo insieme globale di tali impostazioni, non è necessario includere il parametro Identity per l'esecuzione di questo comando.

    Get-CsBackupServiceConfiguration

## Descrizione dettagliata

Le impostazioni di configurazione del servizio di backup vengono utilizzate per gestire i backup dei pool in Lync Server 2013. Si noti che Lync Server supporta solo una singola raccolta globale di impostazioni di configurazione di backup. Questo significa tra l'altro che il backup di tutti i pool deve essere eseguito utilizzando la stessa pianificazione di sincronizzazione e che gli utenti e i gruppi autorizzati a eseguire il backup del pool A sono autorizzati a eseguire il backup anche dei pool B, C, D ed E.

Get-CsBackupServiceConfiguration può essere eseguito da qualsiasi computer che esegue un ruolo del server di Lync Server 2013 o da un'istanza remota di Windows PowerShell.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBackupServiceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsBackupServiceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare valori con caratteri jolly per fare riferimento a una raccolta di impostazioni di configurazione del servizio di backup. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, il parametro Filter non è necessario. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Filter &quot;g*&quot;</p>
<p>La sintassi precedente restituisce tutte le impostazioni di configurazione del servizio di backup la cui identità inizia con la lettera &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione del servizio di backup. Dal momento che è possibile disporre di una sola istanza globale di tali impostazioni, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Get-CsBackupServiceConfiguration</strong>. È tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione del servizio di backup dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsBackupServiceConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsBackupServiceConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BackupService.BackupServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)  
[Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

