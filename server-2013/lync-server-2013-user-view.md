---
title: Visualizzazione User
TOCTitle: Visualizzazione User
ms:assetid: 796f77e6-1da6-4969-b18b-3537209a1fe4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688100(v=OCS.15)
ms:contentKeyID: 49887615
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione User

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella Visualizzazione utente sono archiviate le informazioni relative agli utenti che hanno partecipato a chiamate o sessioni con record nel database. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p>UserId</p></td>
<td><p>int</p></td>
<td><p>Numero univoco che identifica l'utente.</p></td>
</tr>
<tr class="even">
<td><p>UserUri</p></td>
<td><p>nvarchar(450)</p></td>
<td><p>Uri dell'utente.</p></td>
</tr>
<tr class="odd">
<td><p>TenantKey</p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Tenant dell'utente. Per ulteriori informazioni, vedere <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>UriType</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo dell'URI dell'utente. Per maggiori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

