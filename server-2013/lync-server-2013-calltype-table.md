---
title: 'Lync Server 2013: Tabella CallType'
TOCTitle: Tabella CallType
ms:assetid: a1d7187c-f851-4967-88ea-73922911ee7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412752(v=OCS.15)
ms:contentKeyID: 49301527
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella CallType in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella CallType è una tabella statica in cui viene archiviato l'elenco dei tipi di chiamata possibili.


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
<td><p><strong>CallTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>CallType</strong></p></td>
<td><p>nvarchar</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>0 - Sconosciuto</p></li>
<li><p>1 - Messaggistica istantanea</p></li>
<li><p>2 - Condivisione applicazioni</p></li>
<li><p>3 - Audio</p></li>
<li><p>4 - Audio e video</p></li>
<li><p>5 - Trasferimento file</p></li>
</ul></td>
</tr>
</tbody>
</table>

