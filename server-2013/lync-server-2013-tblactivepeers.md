---
title: 'Lync Server 2013: tblActivePeers'
TOCTitle: tblActivePeers
ms:assetid: b50c3f4a-bab6-4cb9-b40e-016cf1a9c607
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615030(v=OCS.15)
ms:contentKeyID: 49301724
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblActivePeers in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In tblActivePeers sono incluse le connessioni peer-to-peer correnti tra i servizi chat.

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
<td><p>aplServerID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del server che ha inviato la voce.</p></td>
</tr>
<tr class="even">
<td><p>aplPeerID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del peer a cui è connesso il server che esegue l'invio.</p></td>
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
<td><p>&lt;aplServerID, aplPeerID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>aplServerID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblServerIdentity.serverID.</p></td>
</tr>
<tr class="odd">
<td><p>aplPeerID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblServerIdentity.serverID.</p></td>
</tr>
</tbody>
</table>

