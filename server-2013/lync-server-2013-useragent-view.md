---
title: Visualizzazione UserAgent
TOCTitle: Visualizzazione UserAgent
ms:assetid: b986f76f-f16e-4e5e-96cb-6e8f7f9b42ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721862(v=OCS.15)
ms:contentKeyID: 49887722
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione UserAgent

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione UserAgent vengono archiviate le informazioni relative agli agenti utente coinvolti in sessioni con record nel database. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


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
<td><p>UserAgentKey</p></td>
<td><p>int</p></td>
<td><p>Numero univoco che identifica l'agente utente.</p></td>
</tr>
<tr class="even">
<td><p>UserAgent</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Stringa dell'agente utente.</p></td>
</tr>
<tr class="odd">
<td><p>UAType</p></td>
<td><p>smallint</p></td>
<td><p>Tipo di agente utente. Per ulteriori informazioni, vedere <a href="lync-server-2013-useragent-table.md">Tabella UserAgent in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>UACategory</p></td>
<td><p>nvarchar(64)</p></td>
<td><p>Categoria a cui appartiene l'agente utente. Ad esempio, l'agente utente Conferencing_Attendant_1.0 appartiene alla UACategory CAA.</p></td>
</tr>
</tbody>
</table>

