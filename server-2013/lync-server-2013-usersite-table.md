---
title: 'Lync Server 2013: Tabella UserSite'
TOCTitle: Tabella UserSite
ms:assetid: 1c2a3cf2-dc05-472e-8097-a31f3a1aafcb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398256(v=OCS.15)
ms:contentKeyID: 49299853
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella UserSite in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella UserSite è una tabella di supporto. Ogni record rappresenta un sito utente definito nell'impostazione di configurazione di rete.


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
<td><p><strong>UserSiteKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il sito utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserSiteName</strong></p></td>
<td><p>nvarchar(128)</p></td>
<td><p>Univoco</p></td>
<td><p>Nome del sito utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RegionKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-region-table.md">Tabella Region in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

