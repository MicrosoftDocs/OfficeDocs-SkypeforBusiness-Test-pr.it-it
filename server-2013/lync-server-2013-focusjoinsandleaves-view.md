---
title: Visualizzazione FocusJoinsAndLeaves
TOCTitle: Visualizzazione FocusJoinsAndLeaves
ms:assetid: 226460ef-766f-4d61-80cb-f332b65a210d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687992(v=OCS.15)
ms:contentKeyID: 49887476
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione FocusJoinsAndLeaves

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La visualizzazione FocusJoinsAndLeaves contiene informazioni sulle partecipazioni e le uscite per una conferenza. In questa visualizzazione ogni conferenza è rappresentata da un record scritto ogni volta che un utente partecipa o esce da una conferenza. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p>Ora dell'istanza della conferenza. Utilizzata insieme a SessionIdSeq per identificare in modo univoco una istanza della conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero ID per identificare l'istanza della conferenza. Utilizzata insieme a SessionIdTime per identificare in modo univoco un'istanza della conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite. Per ulteriori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tenant dell'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite. Per ulteriori informazioni, vedere <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Identificatore univoco dell'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientVersion</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Versione del client usato dall'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserClientType</strong></p></td>
<td><p>int</p></td>
<td><p>Client usato dall'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite. Per ulteriori informazioni, vedere <a href="lync-server-2013-useragentdef-table.md">Tabella UserAgentDef in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>Nome della categoria del client usato dall'utente le cui informazioni di partecipazione o uscita da una conferenza sono state acquisite.</p></td>
</tr>
<tr class="even">
<td><p><strong>FocusUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><strong>IsuserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p>Bit che indica se l'utente è un utente interno o meno.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora di richiesta della sessione. Utilizzata insieme a SessionIdSeq per identificare in modo univoco una sessione. Vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Se un utente è connesso a più computer o dispositivi contemporaneamente, UserInstance consente di identificare in modo univoco la combinazione utente/dispositivo.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogId</strong></p></td>
<td><p>varchar(775)</p></td>
<td><p>ID del dialogo SIP della sessione. Il formato è: dialog;from-tag;to-tag.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora in cui l'utente inizia a partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora in cui l'utente esce dalla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserRole</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Ruolo dell'utente nella conferenza, ad esempio relatore o partecipante.</p></td>
</tr>
</tbody>
</table>

