---
title: 'Lync Server 2013: Tabella MacAddress'
TOCTitle: Tabella MacAddress
ms:assetid: a32e68c5-3f95-4217-aff4-cb3d1cc70505
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412761(v=OCS.15)
ms:contentKeyID: 49301539
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella MacAddress in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella MacAddress è una tabella di supporto. Ogni record rappresenta un'origine.


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
<td><p><strong>MacAddressKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'indirizzo MAC.</p></td>
</tr>
<tr class="even">
<td><p><strong>MacAddress</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>Univoco</p></td>
<td><p>Stringa dell'indirizzo MAC.</p></td>
</tr>
</tbody>
</table>

