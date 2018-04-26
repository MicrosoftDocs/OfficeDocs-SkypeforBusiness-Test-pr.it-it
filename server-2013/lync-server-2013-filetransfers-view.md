---
title: Visualizzazione FileTransfers
TOCTitle: Visualizzazione FileTransfers
ms:assetid: e52c3ad0-152e-4a18-af1c-1aff0d205151
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721914(v=OCS.15)
ms:contentKeyID: 49887794
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione FileTransfers

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione FileTranfers sono archiviate informazioni sulle sessioni di trasferimento file peer-to-peer. La visualizzazione è stata introdotta in Microsoft Lync Server 2013.


> [!NOTE]
> La visualizzazione FileTransfers contiene tutte le colonne della <A href="lync-server-2013-sessiondetails-view.md">Visualizzazione SessionDetails</A> oltre alle colonne elencate di seguito.




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
<td><p><strong>FileName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome del file trasferito.</p></td>
</tr>
<tr class="even">
<td><p><strong>Cookie</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p>Valore utilizzato per identificare ogni messaggio successivo come associato a questo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FileIdentity</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Identificatore univoco per distinguere tra i trasferimenti di file che coinvolgono lo stesso nome di file.</p></td>
</tr>
<tr class="even">
<td><p><strong>Accept</strong></p></td>
<td><p>bit</p></td>
<td><p>Può essere TRUE o NULL. Se TRUE, allora Reject e Cancel saranno NULL.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reject</strong></p></td>
<td><p>bit</p></td>
<td><p>Può essere TRUE o NULL. Se TRUE, allora Accept e Cancel saranno NULL.</p></td>
</tr>
<tr class="even">
<td><p><strong>Cancel</strong></p></td>
<td><p>bit</p></td>
<td><p>Può essere TRUE o NULL. Se TRUE, allora Accept e Reject saranno NULL.</p></td>
</tr>
</tbody>
</table>

