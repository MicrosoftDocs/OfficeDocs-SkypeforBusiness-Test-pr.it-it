---
title: 'Lync Server 2013: Tabella ContentTypes'
TOCTitle: Tabella ContentTypes
ms:assetid: e3e38035-457c-4173-bdb9-d53a7420eba2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399007(v=OCS.15)
ms:contentKeyID: 49302262
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ContentTypes in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella ContentTypes è una tabella di supporto in cui è archiviato un elenco dei tipi di contenuto utilizzati sia nelle sessioni peer-to-peer che nelle sessioni di conferenze. Ogni record della tabella rappresenta un tipo di contenuto.


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
<td><p><strong>ContentTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il tipo di contenuto.</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td> </td>
<td><p>Nome del tipo di contenuto.</p></td>
</tr>
</tbody>
</table>

