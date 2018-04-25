---
title: 'Lync Server 2013: Tabella PayloadDescription'
TOCTitle: Tabella PayloadDescription
ms:assetid: c49d61c0-305a-4770-a5d2-5d9f05decc6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412971(v=OCS.15)
ms:contentKeyID: 49301892
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella PayloadDescription in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella PayloadDescription è una tabella di supporto. Ogni record rappresenta un codec, che viene utilizzato in una sessione audio o video.


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
<td><p><strong>PayloadDescriptionKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il codec.</p></td>
</tr>
<tr class="even">
<td><p><strong>PayloadDescription</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Univoco</p></td>
<td><p>Nome del codec.</p></td>
</tr>
</tbody>
</table>

