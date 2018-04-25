---
title: 'Lync Server 2013: Tabella ErrorReport'
TOCTitle: Tabella ErrorReport
ms:assetid: ae0287b4-e8ca-4f8c-84ef-502897dcaa2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412826(v=OCS.15)
ms:contentKeyID: 49301661
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ErrorReport in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Nella tabella ErrorReport vengono archiviate informazioni sugli errori che si sono verificati. Ogni record corrisponde a un'occorrenza di un errore. Gli errori vengono acquisiti dall'agente CDR in esecuzione nel Front End Server o inviato dal client.


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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Data e ora in cui si è verificato l'errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero ID per identificare la segnalazione errori. Valore utilizzato in combinazione con <strong>ErrorTime</strong> per identificare in modo univoco una segnalazione errori.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID univoco del tipo di errore. Per ulteriori informazioni, vedere <a href="lync-server-2013-errordef-table.md">Tabella ErrorDef in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>FromUserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Utente che ha dato origine alla richiesta che ha causato l'errore. Per ulteriori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ToUserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Utente di destinazione per la richiesta che ha causato l'errore. Per ulteriori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI della conferenza correlato all'errore. Per ulteriori informazioni, vedere <a href="lync-server-2013-conferenceuris-table.md">Tabella ConferenceUris in Lync Server 2013</a>. In genere, se ConferenceUriId non è null, FromUserId o ToUserId sarà null.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Esterna</p></td>
<td><p>Utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di ID per identificare la sessione. Utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Server che ha inviato la segnalazione dell'errore (se la segnalazione viene inviata da un componente server). Per ulteriori informazioni, vedere <a href="lync-server-2013-servers-table.md">Tabella Servers in Lync Server 2013</a>.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>ApplicationId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Server che ha inviato la segnalazione dell'errore (se la segnalazione viene inviata da un componente server). Per ulteriori informazioni, vedere <a href="lync-server-2013-application-table.md">Tabella Application in Lync Server 2013</a>.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>image</p></td>
<td><p> </p></td>
<td><p>Ulteriori informazioni sull'errore.</p>
<p>Questi dati possono essere convertiti in formato testo utilizzando la sintassi seguente:</p>
<p><code>cast(cast(Detail as varbinary(max)) as varchar(max)) </code></p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Versione client dell'endpoint che invia la segnalazione dell'errore. Per ulteriori informazioni, vedere <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsCapturedByServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Si tratta della segnalazione errori acquisita dall'agente CDR in esecuzione nel Front End Server o inviato dal client.</p></td>
</tr>
<tr class="even">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Riservato per utilizzi futuri.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>Identificatore univoco di correlazione delle informazioni sul tempo di partecipazione per i diversi componenti coinvolti in una conferenza.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Tempo (in millisecondi) richiesto da un componente specifico per partecipare a una conferenza.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Rappresenta il nome di dominio completo del server che ha generato la segnalazione dell'errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Rappresenta il nome di dominio completo del pool in cui è stata generata la segnalazione dell'errore.</p></td>
</tr>
</tbody>
</table>

