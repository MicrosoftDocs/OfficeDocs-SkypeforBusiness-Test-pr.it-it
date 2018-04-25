---
title: 'Lync Server 2013: tblPrincipal'
TOCTitle: tblPrincipal
ms:assetid: 79a24502-b4ce-41f0-8979-8caddf535338
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558667(v=OCS.15)
ms:contentKeyID: 49301058
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPrincipal in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Principal contiene tutte le entità, inclusi gli utenti, le cartelle e i gruppi.

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
<td><p>prinID</p></td>
<td><p>int, not null</p></td>
<td><p>ID entità.</p></td>
</tr>
<tr class="even">
<td><p>prinGuid</p></td>
<td><p>GUID, not null</p></td>
<td><p>GUID dell'entità. Valore ampiamente utilizzato come chiave primaria alternativa perché il suo significato corrisponde a quello nell'ambito di Servizi di dominio Active Directory. Il GUID per un'entità memorizzata nella cache equivale al GUID oggetto Active Directory corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p>prinUri</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>URI dell'entità. Lo schema SIP viene utilizzato per gli utenti, mentre ma-grp viene utilizzato per quasi tutte le altre entità.</p></td>
</tr>
<tr class="even">
<td><p>prinName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome comune. Valore utilizzato solo dai tipi utente.</p></td>
</tr>
<tr class="odd">
<td><p>prinDisplayName</p></td>
<td><p>Nvarchar (256)</p></td>
<td><p>Nome visualizzato. Valore utilizzato solo dai tipi utente.</p></td>
</tr>
<tr class="even">
<td><p>prinCompanyName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome della società. Valore utilizzato solo dai tipi utente.</p></td>
</tr>
<tr class="odd">
<td><p>prinEmail</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Posta elettronica. Valore utilizzato solo dai tipi utente.</p></td>
</tr>
<tr class="even">
<td><p>prinADPath</p></td>
<td><p>nvarchar(384)</p></td>
<td><p>Nome di dominio dell'oggetto Active Directory di cui l'entità è una versione memorizzata nella cache. Può essere Null per i tipi che non sono oggetti Active Directory, ad esempio gli utenti di sistema.</p></td>
</tr>
<tr class="odd">
<td><p>prinADUserPrincipalName</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome dell'entità dell'utente. Valore utilizzato solo dai tipi utente normali.</p></td>
</tr>
<tr class="even">
<td><p>prinDisabled</p></td>
<td><p>smallint, not null</p></td>
<td><ul>
<li><p>0: Principale attivo.</p></li>
<li><p>1: Principale è disabilitato poiché le funzionalità SIP dell'utente sono disabilitate.</p></li>
<li><p>2: Principale è eliminato poiché l'oggetto AD associato è stato eliminato.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>prinTypeID</p></td>
<td><p>smallint, not null</p></td>
<td><p>Tipo di entità (dalla tabella PrincipalType).</p></td>
</tr>
<tr class="even">
<td><p>prinPoolID</p></td>
<td><p>Int</p></td>
<td><p>Assegnazione del pool di Lync per il principale.</p></td>
</tr>
<tr class="odd">
<td><p>prinPolicyID</p></td>
<td><p>Int</p></td>
<td><p>Valore del criterio del server Chat persistente per l'utente, se il tipo di criterio tag è presente.</p></td>
</tr>
<tr class="even">
<td><p>prinAddedBy</p></td>
<td><p>int</p></td>
<td><p>ID entità del creatore.</p></td>
</tr>
<tr class="odd">
<td><p>prinAddedOn</p></td>
<td><p>bigint, not null</p></td>
<td><p>Indicatore di data e ora per il momento della creazione.</p></td>
</tr>
<tr class="even">
<td><p>prinUpdatedBy</p></td>
<td><p>int</p></td>
<td><p>ID dell'entità che ha eseguito l'ultimo aggiornamento.</p></td>
</tr>
<tr class="odd">
<td><p>prinUpdatedOn</p></td>
<td><p>bigint, not null</p></td>
<td><p>Indicatore di data e ora per l'ultimo aggiornamento.</p></td>
</tr>
<tr class="even">
<td><p>prinVerifiedOn</p></td>
<td><p>datetime, not null</p></td>
<td><p>Data e ora dell'ultimo aggiornamento di Sincronizzazione Active Directory per l'entità.</p></td>
</tr>
</tbody>
</table>


### Chiavi

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
<td><p>prinID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>prinTypeID</p></td>
<td><p>Chiave esterna con ricerca nella tabella PrincipalType.ptypeID.</p></td>
</tr>
</tbody>
</table>

