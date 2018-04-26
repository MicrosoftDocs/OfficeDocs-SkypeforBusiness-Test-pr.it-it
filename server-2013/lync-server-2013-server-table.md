---
title: 'Lync Server 2013: Tabella Server'
TOCTitle: Tabella Server
ms:assetid: 9af89d08-d35a-48e8-b56d-6df292f973cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398801(v=OCS.15)
ms:contentKeyID: 49301431
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Server è una tabella di supporto. Ogni record rappresenta un server.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Colonna</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ServerKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il server.</p></td>
</tr>
<tr class="even">
<td><p><strong>FQDNOrIP</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>indice</p></td>
<td><p>Stringa dell'indirizzo MAC.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerType</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>1: Mediation Server</p>
<p>2: A/V Conferencing Server 16394: servizio A/V Edge 32769: gateway</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolName</strong></p></td>
<td><p>nvarchar(512)</p></td>
<td><p></p></td>
<td><p>Pool di appartenenza del server. Applicabile solo per A/V Conferencing Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Solo per uso interno.</p></td>
</tr>
</tbody>
</table>

