---
title: 'Lync Server 2013: Tabella Session'
TOCTitle: Tabella Session
ms:assetid: 7f05529c-794d-41ed-bca4-2e85b87b2dec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398635(v=OCS.15)
ms:contentKeyID: 49301121
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Session in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta una sessione con contenuti audio oppure audio e video. Include informazioni generali sulla sessione. Una sessione viene definita come dialogo SIP (Session Initiation Protocol) audio o video tra due endpoint.


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
<td><p>Riferimento dalla <a href="lync-server-2013-dialog-table.md">Tabella Dialog in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-dialog-table.md">Tabella Dialog in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Chiave di conferenza. Riferimento dalla <a href="lync-server-2013-conference-table.md">Tabella Conference in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CorrelationKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Chiave di correlazione. Riferimento dalla <a href="lync-server-2013-sessioncorrelation-table.md">Tabella SessionCorrelation in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogCategory</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Categoria di dialogo. 0 indica la coda da Lync Server a Mediation Server, 1 indica la coda da Mediation Server al gateway PSTN.</p></td>
</tr>
<tr class="even">
<td><p><strong>MediationServerBypassFlag</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Flag che indica se la chiamata è stata o meno ignorata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaBypassWarningFlag</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Questo campo, se presente, indica il motivo per cui una chiamata non è stata ignorata anche in caso di corrispondenza degli ID bypass. Per Lync Server, viene definito un solo valore.</p>
<p>0x0001 - ID bypass sconosciuto per la scheda di rete predefinita.</p></td>
</tr>
<tr class="even">
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora di inizio della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora di fine della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPool</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Pool del chiamante. Riferimento dalla <a href="lync-server-2013-pool-table.md">Tabella Pool in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleePool</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Pool del destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-pool-table.md">Tabella Pool in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleePAI</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI SIP nel campo PAI (P-Asserted Identity) dell'endpoint destinatario. Riferimento dalla <a href="lync-server-2013-user-table.md">Tabella User in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerURI</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI del chiamante. Riferimento dalla <a href="lync-server-2013-user-table.md">Tabella User in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerEndpoint</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Endpoint del chiamante. Riferimento dalla <a href="lync-server-2013-endpoint-table.md">Tabella Endpoint in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerUserAgent</strong></p></td>
<td><p>bit</p></td>
<td><p>Esterna</p></td>
<td><p>Agente utente del chiamante. Riferimento dalla <a href="lync-server-2013-useragent-table.md">Tabella UserAgent in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallPriority</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Priorità della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClassifiedPoorCall</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Questa colonna è stata deprecata e non è utilizzata in Microsoft Lync Server 2013. Le informazioni sono riportate per linea multimediale. Per maggiori informazioni, vedere <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPAI</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>PAI (P-Asserted-Identity) dell'utente che ha avviato la chiamata. Questo valore viene utilizzato per trasmettere l'identità reale di un utente che ha avviato una chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeEndpoint</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Endpoint che ha ricevuto la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeUserAgent</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Agente utente impiegato dall'utente che ha ricevuto la chiamata. Un agente utente rappresenta il dispositivo client endpoint.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeUri</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI SIP dell'utente che ha ricevuto la chiamata.</p></td>
</tr>
</tbody>
</table>

