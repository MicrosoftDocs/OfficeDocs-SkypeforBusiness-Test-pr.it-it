---
title: 'Lync Server 2013: tblPrincipalMemberDifference'
TOCTitle: tblPrincipalMemberDifference
ms:assetid: 0b94f555-6888-4fe0-a048-4660a2513276
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558612(v=OCS.15)
ms:contentKeyID: 49299650
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPrincipalMemberDifference in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblPrincipalMemberDifference contiene e le modifiche relative ai membri dei gruppi (membri sia aggiunti che rimossi) non ancora elaborate dai successivi passaggi di sincronizzazione di Servizi di dominio Active Directory.

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
<td><p>GUID entità del gruppo modificato.</p></td>
</tr>
<tr class="even">
<td><p>memberADPath</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome distinto del membro.</p></td>
</tr>
<tr class="odd">
<td><p>memberRemoved</p></td>
<td><p>bit, not null</p></td>
<td><p>False se il membro è stato aggiunto. True se il membro è stato rimosso.</p></td>
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
<td><p>&lt;prinGuid, memberADPath&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

