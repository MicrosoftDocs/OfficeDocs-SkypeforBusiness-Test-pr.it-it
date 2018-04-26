---
title: 'Lync Server 2013: tblComplianceParticipant'
TOCTitle: tblComplianceParticipant
ms:assetid: 5d7e0dea-74f7-46d1-badf-b94abc8f066d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558655(v=OCS.15)
ms:contentKeyID: 49300703
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblComplianceParticipant in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In tblComplianceParticipant sono inclusi i partecipanti correnti per canale e per server.

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
<td><p>channelUri</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>URI (Uniform Resource Identifier) del canale.</p></td>
</tr>
<tr class="even">
<td><p>userId</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità del partecipante (corrispondente alla tabella tblPrincipal.prinID).</p></td>
</tr>
<tr class="odd">
<td><p>joinedAt</p></td>
<td><p>bigint, not null</p></td>
<td><p>Timestamp dell'evento di partecipazione.</p></td>
</tr>
<tr class="even">
<td><p>partedAt</p></td>
<td><p>bigint</p></td>
<td><p>Null se il partecipante sta ancora partecipando. Timestamp dell'evento di uscita dal canale, se not null.</p>
<p>Queste voci vengono rimosse alle fine quando tutti i convertitori hanno elaborato l'evento.</p></td>
</tr>
<tr class="odd">
<td><p>userUri</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>URI utente.</p></td>
</tr>
<tr class="even">
<td><p>serverID</p></td>
<td><p>int</p></td>
<td><p>Identità del server (come nella tabella tblServerIdentity.serverID).</p></td>
</tr>
<tr class="odd">
<td><p>sessionId</p></td>
<td><p>bigint</p></td>
<td><p>Sessione del server. Numero casuale generato a ogni avvio di un servizio chat, utilizzato per distinguere le sessioni allo scopo di identificare i partecipanti orfani.</p></td>
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
<td><p>&lt;channelUri, userId, joinedAt&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

