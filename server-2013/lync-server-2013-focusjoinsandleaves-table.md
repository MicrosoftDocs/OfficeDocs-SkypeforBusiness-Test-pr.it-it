---
title: 'Lync Server 2013: Tabella FocusJoinsAndLeaves'
TOCTitle: Tabella FocusJoinsAndLeaves
ms:assetid: e6f0212c-67e9-4061-8720-d0296e855991
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399026(v=OCS.15)
ms:contentKeyID: 49302313
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella FocusJoinsAndLeaves in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In ogni record di questa tabella sono contenute le informazioni CDR sulla partecipazione e l'abbandono di una conferenza da parte di un utente. Ogni conferenza è rappresentata in questa tabella da un record per ogni volta che un utente partecipa alla conferenza o la abbandona.


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
<td><p><strong>DialogSessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>DialogSessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero di ID per identificare la sessione. Valore utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero univoco che identifica l'utente, a cui viene fatto riferimento dalla <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>FocusUserInstance</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Se un utente è connesso a più computer o dispositivi contemporaneamente, <strong>UserInstance</strong> consente di identificare in modo univoco la combinazione utente/dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsUserInternal</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Indica se l'utente è connesso o meno dall'interno.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserRole</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Ruolo dell'utente nella conferenza, ad esempio relatore o partecipante.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserJoinTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora in cui l'utente inizia a partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserLeaveTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Ora in cui l'utente lascia la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientVerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Versione del software client dell'utente. Riferimento alla <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserEndpointId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>Identificatore univoco globale (GUID) dell'endpoint utilizzato nella conferenza.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

