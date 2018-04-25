---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412867(v=OCS.15)
ms:contentKeyID: 49301715
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un collegamento tra due aree di rete configurate per il servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene modificato il profilo dei criteri di larghezza di banda di un collegamento di regione di rete denominato NA\_EMEA nel profilo HighBWLimits. Il nome del collegamento di area di rete che si desidera modificare è specificato come valore del parametro Identity. Successivamente, viene assegnato il valore HighBWLimits al parametro BWPolicyProfile. In questo modo vengono assegnati i limiti di larghezza di banda definiti dal profilo dei criteri di larghezza di banda (HighBWLimits) alle connessioni tra queste regioni.

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## Descrizione dettagliata

Le regioni all'interno di una rete sono collegate tramite connettività fisica WAN. Questo cmdlet modifica un collegamento tra due aree, consentendo di modificare le aree collegate, nonché i limiti di larghezza di banda per le connessioni audio e video tra tali aree.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsNetworkRegionLink** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identità del profilo dei criteri di larghezza di banda che definisce i limiti per il collegamento. È possibile recuperare un elenco dei profili disponibili chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il collegamento dell'area della rete che si desidera modificare. I collegamenti delle regioni di rete vengono creati esclusivamente nell'ambito globale, quindi l'identificatore non richiede la specificazione di un ambito. Contiene invece una stringa con un nome univoco che identifica il collegamento.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>Riferimento oggetto a un collegamento di area di rete. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType, che può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identità (NetworkRegionID) della regione collegata alla regione identificata dalla proprietà NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identità (NetworkRegionID) della regione collegata alla regione identificata dalla proprietà NetworkRegionID1.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Accetta l'input da pipeline di oggetti collegamento di aree di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

