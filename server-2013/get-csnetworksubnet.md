---
title: Get-CsNetworkSubnet
TOCTitle: Get-CsNetworkSubnet
ms:assetid: ad74155a-8d83-42f6-bb1e-8bfc7d57d5b0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412825(v=OCS.15)
ms:contentKeyID: 49301655
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni su una o più subnet di rete. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSubnet [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate tutte le subnet della distribuzione di Lync Server.

    Get-CsNetworkSubnet

## ESEMPIO 2

In questo esempio vengono recuperate tutte le informazioni sulla subnet con l'identità (ID della subnet) 172.11.15.0.

    Get-CsNetworkSubnet -Identity 172.11.15.0

## ESEMPIO 3

In questo esempio vengono recuperate tutte le subnet con identità che iniziano con 172.11.

    Get-CsNetworkSubnet -Filter 172.11.*

## ESEMPIO 4

Nell'esempio 4 vengono recuperate tutte le subnet associate al sito Vancouver. Viene chiamato innanzitutto il cmdlet **Get-CsNetworkSubnet** senza parametri. Come illustrato nell'esempio 2, in questo modo vengono recuperate tutte le subnet definite. Questa raccolta di subnet viene quindi viene inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** utilizza tale raccolta e la circoscrive solo alle subnet con NetworkSiteID uguale a (-eq) Vancouver.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"}

## Descrizione dettagliata

Ogni subnet deve essere associata a un sito di rete per la determinazione della posizione geografica dell'host appartenente alla subnet. Utilizzare questo cmdlet per recuperare informazioni sulla subnet, inclusa l'identità (ID della subnet), numero di bit di maschera, il sito di rete associato e la descrizione della subnet.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsNetworkSubnet** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSubnet"}

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
<td><p>Utilizzare questo parametro per eseguire una ricerca con caratteri jolly di tutte le subnet basate sull'identità. Ad esempio, il valore Filter 172.11.* recupera tutte le subnet con identità che inizia con 172.11. (ad esempio 172.11.10.0, 172.11.25.0 e così via).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'ID univoco della subnet che si desidera recuperare. Questo valore è un indirizzo IP (ad esempio 174.11.12.0).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative alla subnet di rete dalla replica locale dell' archivio di gestione centrale anziché dall' archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)

