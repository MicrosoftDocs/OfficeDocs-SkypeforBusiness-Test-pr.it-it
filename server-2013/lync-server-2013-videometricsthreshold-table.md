---
title: Tabella VideoMetricsThreshold in Lync Server 2013
TOCTitle: Tabella VideoMetricsThreshold in Lync Server 2013
ms:assetid: 2e2f4711-35ba-48c6-b15b-5aba61c4eb75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204778(v=OCS.15)
ms:contentKeyID: 49300058
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella VideoMetricsThreshold in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella VideoMetricsThreshold sono contenuti valori ottimali e accettabili per le metriche Quality of Experience usate con le chiamate video.


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
<th><strong>Chiave/Indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CallType</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Tipo di chiamata effettuata.</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoPostFECPLROptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 0.05.</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoPostFECPLRAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 0.10.</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoLocalFrameLostPercentageAverageOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 5.0.</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoLocalFrameLostPercentageAverageAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 10.0.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvFrameRateAverageOptimal</strong></p></td>
<td><p>decimal(9,4)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 12.0000.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvFramerateAverageAcceptable</strong></p></td>
<td><p>decimal(9,4)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 7.0000.</p></td>
</tr>
<tr class="even">
<td><p><strong>LowFrameRateCallPercentOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 5.0.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LowFrameRateCallPercentAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 10.0/</p></td>
</tr>
<tr class="even">
<td><p><strong>LowResolutionCallPercentOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 5.0.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LowResolutionCallPercentAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 10.0.</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoPacketLossRateOptimal</strong></p></td>
<td><p>foat</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 0.05.</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoPacketLossRateAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 0.10.</p></td>
</tr>
<tr class="even">
<td><p><strong>VideoFrameRateAvgOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 12.</p></td>
</tr>
<tr class="odd">
<td><p><strong>VideoFrameRateAvgAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 7.</p></td>
</tr>
<tr class="even">
<td><p><strong>DynamicCapabilityPercentOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 5.00.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DynamicCapabilityPercentAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Il valore predefinito è 10.00.</p></td>
</tr>
</tbody>
</table>

