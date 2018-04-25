---
title: 'Lync Server 2013: tblLastChatId'
TOCTitle: tblLastChatId
ms:assetid: 17a4ffbe-cca9-4ec5-ae46-38a15274889a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558616(v=OCS.15)
ms:contentKeyID: 49299808
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblLastChatId in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In LastChatId è incluso l'ultimo ID chat generato, e utilizzato nella tabella tblChat, per ogni utente.

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
<td><p>nodeID</p></td>
<td><p>int, not null</p></td>
<td><p>ID nodo (solo per il tipo di chat).</p></td>
</tr>
<tr class="even">
<td><p>lastChatID</p></td>
<td><p>bigint, not null</p></td>
<td><p>Ultimo ID chat utilizzato.</p></td>
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
<td><p>&lt;nodeID, lastChatID&gt;</p></td>
<td><p>Chiave primaria (nodeID da solo è sufficiente per l'elaborazione).</p></td>
</tr>
<tr class="even">
<td><p>nodeID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblNode.nodeID.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[tblChat in Lync Server 2013](lync-server-2013-tblchat.md)

