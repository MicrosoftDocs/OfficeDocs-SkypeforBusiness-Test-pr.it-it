---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412739(v=OCS.15)
ms:contentKeyID: 49301501
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una subnet di rete esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene modificata la subnet con Identity (ID subnet) 172.11.15.0. Alla subnet viene applicato un nuovo valore MaskBits (25) e un nuovo NetworkSiteID (Chicago).

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## ESEMPIO 2

Nell'esempio 2 tutte le subnet del sito Vancouver vengono spostate nel sito Chicago. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsNetworkSubnet**. In questo modo verrà recuperata una raccolta di tutte le subnet definite nella distribuzione di Lync Server. Questa raccolta di subnet viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** esamina la raccolta e seleziona solo le subnet in cui NetworkSiteID è uguale a (-eq) Vancouver. Ora che include solo le subnet associate al sito Vancouver, la raccolta viene inviata tramite pipe al cmdlet **Set-CsNetworkSubnet**. Viene specificato un parametro per il cmdlet **Set-CsNetworkSubnet**, ovvero NetworkSiteID. Passando al parametro il valore Chicago, si indica al cmdlet **Set-CsNetworkSubnet** di impostare su Chicago l'ID del sito di rete di ogni membro della raccolta.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## Descrizione dettagliata

Ciascuna subnet deve essere associata ad un sito di rete per stabilire la località geografica dell'host che appartiene a questa subnet. Utilizzare questo cmdlet per modificare il sito di rete associato alla subnet, la sua descrizione o la maschera di bit.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsNetworkSubnet** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Una descrizione della subnet da modificare.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>L'ID univoco della subnet da modificare. Questo valore può essere un indirizzo IP (ad esempio, 174.11.12.0) o un indirizzo URL che inizia con http: o https:.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Tipo subnet</p></td>
<td><p>Riferimento all'oggetto subnet di rete da modificare. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType e può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkSubnet</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>La maschera di bit da applicare alla subnet.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'ID del sito di rete a cui applicare la subnet. È possibile ottenere gli ID dei siti per la propria distribuzione utilizzando il cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Accetta input tramite pipeline da oggetti subnet.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

