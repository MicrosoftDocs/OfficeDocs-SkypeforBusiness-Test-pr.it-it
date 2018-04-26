---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425817(v=OCS.15)
ms:contentKeyID: 49300103
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più route che connettono aree di rete all'interno di una configurazione del servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

L'Esempio 1 recupera la route con Identity NA\_APAC\_Route.

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## ESEMPIO 2

Nell'Esempio 2 viene usato il parametro Filter per recuperare tutte le route che contengono la stringa APAC all'interno della Identity.

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## ESEMPIO 3

In questo esempio vengono recuperate tutte le route di area che utilizzano il collegamento di area di rete NA\_EMEA. Il comando innanzitutto chiama il cmdlet **Get-CsNetworkInterRegionRoute**. Chiamando questo cmdlet senza parametri, vengono recuperate tutte le route definite con la configurazione di Controllo di ammissione di chiamata. Questa raccolta di route viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** esamina la raccolta e seleziona tutti gli elementi che hanno il valore NA\_EMEA all'interno del rispettivo elenco NetworkRegionLinks.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## ESEMPIO 4

L'Esempio 4 recupera tutte le route che includono la regione NorthAmerica. La prima parte del comando è costituita dall'utilizzo del cmdlet **Get-CsNetworkInterRegionRoute**. Questo cmdlet, utilizzato senza parametri aggiuntivi, recupererà tutte le route tra regioni. Poi questa raccolta di route viene inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** limita la raccolta includendo solo quelle route per le quali NorthAmerica è definito come una delle regioni nella route. Questo risultato si ottiene controllando se il valore NetworkRegionID1 è uguale a (-eq) NorthAmerica, o (-or) se il valore NetworkRegionID2 è uguale a NorthAmerica.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## Descrizione dettagliata

Ciascuna regione entro una configurazione CAC deve avere la possibilità di accedere a tutte le altre regioni. Mentre i collegamenti tra regioni impostano delle limitazione alla larghezza di banda nelle connessioni e rappresentano anche un collegamento fisico, una route stabilisce attraverso quale percorso collegato passerà la connessione da una regione all'altra. Questo cmdlet recupera le informazioni relative a queste associazioni di route.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsNetworkInterRegionRoute** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p>Una stringa che consente di recuperare route basandosi sulla corrispondenza tra i valori di identità e la stringa jolly fornita come valore per questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco della route tra regioni della rete che si desidera recuperare. Le route tra regioni della rete vengono create solo nell'ambito globale, per cui in questo identificatore non è necessario specificare un ambito. L'identificatore contiene invece una stringa che costituisce il nome univoco di quella specifica route.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative alla route tra aree di rete dalla replica locale dell'archivio di gestione centrale anziché dall' archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

