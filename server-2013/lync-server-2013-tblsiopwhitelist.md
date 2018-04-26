---
title: 'Lync Server 2013: tblSiopWhiteList'
TOCTitle: tblSiopWhiteList
ms:assetid: 05fc1df4-32eb-4d46-9d1c-e0b607091142
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558607(v=OCS.15)
ms:contentKeyID: 49299564
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblSiopWhiteList in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblSiopWhiteList è l'elenco dei componenti aggiuntivi registrati che possono essere associati ai nodi.

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
<td><p>siopID</p></td>
<td><p>GUID, not null</p></td>
<td><p>GUID del componente aggiuntivo.</p></td>
</tr>
<tr class="even">
<td><p>siopName</p></td>
<td><p>nvarchar (50), not null</p></td>
<td><p>Nome visualizzato del componente aggiuntivo.</p></td>
</tr>
<tr class="odd">
<td><p>siopUrl</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>URL del componente aggiuntivo.</p></td>
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
<td><p>siopID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

