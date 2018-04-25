---
title: Tabella TraceRoute in Lync Server 2013
TOCTitle: Tabella TraceRoute in Lync Server 2013
ms:assetid: b9493cef-6ece-4f13-bf68-dbf132aab4f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205205(v=OCS.15)
ms:contentKeyID: 49301768
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella TraceRoute in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella TraceRoute sono incluse le informazioni di routing provenienti dalle chiamate. Questa tabella è stata introdotta in Microsoft Lync Server 2013.


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
<td><p>Primaria, esterna</p></td>
<td><p>Data e ora di inizio della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Identificatore univoco utilizzato per distinguere le diverse chiamate che possono essere iniziate nella stessa data e alla stessa ora.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Rappresenta il tipo di linea video utilizzata nella chiamata. I valori consentiti sono:</p>
<ul>
<li><p>0 - Audio</p></li>
<li><p>1 - Video</p></li>
<li><p>2 - Panoramica</p></li>
<li><p>3 - Condivisione applicazione/desktop</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>FromCaller</strong></p></td>
<td><p>bit</p></td>
<td><p>Primaria/o</p></td>
<td><p>Endpoint che ha effettuato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Hop</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Hop di rete.</p></td>
</tr>
<tr class="even">
<td><p><strong>IPAddressKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Identificatore univoco dell'indirizzo IP. Le informazioni relative a tale indirizzo sono archiviate nella <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTT</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Tempo di roundtrip, ovvero la quantità di tempo necessaria a un pacchetto voce per raggiungere la relativa destinazione e quindi inviare di nuovo la notifica ricevuta.</p></td>
</tr>
</tbody>
</table>

