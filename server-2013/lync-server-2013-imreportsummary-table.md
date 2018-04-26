---
title: Tabella IMReportSummary in Lync Server 2013
TOCTitle: Tabella IMReportSummary in Lync Server 2013
ms:assetid: 27ff9453-53f2-4fae-b637-70a086c9df96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204753(v=OCS.15)
ms:contentKeyID: 49299990
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella IMReportSummary in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella IMReportSummaryTable offre un rapporto complessivo sulle sessioni di messaggistica istantanea eseguite in un'organizzazione. Tale tabella è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria</p></td>
<td><p>Data e ora di inizio della sessione di messaggistica istantanea.</p></td>
</tr>
<tr class="even">
<td><p><strong>TimePeriod</strong></p></td>
<td><p>char(1)</p></td>
<td><p>Primaria</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><strong>PoolFQDN</strong></p></td>
<td><p>nvarchar(257)</p></td>
<td><p>Primaria</p></td>
<td><p>Nome di dominio completo del pool che ospita la sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>AuthType</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria</p></td>
<td><p>Priorità della chiamata, ad esempio urgente o non urgente. Le informazioni sulla priorità vengono memorizzate nella <a href="lync-server-2013-callpriorities-table.md">Tabella CallPriorities in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionCount</strong></p></td>
<td><p>bigint</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>MsgCount</strong></p></td>
<td><p>bigint</p></td>
<td><p></p></td>
<td><p>Numero totale di messaggi istantanei scambiati durante la sessione.</p></td>
</tr>
</tbody>
</table>

