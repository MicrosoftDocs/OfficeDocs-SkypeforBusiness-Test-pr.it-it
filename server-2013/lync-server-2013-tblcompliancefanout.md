---
title: 'Lync Server 2013: tblComplianceFanout'
TOCTitle: tblComplianceFanout
ms:assetid: f5d9f342-a7cb-4b54-baa6-e656256b75ad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615050(v=OCS.15)
ms:contentKeyID: 49302475
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblComplianceFanout in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblComplianceFanout include i server che hanno elaborato un evento di conformità.

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
<td><p>fanoutEventID</p></td>
<td><p>int</p></td>
<td><p>ID evento.</p></td>
</tr>
<tr class="even">
<td><p>fanoutServerID</p></td>
<td><p>int</p></td>
<td><p>Identità del server (corrispondente alla tabella tblServerIdentity.serverID).</p></td>
</tr>
</tbody>
</table>


### Chiave

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>fanoutEventID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblComplianceData.cmplEventID.</p></td>
</tr>
</tbody>
</table>

