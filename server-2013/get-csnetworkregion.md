---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398406(v=OCS.15)
ms:contentKeyID: 49300689
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più aree di rete. Le aree di rete rappresentano hub di rete o backbone in una rete aziendale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

L'Esempio 1 recupera tutte le aree di rete definite nell'organizzazione.

    Get-CsNetworkRegion

## ESEMPIO 2

L'Esempio 2 recupera tutte le aree di rete con identità NorthAmerica. Poiché le identità sono univoche, questo comando recupera al massimo un'area di rete.

    Get-CsNetworkRegion -Identity NorthAmerica

## ESEMPIO 3

Questo esempio consente di recuperare tutte le aree di rete la cui identità termina con la stringa "America". Verranno recuperate aree con identità come NorthAmerica, SouthAmerica e CentralAmerica.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## ESEMPIO 4

In questo esempio vengono recuperate tutte le aree di rete associate al sito centrale Redmond. Il comando utilizza innanzitutto il cmdlet **Get-CsNetworkRegion** senza alcun parametro per recuperare una raccolta di tutte le aree di rete definite per la distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** filtra questa raccolta e restituisce solo gli elementi (aree di rete) nei quali il valore CentralSite è uguale a (-eq) site:Redmond.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## Descrizione dettagliata

Un'area di rete crea una connessione tra diverse parti di una rete in più aree geografiche. Ciascuna area di rete deve essere associata a un sito centrale. Utilizzare questo cmdlet per recuperare le informazioni su una o più aree di rete, incluse le impostazioni e l'elemento sito centrale associato che determinano se sono consentiti percorsi alternativi per le connessioni audio e video e che associano i siti nella regione a una configurazione di bypass degli elementi multimediali.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsNetworkRegion** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p>Questo parametro consente di effettuare una ricerca con caratteri jolly sulle identità di tutte le aree di rete configurate nell'organizzazione. Utilizzare i caratteri jolly filtrare qualsiasi parte dell'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco dell'area di rete che si desidera recuperare. L'identità sarà nella forma di una stringa che identifica in modo univoco quell'area. Si noti che l'identità è la stessa di NetworkRegionID.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare le informazioni sull'area di rete dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di recuperare uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

