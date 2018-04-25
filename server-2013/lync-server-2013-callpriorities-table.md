---
title: 'Lync Server 2013: Tabella CallPriorities'
TOCTitle: Tabella CallPriorities
ms:assetid: 043b63ae-2d64-4f38-a0df-18aa08d6caf5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398093(v=OCS.15)
ms:contentKeyID: 49299529
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella CallPriorities in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella CallPriorities è una tabella statica in cui è archiviato l'elenco delle possibili priorità delle chiamate, ad esempio 'emergency' (di emergenza), 'urgent' (urgente) o 'normal' (normale).


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
<td><p><strong>PriorityId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>Priority</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>0 - Sconosciuto</p></li>
<li><p>1 - Non urgente</p></li>
<li><p>2 - Normale</p></li>
<li><p>3 - Urgente</p></li>
<li><p>4 - Emergenza</p></li>
</ul></td>
</tr>
</tbody>
</table>

