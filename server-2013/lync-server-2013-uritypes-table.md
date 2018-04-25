---
title: 'Lync Server 2013: Tabella UriTypes'
TOCTitle: Tabella UriTypes
ms:assetid: 77c4dfae-1b29-4e81-ba05-609e61643998
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398587(v=OCS.15)
ms:contentKeyID: 49301031
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella UriTypes in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-06-16_

La tabella UriTypes contiene i diversi tipi di URI (Uniform resource identifier) monitorati in Microsoft Lync Server 2013.


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
<td><p><strong>UriTypeId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco assegnato a un tipo di URI.</p></td>
</tr>
<tr class="even">
<td><p><strong>UriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Descrizione dei diversi tipi di URI. I valori consentiti sono:</p>
<ul>
<li><p>0 – Phone Uri</p></li>
<li><p>1 – User Uri</p></li>
</ul></td>
</tr>
</tbody>
</table>

