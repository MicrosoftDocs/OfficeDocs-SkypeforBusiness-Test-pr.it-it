---
title: New-CsAVEdgeConfiguration
TOCTitle: New-CsAVEdgeConfiguration
ms:assetid: b6bcf426-9037-4679-99dc-e94bfb8f72a6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412884(v=OCS.15)
ms:contentKeyID: 49301744
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAVEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione per i computer che eseguono il servizio A/V Edge. Questi computer sono noti anche come A/V Edge Server. Un A/V Edge Server consente agli utenti interni di condividere dati audio e video con utenti esterni, ovvero utenti non connessi alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAVEdgeConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxBandwidthPerPortKb <UInt32>] [-MaxBandwidthPerUserKb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione A/V Edge per il sito Redmond. In questo esempio il valore della proprietà MaxTokenLifetime è impostato su 4 ore (04 ore : 00 minuti : 00 secondi).

    New-CsAVEdgeConfiguration -Identity site:Redmond -MaxTokenLifetime "04:00:00"

## ESEMPIO 2

Nell'esempio 2 viene illustrato come è possibile creare una nuova raccolta di impostazioni di configurazione di A/V Edge Server in memoria e quindi trasformare queste impostazioni virtuali in una raccolta effettiva di impostazioni di A/V Edge Server. A tale scopo, il primo comando nell'esempio crea una nuova raccolta di impostazioni per il sito Redmond. Viene aggiunto il parametro InMemory per assicurare che queste impostazioni vengano create solo in memoria e non immediatamente applicate al sito Redmond. Poiché queste impostazioni sono presenti solo in memoria, devono essere archiviate in una variabile, in questo caso una variabile denominata $x.

Nel secondo comando il valore della proprietà MaxTokenLifetime è impostato su 4 ore (04 ore:00 minuti:00 secondi). Nel terzo comando viene utilizzato quindi il cmdlet **Set-CsAVEdgeConfiguration** per applicare le impostazioni archiviate nella variabile $x al sito Redmond.

    $x = New-CsAVEdgeConfiguration -Identity site:Redmond -InMemory
    $x.MaxTokenLifetime = "04:00:00"
    Set-CsAVEdgeConfiguration -Instance $x

## Descrizione dettagliata

Un A/V Edge Server consente di scambiare traffico audio e video attraverso il firewall di un'organizzazione. In questo modo gli utenti possono, tra l'altro, utilizzare Lync Server su Internet e quindi scambiare dati audio e video con utenti che hanno effettuato l'accesso al sistema all'interno del firewall. Le impostazioni di configurazione di server perimetrale possono essere assegnate nell'ambito globale, del sito e del servizio. Le impostazioni di configurazione di A/V Edge Server consentono agli amministratori di gestire il tempo di validità dell'autenticazione utente prima del rinnovo e di limitare la larghezza di banda utilizzabile da un singolo utente o da una singola porta.

Il cmdlet **New-CsAVEdgeConfiguration** consente di creare nuove raccolte di impostazioni di configurazione di A/V Edge Server nell'ambito del sito o del servizio. Come illustrato, le impostazioni A/V Edge possono anche essere configurate con ambito globale. Non è possibile tuttavia creare una nuova raccolta nell'ambito globale.

Si noti che un dato sito o servizio può ospitare al massimo un sola raccolta di impostazioni di configurazione di A/V Edge Server. Se il sito Redmond ospita già una raccolta di impostazioni di A/V Edge Server, non sarà possibile creare una nuova raccolta con Identity site:Redmond.

Se non espressamente indicato dal personale del supporto tecnico Microsoft, non è consigliabile modificare le impostazioni di configurazione di A/V Edge Server predefinite. Pertanto, non è probabilmente necessario creare una nuova raccolta di impostazioni per un sito o un servizio.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsAVEdgeConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAVEdgeConfiguration"}

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
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione A/V Edge da creare. Per creare una raccolta di impostazioni da applicare con ambiento di sito, utilizzare una sintassi analoga alla seguente: -Identity site:Redmond. Si noti che questo comando avrà esito negativo se al sito Redmond è già stata applicata una raccolta di impostazioni di configurazione di A/V Edge Server. Per le impostazioni configurate nell'ambito del servizio deve essere utilizzata una sintassi simile alla seguente: -Identity service:EdgeServer:atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsAVEdgeConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Crea le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

