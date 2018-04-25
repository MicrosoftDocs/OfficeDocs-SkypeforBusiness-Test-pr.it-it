---
title: 'Lync Server 2013: Tabella VideoClientEvent'
TOCTitle: Tabella VideoClientEvent
ms:assetid: e8ab963b-fe1d-45b3-b9bd-66a5f44c1629
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399039(v=OCS.15)
ms:contentKeyID: 49302343
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella VideoClientEvent in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In ogni record è contenuto un evento client per un endpoint in una videochiamata. Per una chiamata esistono in genere due record, uno per il chiamante e l'altro per il destinatario della chiamata.


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
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>FromCaller</strong></p></td>
<td><p>bit</p></td>
<td><p>Primaria/o</p></td>
<td><p>0: dati del destinatario della chiamata</p>
<p>1: dati del chiamante</p></td>
</tr>
<tr class="odd">
<td><p><strong>NetworkBandwidthLowEventRatio</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento LowBandwidth ha generato l'avviso di stato non valido. La larghezza di banda disponibile è insufficiente per offrire un'esperienza vocale accettabile.</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkReceiveQualityEventRatio</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento ReceiveSendQuality ha generato l'avviso di stato non valido.</p>
<p>La qualità della rete in termini di instabilità o perdita di pacchetti è insufficiente e influisce sulla qualità dell'audio ricevuto.</p></td>
</tr>
</tbody>
</table>

