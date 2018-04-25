---
title: New-CsNetworkInterRegionRoute
TOCTitle: New-CsNetworkInterRegionRoute
ms:assetid: 97deeba5-b49f-4078-9843-fee7b2d1e72e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398779(v=OCS.15)
ms:contentKeyID: 49301400
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkInterRegionRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova route che connette le aree di rete all'interno di una configurazione di Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkInterRegionRoute -InterNetworkRegionRouteID <String> <COMMON PARAMETERS>

    New-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene creata una nuova route della regione di rete tra la regione NorthAmerica e la regione APAC. Alla nuova route viene assegnata l'identità NA\_APAC\_Route, assegnata automaticamente come InterNetworkRegionRouteID. Le regioni collegate sono NorthAmerica, passato come valore al parametro NetworkRegionID1, e APAC, passato come valore al parametro NetworkRegionID2. In questo esempio si presume che non esista un collegamento di regione configurato per collegare direttamente NorthAmerica ad APAC. Esistono tuttavia collegamenti da NorthAmerica a EMEA (NA\_EMEA) e da EMEA ad APAC (EMEA\_APAC). Come valore del parametro NetworkRegionLinkIDs vengono utilizzati entrambi questi collegamenti, delimitati da una virgola. In questo modo le connessioni da NorthAmerica ad APAC saranno instradate attraverso EMEA, applicando le limitazioni della larghezza di banda per le connessioni audio e video associate a questi collegamenti.

    New-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 APAC -NetworkRegionLinkIDs "NA_EMEA,EMEA_APAC"

## Descrizione dettagliata

Ogni regione all'interno di una configurazione Controllo di ammissione di chiamata deve poter accedere a ciascuna delle altre regioni. Se i collegamenti di regione impostano limitazioni della larghezza di banda per le connessioni tra le regioni e rappresentano i collegamenti fisici, una route determina il percorso collegato attraversato dalla connessione per passare da una regione all'altra. Questo cmdlet consente di creare tale associazione di route.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsNetworkInterRegionRoute** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkInterRegionRoute"}

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
<td><p>Un identificatore univoco per la route della regione di rete appena creata. Le route delle regioni di rete vengono create solo nell'ambito globale, quindi questo identificatore non deve specificare un ambito. Contiene invece una stringa univoca che identifica la route.</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkRegionRouteID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo valore è identico a Identity. Non è possibile specificare un valore sia per Identity sia per InterNetworkRegionRouteID; il valore immesso per l'uno verrà automaticamente utilizzato anche per l'altro.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identità (NetworkRegionID) di una delle due regioni connesse attraverso questa route. Il valore passato a questo parametro deve essere una regione diversa da quella del valore del parametro NetworkRegionID2. In altre parole, non è possibile instradare una regione verso se stessa. Inoltre, la combinazione di NetworkRegionID1 e NetworkRegionID2 deve essere univoca (ad esempio, non è possibile definire due route per la connessione di NorthAmerica ed EMEA).</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identità (NetworkRegionID) di una delle due regioni connesse attraverso questa route. Il valore passato a questo parametro deve essere una regione diversa da quella del valore del parametro NetworkRegionID1. In altre parole, non è possibile instradare una regione verso se stessa. Inoltre, la combinazione di NetworkRegionID1 e NetworkRegionID2 deve essere univoca (ad esempio, non è possibile definire due route per la connessione di NorthAmerica ed EMEA).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare tutti i collegamenti per questa route come stringa di valori delimitati da virgole. I valori sono le identità (NetworkRegionLinkIDs) dei collegamenti di regione. Se si immettono valori sia per NetworkRegionLinkIDs sia per NetworkRegionLinks, NetworkRegionLinkIDs viene ignorato. Questo parametro offre un mezzo conveniente per specificare l'elenco di collegamenti senza dover costruire un oggetto elenco e passarlo al parametro NetworkRegionLinks.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un oggetto elenco contenente le identità (NetworkRegionLinkIDs) dei collegamenti di regione che si applicano a questa route. Per questo cmdlet, il parametro differisce dal parametro NetworkRegionLinkIDs solo nel formato utilizzato per immettere più collegamenti. Il parametro NetworkRegionLinkIDs è il metodo consigliato per definire l'elenco iniziale con questo cmdlet.</p></td>
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

Nessuno.

## Tipi restituiti

Creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

