---
title: Tabella NetworkConnectionDetail in Lync Server 2013
TOCTitle: Tabella NetworkConnectionDetail in Lync Server 2013
ms:assetid: b48cc9a6-5232-48b5-bd20-53b68229336b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205185(v=OCS.15)
ms:contentKeyID: 49301722
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella NetworkConnectionDetail in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella NetworkConnectionDetail i tipi di connessione di rete sono mappati agli identificatori di connessione di rete utilizzati in altre posizioni nel database della qualità percepita dagli utenti (QoE). Questa tabella è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>NetworkConnectionDetailKey</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco del tipo di connessione di rete.</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkConnectionDetail</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>Univoca/o</p></td>
<td><p>Tipo di connessione di rete che corrisponde a NetworkConnectionDetailKey. I valori consentiti sono:</p>
<ol>
<li><p>0 - Cablata</p></li>
<li><p>1 - Wi-Fi</p></li>
<li><p>2 - Ethernet</p></li>
</ol></td>
</tr>
</tbody>
</table>

