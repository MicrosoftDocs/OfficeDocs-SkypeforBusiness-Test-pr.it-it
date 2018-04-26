---
title: Set-CsAVEdgeConfiguration
TOCTitle: Set-CsAVEdgeConfiguration
ms:assetid: b410164b-b47d-450c-8048-983cac4be624
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412869(v=OCS.15)
ms:contentKeyID: 49301716
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAVEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le impostazioni di configurazione per i computer che eseguono il servizio A/V Edge. Questi computer sono noti anche come A/V Edge Server. Un A/V Edge Server consente agli utenti interni di condividere dati audio e video con utenti esterni (ovvero con utenti che non hanno effettuato l'accesso alla rete interna), nonché di scambiare file e partecipare a sessioni di condivisione desktop. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAVEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAVEdgeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxBandwidthPerPortKb <UInt32>] [-MaxBandwidthPerUserKb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il comando modifica la proprietà MaxTokenLifetime relativa alle impostazioni di configurazione globali del server A/V Edge Server. In questo esempio la durata massima del token è impostata su 4 ore (04 ore : 00 minuti : 00 secondi).

    Set-CsAVEdgeConfiguration -Identity global -MaxTokenLifetime "04:00:00"

## Descrizione dettagliata

Un A/V Edge Server consente di scambiare traffico audio e video attraverso il firewall di un'organizzazione. In questo modo gli utenti possono, tra l'altro, utilizzare Lync Server su Internet e quindi scambiare dati audio e video con utenti che hanno effettuato l'accesso al sistema all'interno del firewall. Le impostazioni di configurazione di server perimetrale possono essere assegnate nell'ambito globale, del sito e del servizio. Queste impostazioni di configurazione consentono agli amministratori di effettuare operazioni quali gestire il tempo di validità dell'autenticazione utente prima del rinnovo e limitare la larghezza di banda utilizzabile da un singolo utente o da una singola porta.

Il cmdlet **Set-CsAVEdgeConfiguration** consente di modificare le impostazioni di configurazione del server A/V Edge Server attualmente in uso nell'organizzazione. Se non espressamente indicato dal personale del supporto tecnico Microsoft, è tuttavia consigliabile per gli amministratori non modificare le impostazioni predefinite di A/V Edge Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsAVEdgeConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAVEdgeConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della raccolta di impostazioni di configurazione di A/V Edge Server da modificare. Per modificare la raccolta globale, utilizzare la sintassi seguente: -Identity global. Per modificare la raccolta di un sito, usare una sintassi simile alla seguente: -Identity site:Redmond. Le impostazioni configurate nell'ambito del servizio possono essere referenziate con una sintassi simile alla seguente: -Identity service:EdgeServer:atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto MediaRelaySettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBandwidthPerPortKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la larghezza di banda massima (in kilobit al secondo) che è possibile allocare a una singola porta. È possibile impostare la larghezza di banda massima su qualsiasi valore intero compreso tra 1 e 4294967296 (4096 gigabit) al secondo. Il valore predefinito è 3000.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxBandwidthPerUserKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la larghezza di banda massima (in kilobit al secondo) che è possibile allocare a un utente. È possibile impostare la larghezza di banda massima su qualsiasi valore intero compreso tra 1 e 4294967296 (4096 gigabit) al secondo. Il valore predefinito è 10000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Quantità massima di tempo per cui un token può essere utilizzato prima di scadere e dover essere rinnovato. Le durate dei token sono espresse utilizzando il formato seguente: Giorni.Ore:Minuti:Secondi. La durata 13 giorni ad esempio deve essere espressa come indicato di seguito, ovvero con un punto (.) dopo il numero dei giorni e due punti (:) per separare le ore, i minuti e i secondi:</p>
<p>13.00:00:00</p>
<p>Il valore predefinito di 8 ore deve essere espresso come segue:</p>
<p>08:00:00</p>
<p>La durata token minima consentita è di un minuto (00:01:00); la durata massima consentita è di 180 giorni (180.00:00:00).</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings. Il cmdlet **Set-CsAVEdgeConfiguration** accetta l'input di oggetti impostazioni di Media Relay inviati tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsAVEdgeConfiguration** non restituisce un valore o un oggetto. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

