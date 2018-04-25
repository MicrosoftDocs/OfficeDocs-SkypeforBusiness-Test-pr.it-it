---
title: Remove-CsAVEdgeConfiguration
TOCTitle: Remove-CsAVEdgeConfiguration
ms:assetid: 98bceec5-ed9d-4574-b6bf-f51e0f414ca7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398786(v=OCS.15)
ms:contentKeyID: 49301408
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAVEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di rimuovere una raccolta esistente di impostazioni di configurazione applicate ai computer in cui è in esecuzione il servizio Access Edge. Questi computer sono noti anche come A/V Edge Server. Un A/V Edge Server consente agli utenti interni di condividere dati audio e video con utenti esterni, ovvero non connessi alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAVEdgeConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 rimuove le impostazioni di configurazione A/V Edge con l'identità site:Redmond. Dopo la rimozione delle impostazioni, gli A/V Edge Server nel sito Redmond verranno controllati dalle impostazioni di configurazione globali.

    Remove-CsAVEdgeConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione A/V Edge applicate nell'ambito del servizio. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAVEdgeConfiguration** con il parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni configurate nell'ambito del servizio. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAVEdgeConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsAVEdgeConfiguration -Filter "service:*" | Remove-CsAVEdgeConfiguration

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione A/V Edge in cui il valore della proprietà MaxBandwidthPerUserKB è inferiore a 5.000 kilobit al secondo. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAVEdgeConfiguration** senza parametri aggiuntivi per restituire una raccolta di tutte le impostazioni A/V Edge attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxBandwidthPerUserKB è minore di 5000. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAVEdgeConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -lt 5000} | Remove-CsAVEdgeConfiguration

## Descrizione dettagliata

Un A/V Edge Server consente di scambiare traffico audio e video attraverso il firewall di un'organizzazione. In questo modo gli utenti possono, tra l'altro, utilizzare Lync Server su Internet e quindi scambiare dati audio e video con utenti che hanno effettuato l'accesso al sistema all'interno del firewall. Le impostazioni di configurazione dei server perimetrali (server perimetrale) possono essere assegnate all'ambito globale, del sito e del servizio. Le impostazioni di configurazione A/V Edge consentono agli amministratori di effettuare operazioni quali gestire la durata del periodo di validità dell'autenticazione utente prima del rinnovo e limitare la larghezza di banda utilizzabile da un singolo utente o da una singola porta.

Il cmdlet **Remove-CsAVEdgeConfiguration** consente di eliminare le impostazioni di configurazione A/V Edge applicate nell'ambito del sito o del servizio. Il cmdlet può essere eseguito anche sulle impostazioni globale, ma queste non saranno eliminate. In realtà, le proprietà contenute nella raccolta globale saranno riportate ai loro valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsAVEdgeConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAVEdgeConfiguration"}

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
<td><p>Identificatore univoco per le impostazioni di configurazione A/V Edge da rimuovere. Per &quot;rimuovere&quot; la raccolta globale, utilizzare la seguente sintassi: -Identity global. Come già osservato, le impostazioni globali non possono essere rimosse; in realtà, è possibile solamente riportare le proprietà ai valori predefiniti. Per rimuovere una raccolta di siti, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Le impostazioni configurate nell'ambito del servizio possono essere referenziate con una sintassi simile alla seguente:</p>
<p>-Identity service:EdgeServer:atl-cs-001.litwareinc.com</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità di un criterio.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings. Il cmdlet **Remove-CsAVEdgeConfiguration** accetta l'input da pipeline di oggetti impostazioni di Media Relay. Questi oggetti sono stati recuperati eseguendo il cmdlet **Get-CsAVEdgeConfiguration**.

## Tipi restituiti

Il cmdlet **Remove-CsAVEdgeConfiguration** non restituisce alcun oggetto o valore. Elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

