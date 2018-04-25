---
title: Tabella ErrorCategory
TOCTitle: Tabella ErrorCategory
ms:assetid: 0fde3b73-9a2f-44dd-b8dc-6df512303ff1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204675(v=OCS.15)
ms:contentKeyID: 49299703
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ErrorCategory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella ErrorCategory contiene i nomi descrittivi per ogni classificazione diagnostica di Microsoft Lync Server 2013. Per impostazione predefinita, Lync Server 2013 usa le seguenti classificazioni:

  - 0 -- Esito positivo

  - 1 -- Errore previsto

  - 2 -- Errore imprevisto

Questa tabella è stato introdotta in Microsoft Lync Server 2013.


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
<th>Chiave/Indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CategoryId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco della classificazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Name</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valore e nome descrittivo assegnati alla classificazione. I valori consentiti sono:</p>
<ul>
<li><p>0 -- Esito positivo</p></li>
<li><p>1 -- Errore previsto</p></li>
<li><p>2 -- Errore imprevisto</p></li>
</ul></td>
</tr>
</tbody>
</table>

