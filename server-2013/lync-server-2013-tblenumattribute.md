---
title: 'Lync Server 2013: tblEnumAttribute'
TOCTitle: tblEnumAttribute
ms:assetid: 17f8b87e-36a6-4f6a-8630-7c76b61a7595
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558617(v=OCS.15)
ms:contentKeyID: 49299812
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblEnumAttribute in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblEnumAttribute è una tabella hardcoded in cui sono inclusi gli attributi Visibility e Behavior utilizzati nella tabella Node.

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
<td><p>attributeID</p></td>
<td><p>smallint, not null</p></td>
<td><p>ID dell'attributo.</p></td>
</tr>
<tr class="even">
<td><p>attributeName</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>Nome dell'attributo.</p></td>
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
<td><p>attributeID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>


### Valori della tabella

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>attributeID</th>
<th>attributeName</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Visibility.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Behavior.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[tblNode in Lync Server 2013](lync-server-2013-tblnode.md)

