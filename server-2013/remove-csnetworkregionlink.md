---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413012(v=OCS.15)
ms:contentKeyID: 49302435
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un collegamento tra due aree configurate per il servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nel primo esempio viene rimosso il collegamento delle aree di rete con il parametro Identity NA\_EMEA.

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## ESEMPIO 2

Nell'esempio 2 vengono rimossi tutti i collegamenti delle aree di rete che utilizzano il profilo del criterio di larghezza di banda denominato HighBWLimits. Il primo cmdlet riportato nell'esempio è il cmdlet **Get-CsNetworkRegionLink** (senza alcun parametro), il quale recupererà tutti i collegamenti delle aree. La raccolta dei collegamenti viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** analizza ogni singolo membro della raccolta, controllandone il valore della proprietà BWPolicyProfileID. Se questa proprietà è uguale a (-eq) HighBWLimits, il membro interessato viene inviato tramite pipe al cmdlet **Remove-CsNetworkRegionLink**, il quale rimuove il collegamento.

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## Descrizione dettagliata

Le aree all'interno di una rete sono collegate tramite connettività fisica WAN. Questo cmdlet non influisce sulle connessioni fisiche, ma rimuove il collegamento dalla configurazione CAC.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsNetworkRegionLink** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<td><p>L'identificatore univoco del collegamento delle aree di rete che si desidera rimuovere. I collegamenti delle aree di rete vengono creati esclusivamente nell'ambito globale, quindi l'identificatore non richiede la specificazione di un ambito. Contiene invece una stringa con un nome univoco che identifica il collegamento.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Accetta l'invio tramite pipe di oggetti collegamenti dell'area di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

