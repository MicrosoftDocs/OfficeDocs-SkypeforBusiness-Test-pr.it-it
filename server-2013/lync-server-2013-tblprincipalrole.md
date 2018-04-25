---
title: 'Lync Server 2013: tblPrincipalRole'
TOCTitle: tblPrincipalRole
ms:assetid: dcd16dc1-a66c-4720-a48f-ec8b28337383
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615039(v=OCS.15)
ms:contentKeyID: 49302206
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPrincipalRole in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella tblPrincipalRole include i ruoli espliciti assegnati ai nodi.

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
<td><p>prinRoleNodeID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del nodo a cui si applica il ruolo.</p></td>
</tr>
<tr class="even">
<td><p>prinRolePrinID</p></td>
<td><p>int, not null</p></td>
<td><p>ID entità.</p></td>
</tr>
<tr class="odd">
<td><p>prinRoleTypeID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del tipo di ruolo (da tblRoleType).</p></td>
</tr>
<tr class="even">
<td><p>prinRoleUpdatedBy</p></td>
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
<td><p>&lt;prinRoleNodeID, prinRolePrinID, prinRoleTypeID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>prinRoleNodeID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblNode.nodeID.</p></td>
</tr>
<tr class="odd">
<td><p>prinRolePrinID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblPrincipal.prinID.</p></td>
</tr>
<tr class="even">
<td><p>prinRoleTypeID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblRoleType.rtypeID.</p></td>
</tr>
</tbody>
</table>

