---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398743(v=OCS.15)
ms:contentKeyID: 49301330
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una route che connette le aree di rete all'interno di una configurazione di Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimossa la route con identità NA\_APAC\_Route.

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## ESEMPIO 2

Nell’esempio 2 vengono rimosse tutte le route di aree che includono l'area NorthAmerica. La prima parte di questo comando è una chiamata al cmdlet **Get-CsNetworkInterRegionRoute**. Tale cmdlet, chiamato senza parametri, recupera tutte le route di tutte le aree. Questa raccolta di route viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** circoscrive la raccolta alle route all'interno delle quali è definita l'area NorthAmerica. A tale scopo, il cmdlet controlla se nella route è presente un valore NetworkRegionID1 oppure (-or) un valore NetworkRegionID2 uguale a (-eq) NorthAmerica. Se nella raccolta sono contenute unicamente route che includono l'area NorthAmerica, questa viene inviata tramite pipe al cmdlet **Remove-CsNetworkInterRegionRoute**, che rimuove tutte le route.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## Descrizione dettagliata

Ogni regione all'interno di una configurazione Controllo di ammissione di chiamata deve poter accedere a ciascuna delle altre regioni. Se i collegamenti di regione impostano limitazioni della larghezza di banda per le connessioni tra le regioni e rappresentano i collegamenti fisici, una route determina il percorso collegato attraversato dalla connessione per passare da una regione all'altra. Questo cmdlet consente di rimuovere una di queste associazioni di route.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsNetworkInterRegionRoute** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>L'identificatore univoco per la route della regione di rete che si desidera rimuovere. Le route delle regioni di rete vengono create solo nell'ambito globale, quindi questo identificatore non deve specificare un ambito. Contiene invece una stringa univoca che identifica la route.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Consente di accettare l'input da pipeline di oggetti route interregionali di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

