---
title: 'Lync Server 2013: Tabella ConferenceSessionDetails'
TOCTitle: Tabella ConferenceSessionDetails
ms:assetid: 9eae6a54-69fd-4966-aa17-7ecee1297ad8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412741(v=OCS.15)
ms:contentKeyID: 49301481
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ConferenceSessionDetails in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta una sessione di conferenza, che può indicare la sessione con Focus o la sessione con un server per conferenze specifico.


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>Datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione di conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero ID per identificare la sessione. Valore utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione di conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.*</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI di conferenza Focus associato alla sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-conferenceuris-table.md">Tabella ConferenceUris in Lync Server 2013</a>. Si tratta di un URI di conferenza basata su Focus.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>Identificare che distingue le istanze di conferenze ricorrenti. Ogni conferenza ricorrente presenta lo stesso valore di ConferenceURI ma un valore diverso di ConfInstance.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI di conferenza del server per conferenze associato alla sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-conferenceuris-table.md">Tabella ConferenceUris in Lync Server 2013</a>. Si tratta di un URI di conferenza basata su server di conferenza. Per le sessioni di conferenza Focus, questa colonna sarà null.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID di un utente nella sessione di conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>GUID per l'identificazione dell'istanza dell'endpoint. Ad esempio, se un utente accede a due computer con lo stesso account, ogni computer disporrà di un ID endpoint diverso.</p></td>
</tr>
<tr class="even">
<td><p><strong>OnBehalfOfId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indica l'ID dell'utente per conto del quale il chiamante esegue la chiamata. Per ulteriori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReferredById</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID dell'utente da quale proviene la chiamata. Per ulteriori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Versione del client utilizzata dall'utente della conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConfClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Versione del client utilizzata dal server per conferenze. Per ulteriori informazioni, vedere <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReplaceDialogIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Esterna</p></td>
<td><p>Numero ID per l'identificazione della finestra di dialogo sostituita dalla sessione corrente. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>ReplaceDialogIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero ID per l'identificazione della sessione. Valore utilizzato in combinazione con <strong>ReplacesDialogIdTime</strong> per identificare in modo univoco una sessione sostituita da questa sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsStartedByConfServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se la sessione è stata avviata dal server per conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsEndedByConfServer</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se la sessione è stata terminata dal server per conferenze.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se l'utente è connesso dall'interno o meno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Codice di risposta SIP (Session Initiation Protocol) all'invito alla sessione. Questo campo viene in genere popolato con i dati generati dal messaggio INVITE iniziale nella sessione. Se non sono presenti messaggi INVITE, il campo viene popolato con data e ora del primo messaggio SIP rilevante (BYE, CANCEL, MESSAGE o INFO).</p></td>
</tr>
<tr class="even">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>ID di diagnostica acquisito dall'intestazione SIP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID del Front End Server utilizzato per questa sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-servers-table.md">Tabella Servers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID del pool in cui è stata acquisita la sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-pools-table.md">Tabella Pools in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Mediation Server utilizzato dalla chiamata. Per ulteriori informazioni, vedere <a href="lync-server-2013-mediationservers-table.md">Tabella MediationServers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>GatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Gateway utilizzato dalla chiamata. Per ulteriori informazioni, vedere <a href="lync-server-2013-gateways-table.md">Tabella Gateways in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Server perimetrale utilizzato dalla chiamata. Per ulteriori informazioni, vedere <a href="lync-server-2013-edgeservers-table.md">Tabella EdgeServers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Tipo di contenuto utilizzato nella sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-contenttypes-table.md">Tabella ContentTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InviteTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Ora della prima richiesta INVITE. Questo campo viene in genere popolato con i dati generati dal messaggio INVITE iniziale nella sessione. Se non sono presenti messaggi INVITE, il campo viene popolato con data e ora del primo messaggio SIP rilevante (BYE, CANCEL, MESSAGE o INFO).</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Ora della prima risposta SIP. Questo campo viene in genere popolato con i dati generati dal messaggio INVITE iniziale nella sessione. Se non sono presenti messaggi INVITE, il campo viene popolato con data e ora del primo messaggio SIP rilevante (BYE, CANCEL, MESSAGE o INFO).</p></td>
</tr>
<tr class="odd">
<td><p><strong>SessionEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Ora di fine della sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>UriTypeId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Esterna</p></td>
<td><p>Contiene il valore di tipo URI MCU dalla <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>. Questo campo è usato per migliorare le prestazioni di query.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Set di bit che indica gli attributi dell'utente. Sono incluse le definizioni di attributo seguenti:</p>
<ul>
<li><p>Integrato con telefono da tavolo - 1</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>CallFlag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Set di bit che indica gli attributi della chiamata. Sono incluse le definizioni di attributo seguenti:</p>
<ul>
<li><p>Sessione ripetuta - 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


\* Per la maggior parte delle sessioni il valore di SessionIdSeq sarà 1. Se più sessioni iniziano esattamente alla stessa ora, il valore SessionIdSeq per una sarà 1, per l'altra sarà 2 e così via.

