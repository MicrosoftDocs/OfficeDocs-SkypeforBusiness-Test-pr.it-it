---
title: Tabella UserStatistics in Lync Server 2013
TOCTitle: Tabella UserStatistics in Lync Server 2013
ms:assetid: cfaf803b-1679-4169-92d3-533fad3e56ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721893(v=OCS.15)
ms:contentKeyID: 49887767
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella UserStatistics in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella UserStatistics è una tabella di supporto. Ogni record della tabella memorizza informazioni sull'utilizzo del sistema da parte di un singolo utente. Questa tabella è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria</p></td>
<td><p>Numero univoco che identifica l'utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>LastLogInTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora dell'ultimo accesso dell'utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastConfOrganizedTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora dell'ultima conferenza organizzata dall'utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>LastCallOrganizerCallFailureTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora dell'ultimo errore di chiamata dell'utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastConfOrganizerCallFailureTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora dell'ultimo errore di chiamata dell'utente in qualità di organizzatore di una conferenza.</p></td>
</tr>
</tbody>
</table>

