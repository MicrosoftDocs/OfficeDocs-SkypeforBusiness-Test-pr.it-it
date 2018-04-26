---
title: 'Lync Server 2013: Tabella MediationServers'
TOCTitle: Tabella MediationServers
ms:assetid: 9f757377-ab79-4795-aaa9-1163cb9c8a59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412743(v=OCS.15)
ms:contentKeyID: 49301487
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella MediationServers in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella MediationServers è una tabella di supporto. In ogni record sono archiviate informazioni su un Mediation Server coinvolto in chiamate con record nel database.


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
<td><p><strong>MediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica questo Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>MediationServer</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p> </p></td>
<td><p>Nome del Mediation Server.</p></td>
</tr>
</tbody>
</table>

