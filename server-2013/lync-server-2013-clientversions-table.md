---
title: 'Lync Server 2013: Tabella ClientVersions'
TOCTitle: Tabella ClientVersions
ms:assetid: 542316cf-a6db-4d52-ab28-8bf6d27a3b48
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398356(v=OCS.15)
ms:contentKeyID: 49300528
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ClientVersions in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella ClientVersions è una tabella di supporto in cui è archiviato un elenco dei diversi tipi di client e delle versioni che hanno partecipato alle sessioni registrate nel database. Ogni record della tabella rappresenta una versione client.


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
<td><p><strong>VersionId</strong></p></td>
<td><p><strong>int</strong></p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il tipo di client e la versione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Version</strong></p></td>
<td><p><strong>nvarchar(256)</strong></p></td>
<td><p></p></td>
<td><p>Nome della versione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica il tipo di client usato nella sessione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-useragentdef-table.md">Tabella UserAgentDef in Lync Server 2013</a>.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

