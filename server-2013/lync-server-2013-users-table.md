---
title: 'Lync Server 2013: Tabella Users'
TOCTitle: Tabella Users
ms:assetid: a8d71373-4b57-4245-9f02-f7fc0d9fcd3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412791(v=OCS.15)
ms:contentKeyID: 49301594
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Users in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Users è una tabella di supporto. In ogni record della tabella sono archiviate le informazioni relative a un utente che ha partecipato a chiamate o sessioni con record nel database.


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
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Indicatore data/ora per uso interno.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p> </p></td>
<td><p>URI utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>TenantId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID tenant dell'utente. Per ulteriori informazioni, vedere <a href="lync-server-2013-tenants-table.md">Tabella Tenants in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UriTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Tipo URI dell'utente. Per ulteriori informazioni, vedere <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

