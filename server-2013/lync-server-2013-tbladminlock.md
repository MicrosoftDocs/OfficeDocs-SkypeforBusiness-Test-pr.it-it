---
title: 'Lync Server 2013: tblAdminLock'
TOCTitle: tblAdminLock
ms:assetid: 785a43c0-6892-474c-821c-fa9cdbeb99d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558665(v=OCS.15)
ms:contentKeyID: 49301042
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblAdminLock in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella AdminLock contiene il blocco dell'amministratore necessario per eseguire alcuni comandi di amministrazione.

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
<td><p>lockExpiresTime</p></td>
<td><p>datetime, not null</p></td>
<td><p>Data e ora di scadenza del blocco. Il proprietario può estendere questo valore periodicamente.</p></td>
</tr>
<tr class="even">
<td><p>lockServerID</p></td>
<td><p>int, not null</p></td>
<td><p>ID del server proprietario del blocco.</p></td>
</tr>
<tr class="odd">
<td><p>lockActorID</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità proprietaria del blocco.</p></td>
</tr>
</tbody>
</table>

