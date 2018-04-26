---
title: Visualizzazione ConferenceMessageCount
TOCTitle: Visualizzazione ConferenceMessageCount
ms:assetid: 8ee3ee95-fb78-4d4e-bcdd-6ce5a0a23b44
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688129(v=OCS.15)
ms:contentKeyID: 49887651
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione ConferenceMessageCount

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La vista ConferenceMessageCount archivia informazioni sul numero di messaggi inviati da un utente a una conferenza. Questa vista è stata introdotta in Microsoft Lync Server 2013.


> [!NOTE]
> La vista ConferenceMessageCount contiene tutte le colonne della <A href="lync-server-2013-conferencesessiondetails-view.md">Visualizzazione ConferenceSessionDetails</A> oltre alle colonne indicate di seguito.




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
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente che ha inviato il messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente che ha inviato il messaggio. Per ulteriori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserTenant</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Tenant dell'utente che ha inviato i messaggi. Per ulteriori informazioni, vedere <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserMessageCount</strong></p></td>
<td><p>smallint</p></td>
<td><p>Numero di messaggi inviati dall'utente durante la sessione di conferenza.</p></td>
</tr>
</tbody>
</table>

