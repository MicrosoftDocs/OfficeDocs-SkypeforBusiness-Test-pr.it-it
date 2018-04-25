---
title: 'Lync Server 2013: Tabella MediaList'
TOCTitle: Tabella MediaList
ms:assetid: 1f440590-c1bc-483e-b7bc-6cc763847768
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398279(v=OCS.15)
ms:contentKeyID: 49299888
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella MediaList in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella MediaList è una tabella statica in cui è archiviato l'elenco di diversi tipi di elementi multimediali.


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
<td><p><strong>MediaId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>Media</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>1 – Messaggistica istantanea</p></li>
<li><p>2 – Trasferimento file</p></li>
<li><p>3 – Assistenza remota</p></li>
<li><p>4 – Condivisione applicazioni</p></li>
<li><p>5 – Audio</p></li>
<li><p>6 – Video</p></li>
<li><p>7 – Invito applicazione</p></li>
</ul></td>
</tr>
</tbody>
</table>

