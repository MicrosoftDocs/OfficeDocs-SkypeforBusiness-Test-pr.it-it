---
title: 'Lync Server 2013: Tabella Region'
TOCTitle: Tabella Region
ms:assetid: 1751a6aa-a6e8-4f16-8eb7-ae731c2e3ee3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398235(v=OCS.15)
ms:contentKeyID: 49299805
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Region in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Region è una tabella di supporto. Ogni record rappresenta un paese o un'area geografica definita nell'impostazione di configurazione di rete.


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
<td><p><strong>RegionKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il paese o l'area geografica.</p></td>
</tr>
<tr class="even">
<td><p><strong>RegionName</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p>Univoco</p></td>
<td><p>Nome del paese o dell'area geografica.</p></td>
</tr>
</tbody>
</table>

