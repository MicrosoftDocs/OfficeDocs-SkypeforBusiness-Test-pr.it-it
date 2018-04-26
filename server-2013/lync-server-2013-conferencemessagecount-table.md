---
title: 'Lync Server 2013: Tabella ConferenceMessageCount'
TOCTitle: Tabella ConferenceMessageCount
ms:assetid: 78569dbf-5217-42fa-ba1a-4380f56e2a3d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398590(v=OCS.15)
ms:contentKeyID: 49301041
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ConferenceMessageCount in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record di questa tabella rappresenta un utente in una conferenza di messaggistica istantanea e include il numero di messaggi inviati dall'utente. Ogni conferenza è rappresentata da più record della tabella, un record per ogni utente.


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Ora dell'istanza della conferenza. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco un'istanza di conferenza. Vedere la <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero di ID per identificare l'istanza della conferenza. Valore utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco l'istanza della conferenza. Vedere la <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero univoco che identifica l'utente, a cui viene fatto riferimento dalla <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageCount</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>Numero di messaggi inviati dall'utente durante la conferenza.</p></td>
</tr>
</tbody>
</table>

