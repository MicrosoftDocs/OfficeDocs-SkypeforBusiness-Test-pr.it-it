---
title: Visualizzazione McuJoinsAndLeaves
TOCTitle: Visualizzazione McuJoinsAndLeaves
ms:assetid: 6f00b8e7-b8b6-4657-ac5e-d8a571806ae2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688088(v=OCS.15)
ms:contentKeyID: 49887601
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione McuJoinsAndLeaves

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La visualizzazione McuJoinsAndLeaves contiene informazioni sulla partecipazione e l'abbandono da parte degli utenti in un server per conferenze. In ogni record di questa visualizzazione sono inclusi dettagli di chiamata su una combinazione di partecipazione o abbandono di un utente e un server per conferenze. La visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data e ora dell'istanza di conferenza. Valore utilizzato insieme a SessionIdSeq per identificare in modo univoco un'istanza di conferenza. Per maggiori informazioni, vedere <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero ID per identificare l'istanza di conferenza. Valore utilizzato insieme a SessionIdTime per identificare in modo univoco un'istanza di conferenza. Per maggiori informazioni, vedere <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuUri</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>URI del server per le conferenze al quale l'utente è connesso.</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>URI del server per le conferenze al quale l'utente è connesso. Per ulteriori informazioni, vedere la tabella <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte. Per ulteriori informazioni, vedere la tabella <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tenant dell'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte. Per ulteriori informazioni, vedere la tabella <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Versione del client utilizzato dall'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientType</strong></p></td>
<td><p>int</p></td>
<td><p>Client utilizzato dall'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte. Per ulteriori informazioni, vedere la tabella <a href="lync-server-2013-useragentdef-table.md">Tabella UserAgentDef in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>Nome di categoria del client utilizzato dall'utente le cui informazioni di accesso e abbandono relative al server per le conferenze sono state raccolte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>McuUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p>Identifica in maniera univoca la combinazione utente/dispositivo per gli utenti connessi a più di un dispositivo contemporaneamente.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsUserFromPstn</strong></p></td>
<td><p>bit</p></td>
<td><p>Bit che determina se l'utente è interno o meno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data e ora della richiesta di sessione. Valore utilizzato insieme a SessionIdSeq per identificare in modo univoco una sessione. Per maggiori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero ID per identificare la sessione. Valore utilizzato insieme a SessionIdTime per identificare in modo univoco una sessione. Per maggiori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>ID dialogo SIP della sessione, nel formato: dialog;from-tag;to-tag.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora di connessione dell'utente al server per conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora di disconnessione dell'utente dal server per conferenze.</p></td>
</tr>
</tbody>
</table>

