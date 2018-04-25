---
title: 'Lync Server 2013: tblRoleType'
TOCTitle: tblRoleType
ms:assetid: 1eac3a54-656a-40ac-b771-edfc64d6e34b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558623(v=OCS.15)
ms:contentKeyID: 49299885
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblRoleType in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblRoleType è una tabella di ricerca statica con i tipi di ruoli e i relativi set di autorizzazioni associati.

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
<td><p>rtypeID</p></td>
<td><p>int, non nullo</p></td>
<td><p>ID del tipo di ruolo.</p></td>
</tr>
<tr class="even">
<td><p>rtypeDesc</p></td>
<td><p>nvarchar (256), non nullo</p></td>
<td><p>Descrizione del tipo di ruolo. Sono disponibili quattro ruoli:</p>
<ul>
<li><p>Member: membro della chat.</p></li>
<li><p>Manager: responsabile della chat.</p></li>
<li><p>Voiced: relatore per una chat. auditorium</p></li>
<li><p>Creator: creazione di chat room</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>rtypeAllowedPermSet</p></td>
<td><p>bigint, non nullo</p></td>
<td><p>Set di autorizzazioni per il ruolo. I bit utilizzati sono:</p>
<ul>
<li><p>2: true se il ruolo può gestire i nodi.</p></li>
<li><p>4: true se il ruolo può creare nodi figlio.</p></li>
<li><p>7: true se il ruolo può partecipare a una chat (o a chat figlio di una categoria).</p></li>
<li><p>8: true se il ruolo può eseguire chat in una chat (o in chat figlio di una categoria).</p></li>
<li><p>10: true se il ruolo può leggere la cronologia delle chat anche se non partecipa a una chat.</p></li>
<li><p>11: true se il ruolo può visualizzare la chat (ulteriormente definito da fattori come l'ambito e la visibilità).</p></li>
<li><p>12: true se il ruolo può eseguire chat in una chat auditorium.</p></li>
<li><p>13: true se il ruolo può ignorare le regole di visibilità quando visualizza i nodi.</p></li>
</ul></td>
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
<td><p>rtypeID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

