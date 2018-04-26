---
title: 'Lync Server 2013: Tabella EndpointSubnet'
TOCTitle: Tabella EndpointSubnet
ms:assetid: d62e51d6-2117-4c41-adce-08f8d9d75ce0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398933(v=OCS.15)
ms:contentKeyID: 49302104
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella EndpointSubnet in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella EndpointSubnet è una tabella di supporto. Ogni record rappresenta una subnet acquisita da endpoint.


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
<td><p>Rappresentazione Integer per la subnet.</p></td>
</tr>
<tr class="even">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Solo per uso interno.</p></td>
</tr>
</tbody>
</table>

