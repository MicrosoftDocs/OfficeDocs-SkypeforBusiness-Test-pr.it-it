---
title: 'Lync Server 2013: Tabella Subnet'
TOCTitle: Tabella Subnet
ms:assetid: 76f5c995-96c8-4aa3-bc30-1d74991d7c42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398582(v=OCS.15)
ms:contentKeyID: 49301024
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Subnet in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Subnet è una tabella di supporto. Ogni record rappresenta una subnet definita nell'impostazione di configurazione di rete.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Colonna</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SubnetIP</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Rappresentazione in forma di numero intero dell'IP della subnet.</p></td>
</tr>
<tr class="even">
<td><p><strong>SubnetMask</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Subnet mask.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserSiteKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-usersite-table.md">Tabella UserSite in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SubnetDescription</strong></p></td>
<td><p>nvarchar(512)</p></td>
<td><p></p></td>
<td><p>Descrizione della subnet.</p></td>
</tr>
</tbody>
</table>

