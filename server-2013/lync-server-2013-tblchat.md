---
title: 'Lync Server 2013: tblChat'
TOCTitle: tblChat
ms:assetid: b7fcf1b4-7a3f-4585-a6d9-95e7f030c7dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615031(v=OCS.15)
ms:contentKeyID: 49301757
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblChat in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In tblChat sono inclusi tutti i messaggi di chat.

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
<td><p>channelId</p></td>
<td><p>int, not null</p></td>
<td><p>ID del nodo.</p></td>
</tr>
<tr class="even">
<td><p>chatId</p></td>
<td><p>bigint, not null</p></td>
<td><p>Numero sequenziale univoco (per ID di nodo) che definisce l'ordine delle chat room, generato dalla tabella tblLastChatId.</p></td>
</tr>
<tr class="odd">
<td><p>chatDate</p></td>
<td><p>bigint, not null</p></td>
<td><p>Timestamp per il messaggio chat.</p></td>
</tr>
<tr class="even">
<td><p>userId</p></td>
<td><p>int, not null</p></td>
<td><p>ID di entità dell'autore del post.</p></td>
</tr>
<tr class="odd">
<td><p>isAlert</p></td>
<td><p>bit, not null</p></td>
<td><p>True se il messaggio è un messaggio di avviso. False in caso contrario.</p></td>
</tr>
<tr class="even">
<td><p>content</p></td>
<td><p>nvarchar (max), not null</p></td>
<td><p>Contenuto della chat (versione in testo normale). Il contenuto è solitamente in testo normale con le eccezioni seguenti:</p>
<ul>
<li><p>I file sono rappresentati come collegamenti ma-filelink:.</p></li>
<li><p>I collegamenti sono rappresentati come elemento HTML (sebbene il tipo di contenuto non possa essere considerato HTML).</p></li>
<li><p>I brani sono codificati nel formato &quot;[STORY]....&quot;-like.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>rtf</p></td>
<td><p>varchar(max)</p></td>
<td><p>Contenuto della chat (versione RTF). Può essere Null se il client non lo fornisce.</p></td>
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
<td><p>&lt;channelID, chatID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

