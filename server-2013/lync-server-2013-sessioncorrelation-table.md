---
title: 'Lync Server 2013: Tabella SessionCorrelation'
TOCTitle: Tabella SessionCorrelation
ms:assetid: 041705e1-7290-464f-95f8-96256cfa2e3e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398091(v=OCS.15)
ms:contentKeyID: 49299525
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella SessionCorrelation in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella SessionCorrelation è una tabella di supporto. Ogni record rappresenta un elemento CorrelationID, che viene utilizzato per correlare più sessioni.


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
<td><p><strong>Checksum</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>CorrelationKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'A/V Conferencing Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CorrelationID</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Univoco</p></td>
<td><p>Le sessioni correlate avranno lo stesso ID correlazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Solo per uso interno.</p></td>
</tr>
</tbody>
</table>

