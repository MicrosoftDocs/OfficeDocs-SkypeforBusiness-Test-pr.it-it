---
title: 'Lync Server 2013: Tabella EdgeServers'
TOCTitle: Tabella EdgeServers
ms:assetid: aeda8c01-c88c-4f56-b3d0-bac475fae449
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412833(v=OCS.15)
ms:contentKeyID: 49301659
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella EdgeServers in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella EdgeServers è una tabella di supporto. In ogni record sono archiviate informazioni su un Edge Server coinvolto in chiamate contenenti record nel database.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Chiave/indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica questo Edge Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p> </p></td>
<td><p>Nome dell'Edge Server.</p></td>
</tr>
</tbody>
</table>

