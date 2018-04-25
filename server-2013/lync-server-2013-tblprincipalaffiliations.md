---
title: 'Lync Server 2013: tblPrincipalAffiliations'
TOCTitle: tblPrincipalAffiliations
ms:assetid: 45fd8484-5837-44d2-85bb-45c83546607c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558642(v=OCS.15)
ms:contentKeyID: 49300388
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPrincipalAffiliations in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

tblPrincipalAffiliations contiene le affiliazioni delle entità che descrivono le appartenenze a posizioni, inclusi i gruppi di sicurezza di Servizi di dominio Active Directory, i contenitori di Active Directory e i domini.

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
<td><p>principalID</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità affiliata.</p></td>
</tr>
<tr class="even">
<td><p>affiliationID</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità che rappresenta l'affiliazione. Ogni entità prevede anche un'auto-affiliazione (eccetto system-user-types).</p></td>
</tr>
<tr class="odd">
<td><p>indice</p></td>
<td><p>int, not null</p></td>
<td><p>Indice. Il valore per le auto-affiliazioni è -1 e per le altre affiliazioni aumenta in sequenza a partire da 1 all'interno di ogni bucket &lt;principalID, affiliationId&gt;.</p></td>
</tr>
<tr class="even">
<td><p>updatedBy</p></td>
<td><p>int, not null</p></td>
<td><p>Entità che ha effettuato l'ultimo aggiornamento. Viene utilizzato in genere il valore 1, che indica la sincronizzazione di Active Directory.</p></td>
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
<th>Colonne</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;principalID, index, affiliationID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>principalID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblPrincipal.prinID.</p></td>
</tr>
<tr class="odd">
<td><p>affiliationID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblPrincipal.prinID.</p></td>
</tr>
</tbody>
</table>

