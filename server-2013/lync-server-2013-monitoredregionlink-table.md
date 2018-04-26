---
title: 'Lync Server 2013: Tabella MonitoredRegionLink'
TOCTitle: Tabella MonitoredRegionLink
ms:assetid: cebda194-7be3-42d6-b6f0-c86f8b0f200a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398874(v=OCS.15)
ms:contentKeyID: 49302006
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella MonitoredRegionLink in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella MonitoredRegionLink è una tabella di supporto. Ogni record rappresenta un collegamento tra due paesi.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Colonna</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Region1Key</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-region-table.md">Tabella Region in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Region2Key</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-region-table.md">Tabella Region in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

