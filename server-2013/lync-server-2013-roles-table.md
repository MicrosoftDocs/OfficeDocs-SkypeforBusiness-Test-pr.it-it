---
title: 'Lync Server 2013: Tabella Roles'
TOCTitle: Tabella Roles
ms:assetid: e8eb8a10-26b5-488b-bc8c-f9ef93f98bdb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399043(v=OCS.15)
ms:contentKeyID: 49302346
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Roles in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Roles è una tabella statica in cui viene archiviato l'elenco di possibili ruoli per conferenze, ad esempio partecipante e relatore.


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
<td><p><strong>RoleId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>Role</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>0 - Sconosciuto</p></li>
<li><p>1 - Relatore</p></li>
<li><p>2 - Partecipante</p></li>
</ul></td>
</tr>
</tbody>
</table>

