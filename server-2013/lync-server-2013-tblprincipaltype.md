---
title: 'Lync Server 2013: tblPrincipalType'
TOCTitle: tblPrincipalType
ms:assetid: 32e1c1d6-80f4-4624-bf4e-b4c77d3982fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558633(v=OCS.15)
ms:contentKeyID: 49300124
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPrincipalType in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella tblPrincipalType sono inclusi i tipi di entità per classificare gli elementi contenuti nella tabella tblPrincipal.

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
<td><p>ptypeID</p></td>
<td><p>smallint, not null</p></td>
<td><p>ID del tipo di entità.</p></td>
</tr>
<tr class="even">
<td><p>ptypeDesc</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>Descrizione del tipo.</p></td>
</tr>
<tr class="odd">
<td><p>ptypeIsSystemUser</p></td>
<td><p>bit, not null</p></td>
<td><p>True se il tipo corrisponde alle entità usate per scopi interni.</p></td>
</tr>
<tr class="even">
<td><p>ptypeIsUser</p></td>
<td><p>bit, not null</p></td>
<td><p>True se il tipo è un tipo utente.</p></td>
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
<td><p>ptypeID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>


### Valori principali

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID</th>
<th>Ruolo</th>
<th>Descrizione</th>
<th>User</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Entità generica senza tipo conosciuto. Non usata nella tabella tblPrincipal.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>AnyUser</p></td>
<td><p>Entità generica di tipo utente. Non usate nella tabella tblPrincipal.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>AnyGroup</p></td>
<td><p>Entità generica con semantica di gruppo. Non usata nella tabella tblPrincipal.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>SystemUser</p></td>
<td><p>Entità usata internamente da server Chat persistente.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>User</p></td>
<td><p>Utente normale.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>DC</p></td>
<td><p>Controller di dominio di Servizi di dominio Active Directory.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>Gruppo</p></td>
<td><p>Gruppo di sicurezza di Active Directory.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>Folder</p></td>
<td><p>Contenitore o unità organizzativa di Active Directory.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[tblPrincipal in Lync Server 2013](lync-server-2013-tblprincipal.md)

