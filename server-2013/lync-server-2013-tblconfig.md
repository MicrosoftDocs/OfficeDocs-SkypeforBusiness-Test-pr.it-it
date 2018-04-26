---
title: 'Lync Server 2013: tblConfig'
TOCTitle: tblConfig
ms:assetid: 7445e7db-c574-46fa-b964-8640d77047a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558663(v=OCS.15)
ms:contentKeyID: 49300982
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblConfig in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblConfig contiene configurazioni di server Chat persistente in una riga.

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
<td><p>configLabel</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>Contiene &quot;pool.&quot;</p></td>
</tr>
<tr class="even">
<td><p>configContent</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>Contenuto della configurazione.</p></td>
</tr>
<tr class="odd">
<td><p>configPoolID</p></td>
<td><p>GUID, not null</p></td>
<td><p>ID univoco dell'istanza di database.</p></td>
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
<td><p>configLabel</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

