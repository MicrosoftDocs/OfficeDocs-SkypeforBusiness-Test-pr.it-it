---
title: Visualizzazione ErrorReport
TOCTitle: Visualizzazione ErrorReport
ms:assetid: ca873f7e-b18b-4eaf-8db0-5f9d5a9b60a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721887(v=OCS.15)
ms:contentKeyID: 49887752
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione ErrorReport

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione ErrorReport vengono archiviate informazioni sugli errori segnalati. Ogni record corrisponde a un'occorrenza di un errore. Gli errori vengono acquisiti dall'agente registrazione dettagli chiamata in esecuzione nel Front End Server o inviati dal client. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data/ora in cui si è verificato l'errore. Valore utilizzato con ErrorReportSeq per identificare in modo univoco un errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero ID per identificare l'errore. Valore utilizzato con ErrorTime per identificare in modo univoco un errore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p>ID diagnostica della segnalazione errori.</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente che ha dato origine all'errore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente che ha dato origine all'errore. Per ulteriori informazioni, vedere la <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>FromTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tenant dell'utente che ha dato origine all'errore. Per ulteriori informazioni, vedere la <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente di destinazione della segnalazioni errori.</p></td>
</tr>
<tr class="even">
<td><p><strong>ToUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente di destinazione della segnalazione errori. Per ulteriori informazioni, vedere la tabella UriTypes.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tenant dell'utente di destinazione della segnalazione errori. Per ulteriori informazioni, vedere la <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI della conferenza di destinazione della segnalazioni errori.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI della conferenza di destinazione della segnalazioni errori. Per ulteriori informazioni, vedere la <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data/ora della richiesta di sessione che ha dato origine alla segnalazione errori. Valore utilizzato con SessionIDSeq per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero ID per identificare la richiesta di sessione che ha dato origine alla segnalazione errori. Valore utilizzato con SessionIDTime per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogId</strong></p></td>
<td><p>varstring(775)</p></td>
<td><p>ID dialogo SIP della sessione che ha dato origine all'errore. Il formato è il seguente:</p>
<p>dialog;from-tag;to-tag</p>
<p>Questi dati possono essere convertiti in formato testo utilizzando la sintassi seguente:</p>
<p>cast(cast(ExternalId as varbinary(max)) as varchar(max))</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Versione del client utilizzato dall'utente che ha dato origine all'errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p>Client utilizzato dall'utente che ha dato origine all'errore. Per ulteriori informazioni, vedere la <a href="lync-server-2013-useragentdef-table.md">Tabella UserAgentDef in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>Nome della categoria del client utilizzato dall'utente che ha dato origine all'errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Source</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome del server che ha dato origine all'errore (se il rapporto è stato inviato da un componente del server).</p></td>
</tr>
<tr class="odd">
<td><p><strong>Application</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome dell'applicazione che ha dato origine all'errore (se il rapporto è stato inviato da un componente del server).</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p>Codice di risposta SIP per la sessione del messaggio SIP contenente la segnalazione errori.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RequestType</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>Tipo della richiesta non riuscita.</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>Tipo di contenuto della richiesta non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di sessione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-calltype-table.md">Tabella CallType in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Identificatore univoco di correlazione delle informazioni sul tempo di partecipazione per i diversi componenti coinvolti in una conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p>Tempo (in millisecondi) richiesto da un componente specifico per partecipare a una conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsCapturedByServer</strong></p></td>
<td><p>bit</p></td>
<td><p>Indica se la segnalazione errori è stata acquisita dall'agente registrazione dettagli chiamata in esecuzione nel Front End Server o è stata inviata dal client.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p>Riservato per utilizzi futuri.</p></td>
</tr>
<tr class="even">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>Informazioni aggiuntive sull'errore.</p></td>
</tr>
</tbody>
</table>

