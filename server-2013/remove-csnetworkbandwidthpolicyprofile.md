---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398609(v=OCS.15)
ms:contentKeyID: 49301070
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un profilo dei criteri di larghezza di banda di rete. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimosso il profilo dei criteri di larghezza di banda con identità LowBWProfile. Poiché l'identità deve essere univoca questo rimuoverà un solo profilo.

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## ESEMPIO 2

Nell'esempio 2 vengono rimossi tutti i riferimenti al profilo dei criteri di larghezza di banda con identità (Identity) LowBWProfile da tutti i siti ai quali era stato assegnato, quindi rimuove il profilo. La prima riga di questo esempio inizia con una chiamata al cmdlet **Get-CsNetworkSite** per recuperare tutti i siti configurati per il servizio Controllo di ammissione di chiamata. Questa raccolta di siti viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i siti in cui la proprietà BWPolicyProfileID è uguale a (-eq) LowBWProfile. Questa raccolta ridotta, contenente solo i siti in cui la proprietà BWPolicyProfileID è impostata sul valore LowBWProfile, viene inviata tramite pipe al cmdlet **Set-CSNetworkSite**, che modifica ogni sito impostando la proprietà BWPolicyProfileID su Null ($null). In questo modo vengono trovati tutti i siti con BWPolicyProfileID uguale a LowBWProfile e tale valore è stato impostato su Null. A questo punto nessun sito utilizza più il profilo LowBWProfile. Ora è possibile chiamare il cmdlet **Remove-CsNetworkBandwidthPolicyProfile** nel profilo LowBWProfile per rimuoverlo, sapendo che tale profilo non è più utilizzato in alcun sito.

Per accertarsi che il profilo non sia utilizzato in nessuna altra parte della configurazione di rete, ripetere gli stessi passi della Linea 1 per i criteri inter-sito e per i collegamenti delle regioni di rete.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## Descrizione dettagliata

Come parte del controllo di ammissione di chiamata (CAC), viene utilizzato un criterio di larghezza di banda per definire le limitazioni relative alla larghezza di banda per alcune modalità. In Lync Server possono essere assegnate limitazioni della larghezza di banda solo alle modalità audio e video. Questo cmdlet rimuove un profilo contenitore di questi criteri.

IMPORTANTE: se un profilo viene assegnato a un sito (utilizzando il cmdlet **New-CsNetworkSite** o **Set-CsNetworkSite**), a un criterio tra siti (utilizzando il cmdlet **New-CsNetworkInterSitePolicy** o **Set-CsNetworkInterSitePolicy**) o a un collegamento tra aree di rete (utilizzando il cmdlet **New-CsNetworkRegionLink** o **Set-CsNetworkRegionLink**), non può essere rimosso. Si riceverà un messaggio di errore se si tenta di rimuovere il profilo chiamando il cmdlet **Remove-CsNetworkBandwidthPolicyProfile**. È necessario prima rimuovere il profilo da tutti i siti, criteri tra siti e collegamenti tra aree di rete, quindi sarà possibile rimuovere il profilo.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsNetworkBandwidthPolicyProfile** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un valore di stringa che identifica in modo univoco il profilo dei criteri di larghezza di banda da rimuovere. Specificando una identità verrà rimosso un solo profilo.</p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Accetta input tramite pipeline di oggetti profilo dei criteri di larghezza di banda della rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

