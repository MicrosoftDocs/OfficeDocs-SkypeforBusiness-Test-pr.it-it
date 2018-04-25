---
title: 'Lync Server 2013: Tabella Servers'
TOCTitle: Tabella Servers
ms:assetid: 1535e676-a647-4606-bc56-e8bfde5ca823
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398223(v=OCS.15)
ms:contentKeyID: 49299780
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Servers in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Servers è una tabella di supporto in cui sono archiviate le informazioni relative ai diversi server. Ogni record della tabella rappresenta un server.


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
<td><p><strong>ServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il server.</p></td>
</tr>
<tr class="even">
<td><p><strong>ServerFQDN</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p> </p></td>
<td><p>FQDN del server.</p></td>
</tr>
</tbody>
</table>

