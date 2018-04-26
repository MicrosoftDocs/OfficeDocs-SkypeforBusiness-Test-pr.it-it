---
title: 'Lync Server 2013: Tabella AppliedBandwidthSource'
TOCTitle: Tabella AppliedBandwidthSource
ms:assetid: 24fb3caf-19b3-4c0a-90d7-ca5d53de32ad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425725(v=OCS.15)
ms:contentKeyID: 49299948
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella AppliedBandwidthSource in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella AppliedBandwidthSource è una tabella di supporto. Ogni record rappresenta un'origine.


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
<td><p><strong>AppliedBandwidthSourceKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthSource</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>Univoco</p></td>
<td><p>Origine del limite della larghezza di banda imposto. Descrive l'origine del limite della larghezza di banda, ad esempio &quot;Policy Server&quot;, &quot;TURN Server&quot; o &quot;Modality&quot;.</p></td>
</tr>
</tbody>
</table>

