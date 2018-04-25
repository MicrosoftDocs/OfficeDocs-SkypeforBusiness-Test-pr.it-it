---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425726(v=OCS.15)
ms:contentKeyID: 49299949
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una subnet di rete esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene rimossa la subnet con identità (ID di subnet) 172.11.15.0.

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le subnet associate al sito Vancouver. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsNetworkSubnet**, che recupera una raccolta di tutte le subnet definite nella distribuzione di Lync Server. Questa raccolta di subnet viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** recupera la raccolta e la circoscrive alle subnet con NetworkSiteID uguale a (-eq) Vancouver. Ora che la raccolta è costituita solamente dalle subnet associate al sito Vancouver, è possibile inviarla tramite pipe al cmdlet **Remove-CsNetworkSubnet**, che rimuove ogni elemento della raccolta.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## Descrizione dettagliata

Ogni subnet deve essere associata a un sito di rete allo scopo di determinare la posizione geografica dell'host appartenente alla subnet. Utilizzare questo cmdlet per rimuovere una subnet di rete.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsNetworkSubnet** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>Identificatore univoco della subnet da rimuovere. Questo valore è un indirizzo IP (ad esempio 174.11.12.0).</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Consente di accettare l'input da pipeline di oggetti subnet di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

