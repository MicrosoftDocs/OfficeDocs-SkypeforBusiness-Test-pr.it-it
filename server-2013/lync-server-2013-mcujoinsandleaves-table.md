---
title: 'Lync Server 2013: Tabella McuJoinsAndLeaves'
TOCTitle: Tabella McuJoinsAndLeaves
ms:assetid: 4e073366-0b5d-45b4-a3f6-d63dd5fd9f25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398316(v=OCS.15)
ms:contentKeyID: 49300504
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella McuJoinsAndLeaves in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In ogni record di questa tabella sono inclusi dettagli di chiamata su una combinazione di partecipazione o abbandono di un utente e un server per conferenze. Ad esempio, se un utente partecipa a una conferenza contenente elementi di conferenza Web ed elementi audio/video, verrà creato un record per la partecipazione dell'utente alla conferenza Web e un altro record verrà creato per la partecipazione dell'utente alla conferenza audio/video.


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
<td><p>datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Ora dell'istanza della conferenza. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco un'istanza di conferenza. Vedere la <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero di ID per identificare l'istanza della conferenza. Valore utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco l'istanza della conferenza. Vedere la <a href="lync-server-2013-conferences-table.md">Tabella Conferences in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero univoco che identifica l'utente. Per ulteriori informazioni, vedere la <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Se un utente è connesso contemporaneamente a più utenti o dispositivi, McuUserInstance identifica in modo univoco la combinazione utente/dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsFromPstn</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Indica se l'utente partecipa o meno da un PSTN.</p></td>
</tr>
<tr class="even">
<td><p><strong>McuId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero univoco che identifica questo server per conferenze. Per ulteriori informazioni, vedere la <a href="lync-server-2013-mcus-table.md">Tabella Mcus in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Esterna</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di ID per identificare la sessione. Utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora di accesso dell'utente al server per conferenze.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora di disconnessione dell'utente dal server per conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Identificatore che specifica il numero di versione del software client usato nella conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

