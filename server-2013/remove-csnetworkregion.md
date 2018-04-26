---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398466(v=OCS.15)
ms:contentKeyID: 49300814
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un'area di rete esistente. Le aree di rete rappresentano hub di rete o backbone in una rete aziendale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene rimossa l'area di rete con identità NorthAmerica. Poiché le identità sono univoche, con questo comando viene rimossa una sola area di rete.

    Remove-CsNetworkRegion -Identity NorthAmerica

## ESEMPIO 2

In questo esempio vengono rimosse tutte le aree di rete associate al sito centrale Redmond. Il comando chiama innanzitutto il cmdlet **Get-CsNetworkRegion** senza alcun parametro per recuperare una raccolta di tutte le aree di rete definite per la distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** filtra questa raccolta per restituire solo gli elementi (aree di rete) in cui il valore CentralSite è uguale (-eq) a site:Redmond. Dopo aver circoscritto la raccolta a questi elementi, questa nuova raccolta viene inviata tramite pipe al cmdlet **Remove-CsNetworkRegion**, che rimuove ogni elemento della raccolta.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## ESEMPIO 3

Con questo esempio viene rimossa l'area di rete con identità NorthAmerica. Un'area non può però essere rimossa se è associata a un sito. Pertanto, in questo esempio per prima cosa vengono rimosse le associazioni tra l'area NorthAmerica e un sito.

Nell'esempio viene chiamato innanzitutto il cmdlet **Get-CsNetworkSite** senza alcun parametro per recuperare una raccolta di tutti i siti di rete definiti per la distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** filtra questa raccolta per restituire solo quegli elementi (siti di rete) in cui il valore NetworkRegionID è uguale (-eq) a NorthAmerica. Dopo aver circoscritto la raccolta a questi elementi, questa nuova raccolta viene inviata tramite pipe al cmdlet **Set-CsNetworkSite**. Per ogni sito contenente NorthAmerica come valore di NetworkRegionID, viene impostato NetworkRegionID su Null ($null). In questo modo viene rimosso il riferimento a quella area in tale sito. Un sito tuttavia non può disporre di un ID di bypass se non è associato a un sito. Pertanto, oltre a rimuovere il riferimento all'area impostando NetworkRegionID su Null, è necessario rimuovere anche l'associazione di bypass impostando BypassID su Null.

Una volta completata la riga 1, qualsiasi sito associato alla regione NorthAmerica non è più associato a una regione o a qualche impostazione di bypass. A questo punto è possibile chiamare la riga 2, che rimuove l'area di rete.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## Descrizione dettagliata

Un'area di rete collega diverse parti di una rete attraverso molteplici aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il sito del data center su cui è in esecuzione il servizio dei criteri di larghezza di banda. Utilizzare questo cmdlet per rimuovere un'area di rete.

Non è possibile rimuovere un'area di rete se è associata a un sito di rete (vale a dire se il NetworkRegionID di un sito è uguale all'identità della regione). Se si tenta di rimuovere un'area associata a un sito viene visualizzato un messaggio di errore.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsNetworkRegion** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p>L'identificatore univoco dell'area di rete da rimuovere. L'identità sarà rappresentata da una stringa che identifica in modo univoco tale area.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Consente di accettare l'input da pipeline di oggetti area di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

