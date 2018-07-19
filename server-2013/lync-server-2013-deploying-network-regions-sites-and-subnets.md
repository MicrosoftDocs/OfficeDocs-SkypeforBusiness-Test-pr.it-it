---
title: Implementazione di aree di rete, siti di rete e subnet in Lync Server 2013
TOCTitle: Implementazione di aree di rete, siti di rete e subnet in Lync Server 2013
ms:assetid: c4b75601-3538-4d07-8d23-1ad90459ae48
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994067(v=OCS.15)
ms:contentKeyID: 52062261
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Implementazione di aree di rete, siti di rete e subnet in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Dopo aver distribuito VoIP aziendale è necessario configurare:

  - Aree di rete

  - Siti di rete

  - Subnet di rete

## Definire le aree di rete

Usare il comando New-CsNetworkRegion di Windows PowerShell per Lync Server, oppure il Pannello di controllo di Lync Server per definire le aree di rete.

    New-CsNetworkRegion -NetworkRegionID <region ID> -CentralSite <site ID>

Per ulteriori informazioni, vedere [New-CsNetworkRegion](new-csnetworkregion.md).

Per questo esempio, il comando seguente di Windows PowerShell illustra l'area di rete, Area 1 (India), definita in questo scenario.

    New-CsNetworkRegion -NetworkRegionID "India" -CentralSite "India Central Site"


## Definire i siti di rete

Usare il comando New-CsNetworkSite di Windows PowerShell per Lync Server, oppure il Pannello di controllo di Lync Server per definire i siti di rete.

    New-CsNetworkSite -NetworkSiteID <site ID> -NetworkRegionID <region ID>

Per ulteriori informazioni, vedere [New-CsNetworkSite](new-csnetworksite.md).

Per questo esempio, la tabella seguente e il comando seguente di Windows PowerShell per Lync Server illustrano i siti di rete definiti in questo scenario. A scopi illustrativi, la tabella contiene solo le impostazioni specifiche per il routing in base alla posizione.

    New-CsNetworkSite -NetworkSiteID "Delhi" -NetworkRegionID "India"
    New-CsNetworkSite -NetworkSiteID "Hyderabad" -NetworkRegionID "India"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Sito 1 (Delhi)</th>
<th>Sito 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID sito</p></td>
<td><p>Sito 1 (Delhi)</p></td>
<td><p>Sito 2 (Hyderabad)</p></td>
</tr>
<tr class="even">
<td><p>ID area</p></td>
<td><p>Area 1 (India)</p></td>
<td><p>Area 1 (India)</p></td>
</tr>
</tbody>
</table>



## Definire le subnet di rete

Usare il comando New-CsNetworkSubnet di Windows PowerShell per Lync Server, oppure il Pannello di controllo di Lync Server per definire le subnet di rete e assegnarle a siti di rete.

    New-CsNetworkSubnet -SubnetID <Subnet IP address> -MaskBits <Subnet bitmask> -NetworkSiteID <site ID>

Per ulteriori informazioni, vedere [New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet).

Per questo esempio, la tabella seguente e i comandi seguenti di Windows PowerShell illustrano l'assegnazione delle subnet di rete ai siti di rete, Delhi e Hyderabad, definiti in questo scenario. A scopi illustrativi, la tabella contiene solo le impostazioni specifiche per il routing in base alla posizione.

    New-CsNetworkSubnet -SubnetID "192.168.0.0" -MaskBits "24" -NetworkSiteID "Delhi"
    New-CsNetworkSubnet -SubnetID "192.168.1.0" -MaskBits "24" -NetworkSiteID "Hyderabad"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Sito 1 (Delhi)</th>
<th>Sito 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID subnet</p></td>
<td><p>192.168.0.0</p></td>
<td><p>192.168.1.0</p></td>
</tr>
<tr class="even">
<td><p>Maschera</p></td>
<td><p>24</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>ID sito</p></td>
<td><p>Sito 1 (Delhi)</p></td>
<td><p>Sito 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## Vedere anche

#### Ulteriori risorse

[Configurazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-configuring-location-based-routing.md)

