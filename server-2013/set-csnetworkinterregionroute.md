---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398410(v=OCS.15)
ms:contentKeyID: 49300704
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una route esistente che connette le aree di rete all'interno di una configurazione di Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene modificata la route NA\_APAC\_Route cambiando i collegamenti della regione della route che verranno attraversati. Il parametro NetworkRegionLinkIDs viene utilizzato con il valore "NA\_SA,SA\_APAC" che sostituisce qualsiasi collegamento esistente con i due collegamenti specificati nella stringa.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## ESEMPIO 2

Come nell'Esempio 1, nell'Esempio 2 vengono modificati i collegamenti nella route NA\_APAC\_Route. Tuttavia, in questo esempio, invece di sostituire tutti i collegamenti della route utilizzando il parametro NetworkRegionLinkIDs, viene utilizzato il parametro NetworkRegionLinks per aggiungere un collegamento all'elenco dei collegamenti esistenti nella route. In questo caso, viene aggiunto alla route il collegamento SA\_EMEA. La sintassi @{add=\<collegamento\>} consente di aggiungere un elemento all'elenco dei collegamenti. È possibile utilizzare anche la sintassi @{replace=\<collegamento\>} per sostituire tutti i collegamenti esistenti con quelli specificati da \<collegamento\> (che si comporta allo stesso modo di NetworkRegionLinkIDs) o la sintassi @{remove=\<collegamento\>} per rimuovere un collegamento dall'elenco.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## ESEMPIO 3

Nell'esempio 3 viene modificata la route denominata NA\_Route5. In questo esempio viene modificata una delle aree di questa route. Vengono utilizzati il parametro NetworkRegionID2 per specificare la nuova area e quindi il parametro NetworkRegionLinkIDs per creare un nuovo elenco di collegamenti per la connessione delle aree della route.

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## Descrizione dettagliata

Ciascuna regione entro una configurazione CAC deve avere la possibilità di accedere a tutte le altre regioni. Mentre i collegamenti tra regioni impostano delle limitazione alla larghezza di banda nelle connessioni e rappresentano anche un collegamento fisico, una route stabilisce attraverso quale percorso collegato passerà la connessione da una regione all'altra. Questo cmdlet consente di modificare l'associazione di route.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsNetworkInterRegionRoute** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco della route tra regioni della rete che si desidera modificare. Le route tra regioni della rete vengono create solo nell'ambito globale, per cui in questo identificatore non è necessario specificare un ambito. L'identificatore contiene invece una stringa che costituisce il nome univoco di quella specifica route.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>InterNetworkRegionRouteType</p></td>
<td><p>Un riferimento oggetto ad una route della regione esistente. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType e può essere recuperato utilizzando il cmdlet <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità di una delle due regioni connesse mediante questa route. Il valore specificato per questo parametro deve essere una regione diversa dal valore specificato per il parametro NetworkRegionID2. In altre parole, non è possibile eseguire il routing di una regione a se stessa. Inoltre, la combinazione di NetworkRegionID1 e NetworkRegionID2 deve essere univoca (ad esempio, non è possibile avere due route definite che connettono NorthAmerica e EMEA.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità di una delle due regioni connesse mediante questa route. Il valore specificato per questo parametro deve essere una regione diversa dal valore specificato per il parametro NetworkRegionID1. In altre parole, non è possibile eseguire il routing di una regione a se stessa. Inoltre, la combinazione di NetworkRegionID1 e NetworkRegionID2 deve essere univoca (ad esempio, non è possibile avere due route definite che connettono NorthAmerica e EMEA.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Consente di specificare tutti i collegamenti per questa route come stringa di valori delimitati da virgole. I valori sono le identità dei collegamenti della regione. Se si immettono dei valori sia per NetworkRegionLinkIDs che per NetworRegionLinks, NetworkRegionLinkIDs verrà ignorato. I collegamenti modificati utilizzando questo parametro sostituiranno tutti i collegamenti esistenti nella route.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un oggetto contenente le identità (NetworkRegionLinkIDs) dei collegamenti della regione che vengono applicati a questa route. Per questo cmdlet, questo parametro si differenzia da NetworkRegionLinkIDs in quanto non permette solo di sostituire tutti i collegamenti esistenti nella route, ma consente anche di aggiungere o rimuovere questi singoli collegamenti.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Consente di accettare l'input tramite pipeline di oggetti route tra aree di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

