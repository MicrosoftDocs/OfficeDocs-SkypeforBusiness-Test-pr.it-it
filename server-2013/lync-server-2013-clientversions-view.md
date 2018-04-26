---
title: Visualizzazione ClientVersions
TOCTitle: Visualizzazione ClientVersions
ms:assetid: caf7678f-83a0-46c8-83cc-fee4c3991f52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721891(v=OCS.15)
ms:contentKeyID: 49887753
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione ClientVersions

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione ClientVersions vengono archiviate informazioni sui diversi tipi di client e sulle relative versioni che hanno partecipato alle sessioni registrate nel database. Ogni record della visualizzazione rappresenta una versione client. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


> [!NOTE]
> Per alcune colonne possono essere presenti più record.




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
<td><p><strong>VersionId</strong></p></td>
<td><p>int</p></td>
<td><p>Numero univoco che identifica il tipo di client e la versione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Version</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Rappresenta l'agente utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientType</strong></p></td>
<td><p>int</p></td>
<td><p>Tipo di client.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientCategory</strong></p></td>
<td><p>nvarchar(64)</p></td>
<td><p>Categoria a cui appartiene il client. Ad esempio, il client Conferencing_Attendant_1.0 appartiene alla categoria (ClientCategory) CAA.</p></td>
</tr>
</tbody>
</table>

