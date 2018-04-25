---
title: Visualizzazione Session
TOCTitle: Visualizzazione Session
ms:assetid: 49e33f5b-45d0-4146-a5a4-76954d895a98
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688048(v=OCS.15)
ms:contentKeyID: 49887549
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione Session

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione Session sono archiviate informazioni sulle sessioni per le quali sono presenti record nel database. Questa visualizzazione è stata introdotta con Microsoft Lync Server 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ConferenceDateTime</p></td>
<td><p>datetime</p></td>
<td><p>Riferimento dalla tabella MediaLine.</p></td>
</tr>
<tr class="even">
<td><p>ConferenceURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI conferenza nel caso di una conferenza oppure DialogID nel caso di una sessione peer-to-peer.</p></td>
</tr>
<tr class="odd">
<td><p>Correlation</p></td>
<td><p>varchar(max)</p></td>
<td><p>ID correlazione della sessione.</p></td>
</tr>
<tr class="even">
<td><p>DialogCategory</p></td>
<td><p>bit</p></td>
<td><p>Categoria di dialogo. 0 indica la coda da Lync Server a Mediation Server, 1 indica la coda da Mediation Server al gateway PSTN.</p></td>
</tr>
<tr class="odd">
<td><p>MediationServerBypassFlag</p></td>
<td><p>bit</p></td>
<td><p>Indica se la chiamata è stata ignorata o meno.</p></td>
</tr>
<tr class="even">
<td><p>MediaBypassWarningFlag</p></td>
<td><p>int</p></td>
<td><p>Questo campo, se presente, indica il motivo per cui una chiamata non è stata ignorata anche in caso di corrispondenza degli ID bypass. Per Lync Server viene definito un solo valore:</p>
<p>0x0001 - ID bypass sconosciuto per la scheda di rete predefinita</p></td>
</tr>
<tr class="odd">
<td><p>StartTime</p></td>
<td><p>datetime</p></td>
<td><p>Ora di inizio della chiamata.</p></td>
</tr>
<tr class="even">
<td><p>EndTime</p></td>
<td><p>datetime</p></td>
<td><p>Ora di fine della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CallerPool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>FQDN del pool del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>CalleePool</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>FQDN del pool del destinatario chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CallerPAI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI P-Asserted-Identity del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>CalleePAI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI P-Asserted-Identity del destinatario chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CallerEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome dell'endpoint del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>CalleeEndpoint</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome dell'endpoint del destinatario chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Stringa dell'agente utente del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>CallerUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>Tipo dell'agente utente del chiamante. Per informazioni dettagliate, vedere la <a href="lync-server-2013-useragent-table.md">Tabella UserAgent in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>CallerUserAgentCategory</p></td>
<td><p>nvarchar (64)</p></td>
<td><p>Categoria dell'agente utente del chiamante. Per informazioni dettagliate, vedere la <a href="lync-server-2013-useragentdef-table-qoe.md">Tabella UserAgentDef (QoE) in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Stringa dell'agente utente del destinatario chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CalleeUserAgentType</p></td>
<td><p>smallint</p></td>
<td><p>Tipo dell'agente utente per il destinatario chiamata. Per informazioni dettagliate, vedere la <a href="lync-server-2013-useragent-table.md">Tabella UserAgent in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>CalleeUserAgentCategory</p></td>
<td><p>nvarchar (64)</p></td>
<td><p>Categoria dell'agente utente per il destinatario chiamata. Per informazioni dettagliate, vedere la <a href="lync-server-2013-useragentdef-table-qoe.md">Tabella UserAgentDef (QoE) in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>CallerURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI del chiamante.</p></td>
</tr>
<tr class="even">
<td><p>CalleeURI</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI del destinatario chiamata.</p></td>
</tr>
<tr class="odd">
<td><p>CallPrioirty</p></td>
<td><p>int</p></td>
<td><p>Priorità della chiamata.</p></td>
</tr>
</tbody>
</table>

