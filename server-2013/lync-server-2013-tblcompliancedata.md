---
title: 'Lync Server 2013: tblComplianceData'
TOCTitle: tblComplianceData
ms:assetid: 05b28f9b-4aba-4b69-ba8d-2ceeb6cbfaac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558606(v=OCS.15)
ms:contentKeyID: 49299554
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblComplianceData in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblComplianceData contiene gli eventi di conformità ancora non elaborati dall'adattatore di conformità.

### Colonne

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>cmplEventID</p></td>
<td><p>bigint, not null</p></td>
<td><p>ID evento.</p></td>
</tr>
<tr class="even">
<td><p>entryDate</p></td>
<td><p>smalldatetime, not null</p></td>
<td><p>Data/ora di inserimento (può essere molto lontana nel futuro per cmplType=9, poiché in tal caso la voce è solo un segnaposto).</p></td>
</tr>
<tr class="odd">
<td><p>cmplType</p></td>
<td><p>int, not null</p></td>
<td><p>Tipo di evento di conformità:</p>
<ul>
<li><p>1: chat</p></li>
<li><p>2: dialogo della chat</p></li>
<li><p>3: download di file</p></li>
<li><p>4: caricamento di file</p></li>
<li><p>9: trasferimento file provvisorio</p></li>
<li><p>10: eliminazione della chat (con sostituzione)</p></li>
<li><p>11: eliminazione della chat</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>cmplTime</p></td>
<td><p>bigint, not null</p></td>
<td><p>Data e ora dell'evento.</p></td>
</tr>
<tr class="odd">
<td><p>cmplChannelUri</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>URI (Uniform Resource Identifier) del canale.</p></td>
</tr>
<tr class="even">
<td><p>cmplChatID</p></td>
<td><p>bigint</p></td>
<td><p>ID chat (corrispondente alla tabella tblChat.chatId).</p></td>
</tr>
<tr class="odd">
<td><p>cmplUserID</p></td>
<td><p>int, not null</p></td>
<td><p>ID entità di chi effettua l'invio (corrispondente alla tabella tblPrincipal.prinID).</p></td>
</tr>
<tr class="even">
<td><p>cmplUserUri</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>URI utente.</p></td>
</tr>
<tr class="odd">
<td><p>cmplMessage</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>Messaggio (la codifica dipende da cmplType).</p></td>
</tr>
</tbody>
</table>


### Chiave

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>cmplEventID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

