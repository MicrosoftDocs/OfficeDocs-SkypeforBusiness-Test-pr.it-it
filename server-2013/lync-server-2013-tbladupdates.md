---
title: 'Lync Server 2013: tblADUpdates'
TOCTitle: tblADUpdates
ms:assetid: ba19fa16-4d2d-4635-ac32-f93e09469546
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615033(v=OCS.15)
ms:contentKeyID: 49301783
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblADUpdates in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In tblADUpdates sono incluse le modifiche di Servizi di dominio Active Directory non ancora elaborate dalle successive operazioni di sincronizzazione di Active Directory.

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
<td><p>prinGuid</p></td>
<td><p>GUID, not null</p></td>
<td><p>GUID di entità dell'oggetto modificato.</p></td>
</tr>
<tr class="even">
<td><p>prinADPath</p></td>
<td><p>nvarchar (384), not null</p></td>
<td><p>Nome distinto dell'oggetto.</p></td>
</tr>
<tr class="odd">
<td><p>prinAttributesChanged</p></td>
<td><p>bit, not null</p></td>
<td><p>True se viene modificato almeno un attributo dell'oggetto.</p></td>
</tr>
<tr class="even">
<td><p>prinMembersChanged</p></td>
<td><p>bit, not null</p></td>
<td><p>True se l'appartenenza è stata modificata.</p></td>
</tr>
<tr class="odd">
<td><p>prinAffiliationsChanged</p></td>
<td><p>bit, not null</p></td>
<td><p>Non utilizzata.</p></td>
</tr>
<tr class="even">
<td><p>prinDeleted</p></td>
<td><p>bit, not null</p></td>
<td><p>True se l'oggetto è stato modificato.</p></td>
</tr>
<tr class="odd">
<td><p>lastUpdated</p></td>
<td><p>datetime, not null</p></td>
<td><p>Timestamp dell'inserimento della riga.</p></td>
</tr>
</tbody>
</table>

