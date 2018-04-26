---
title: 'Lync Server 2013: tblServerIdentity'
TOCTitle: tblServerIdentity
ms:assetid: 5411c9bc-b0b3-41fc-8b7e-fa71cccd770b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558648(v=OCS.15)
ms:contentKeyID: 49300534
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblServerIdentity in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblServerIdentity contiene i server di chat attivi nel pool di server Chat persistente.

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
<td><p>serverID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del server. Corrisponde all'ID istanza dell' archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p>serverAddress</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>Indirizzo del server che usa l'indirizzo di Windows Communication Foundation.</p></td>
</tr>
<tr class="odd">
<td><p>serverLastPingTime</p></td>
<td><p>datetime</p></td>
<td><p>Ora dell'ultimo aggiornamento di questa riga eseguito dal Channel Server per confermare che è in esecuzione.</p></td>
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
<td><p>serverID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

