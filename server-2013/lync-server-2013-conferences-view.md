---
title: Visualizzazione Conferences
TOCTitle: Visualizzazione Conferences
ms:assetid: c0e5c4db-c135-401f-9296-e9a49f6499a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721871(v=OCS.15)
ms:contentKeyID: 49887733
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione Conferences

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione Conferences vengono archiviate le informazioni relative alle conferenze. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p>Data e ora della richiesta di sessione. Valore utilizzato con SessionIdSeq per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Numero di ID per identificare la sessione. Valore utilizzato con SessionIdTime per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI della conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceUriType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI della conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Valore utilizzato per le conferenze ricorrenti. A ogni istanza di una conferenza ricorrente viene assegnato lo stesso ConferenceUri, ma il valore ConfInstance è diverso.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceStartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data e ora di inizio della conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data e ora di fine della conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>URI dell'utente che ha organizzato la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrganizerType</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di URI dell'utente che ha organizzato la conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerTenant</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tenant dell'utente che ha organizzato la conferenza. Per ulteriori informazioni, vedere <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome di dominio completo del pool che ha ospitato la conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p>Maschera di bit che contiene gli attributi della conferenza. I valori possibili sono:</p>
<p>0X01 - Transazione sintetica</p></td>
</tr>
</tbody>
</table>

