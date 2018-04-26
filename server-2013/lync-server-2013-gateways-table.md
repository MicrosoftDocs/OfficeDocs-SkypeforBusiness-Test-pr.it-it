---
title: 'Lync Server 2013: Tabella Gateways'
TOCTitle: Tabella Gateways
ms:assetid: a909daad-d137-45e0-b149-1de9f8e1e029
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412795(v=OCS.15)
ms:contentKeyID: 49301602
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Gateways in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Gateways è una tabella di supporto. In ogni record sono archiviate informazioni su un gateway utilizzato in chiamate della rete PSTN (Public Switched Telephone Network) con record nel database.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Chiave/indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il gateway.</p></td>
</tr>
<tr class="even">
<td><p><strong>Gateway</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p> </p></td>
<td><p>Nome del gateway.</p></td>
</tr>
</tbody>
</table>

