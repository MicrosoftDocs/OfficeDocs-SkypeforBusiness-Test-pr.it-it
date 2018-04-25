---
title: 'Lync Server 2013: tblComplianceState'
TOCTitle: tblComplianceState
ms:assetid: ea82e56c-3cca-4d89-b4e6-6bcaeb1f2830
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615045(v=OCS.15)
ms:contentKeyID: 49302339
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblComplianceState in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblComplianceState contiene informazioni sullo stato della conformità a livello di pool.

### Colonne

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>lastProcessedEntryID</p></td>
<td><p>bigint, not null</p></td>
<td><p>ID dell'ultimo evento di conformità elaborato.</p></td>
</tr>
<tr class="even">
<td><p>activeServerID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del server di conformità che detiene il blocco esclusivo sul database, o -1 se assente.</p></td>
</tr>
<tr class="odd">
<td><p>lockExpirationTime</p></td>
<td><p>datetime2, not null</p></td>
<td><p>Ora di scadenza del blocco (se activeServerID è diverso da -1).</p></td>
</tr>
</tbody>
</table>

