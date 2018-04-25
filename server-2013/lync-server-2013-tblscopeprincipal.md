---
title: 'Lync Server 2013: tblScopePrincipal'
TOCTitle: tblScopePrincipal
ms:assetid: 422d6c7f-7ba7-4dd4-bacc-95ace47959ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558639(v=OCS.15)
ms:contentKeyID: 49300348
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblScopePrincipal in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblScopePrincipal contiene gli ambiti assegnati ai nodi.

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
<td><p>scopeNodeID</p></td>
<td><p>int, not null</p></td>
<td><p>ID di nodo a cui si applica l'ambito.</p></td>
</tr>
<tr class="even">
<td><p>scopePrinID</p></td>
<td><p>int, not null</p></td>
<td><p>ID entità.</p></td>
</tr>
<tr class="odd">
<td><p>scopeIsDenied</p></td>
<td><p>bit, not null</p></td>
<td><p>True se il tipo di ambito è Deny; False se è Allow.</p></td>
</tr>
<tr class="even">
<td><p>scopeUpdatedBy</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità che ha aggiornato per ultima questa voce.</p></td>
</tr>
</tbody>
</table>


### Chiavi

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
<td><p>&lt;scopeNodeID, scopePrinID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>scopeNodeID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblNode.nodeID.</p></td>
</tr>
<tr class="odd">
<td><p>scopePrinID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblPrincipal.prinID.</p></td>
</tr>
</tbody>
</table>

