---
title: 'Lync Server 2013: Tabella ErrorDef'
TOCTitle: Tabella ErrorDef
ms:assetid: 6acf3b86-da61-4923-9812-300db6f66dec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398503(v=OCS.15)
ms:contentKeyID: 49300876
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ErrorDef in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella ErrorDef sono archiviate informazioni su ogni tipo di errore che può verificarsi. Ogni record rappresenta un tipo di errore.


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
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>ID univoco che identifica questo tipo di errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Codice di risposta SIP standard associato all'errore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>ID diagnostica Microsoft.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallTypeId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Tipo della chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-calltype-table.md">Tabella CallType in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RequestType</strong></p></td>
<td><p>varbinary(33)</p></td>
<td><p> </p></td>
<td><p>Tipo della richiesta non riuscita.</p>
<p>Questi dati possono essere convertiti in formato testo utilizzando la sintassi seguente:</p>
<p><code>cast(cast(RequestType as varbinary(max)) as varchar(max))</code></p></td>
</tr>
<tr class="even">
<td><p><strong>ContentType</strong></p></td>
<td><p>varbinary(257)</p></td>
<td><p> </p></td>
<td><p>Tipo di contenuto della richiesta non riuscita.</p>
<p>Questi dati possono essere convertiti in formato testo tramite la sintassi seguente:</p>
<p><code>cast(cast(ContentType as varbinary(max)) as varchar(max))</code></p></td>
</tr>
</tbody>
</table>

