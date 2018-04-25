---
title: 'Lync Server 2013: Tabella Pool'
TOCTitle: Tabella Pool
ms:assetid: 92ded8fd-d0ad-4f8a-9e6f-2e8a690fda3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398746(v=OCS.15)
ms:contentKeyID: 49301345
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Pool è una tabella di supporto in cui vengono archiviate informazioni sui diversi pool Front End. Ogni record della tabella rappresenta un pool.


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
<td><p><strong>PoolKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il pool.</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Unique </p></td>
<td><p>Nome di dominio completo del pool.</p></td>
</tr>
</tbody>
</table>

