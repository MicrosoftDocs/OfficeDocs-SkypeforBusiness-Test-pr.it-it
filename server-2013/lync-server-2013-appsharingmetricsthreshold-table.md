---
title: Tabella AppSharingMetricsThreshold in Lync Server 2013
TOCTitle: Tabella AppSharingMetricsThreshold
ms:assetid: 782cfab9-01a6-4843-aea1-28f47b0b51f7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205018(v=OCS.15)
ms:contentKeyID: 49301037
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella AppSharingMetricsThreshold in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella AppSharingMetricsThreshold contiene i valori ottimali e accettabili delle metriche QoE utilizzate con la condivisione delle applicazioni. Questi valori soglia sono utilizzati per determinare se l'esperienza di condivisione deve essere classificata come insufficiente.

Questa tabella è stato introdotta in Microsoft Lync Server 2013.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Column</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CallType</strong></p></td>
<td><p>int</p></td>
<td><p>Primario</p></td>
<td><p>Tipo di chiamata effettuata.</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthLimitOptimal</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Limitazione ottimale della larghezza di banda per la condivisione delle applicazioni. Il valore predefinito è 1000000.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AppliedBandwidthLimitAcceptable</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Limitazione accettabile della larghezza di banda per la condivisione delle applicazioni. Il valore predefinito è 500000.</p></td>
</tr>
<tr class="even">
<td><p><strong>SpoiledTilePercentTotalOptimal</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Tasso percentuale ottimale delle sezioni “danneggiate” per la classificazione della qualità di una condivisione delle applicazioni. Questo valore rappresenta la percentuale di contenuto del condivisore che non ha raggiunto il visualizzatore. Il contenuto potrebbe essere scartato (o danneggiato) rispettivamente quando il condivisore scarta le sezioni dall'origine grafica o ASMCU scarica le sezioni dal condivisore. Il valore predefinito è 11 percento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SpoiledTilePercentTotalAcceptable</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Tasso percentuale accettabile delle sezioni “danneggiate” per la classificazione della qualità di una condivisione delle applicazioni. Questo valore rappresenta la percentuale di contenuto del condivisore che non ha raggiunto il visualizzatore. Il contenuto potrebbe essere scartato (o danneggiato) rispettivamente quando il condivisore scarta le sezioni dall'origine grafica o ASMCU scarica le sezioni dal condivisore. Il valore predefinito è 36 percento.</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalOptimal</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrivalAcceptable</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstDensityOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstDensityAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyBurstDensityOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyBurstDensityAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Questa colonna non è utilizzata in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayAverageOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Valore ottimale per il ritardo unidirezionale relativo tra i due endpoint multimediali coinvolti nella condivisione delle applicazioni. È una misura della latenza a hop singolo. Il valore predefinito è 1,0 secondi.</p>
<p>La colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayAverageAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Valore ottimale per il ritardo unidirezionale relativo tra i due endpoint multimediali coinvolti nella condivisione delle applicazioni. È una misura della latenza a hop singolo. Il valore predefinito è 1,75 secondi.</p>
<p>La colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RDPTileProcessingLatencyAverageOptimal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Latenza ottimale di elaborazione delle sezioni RDP nel server per conferenze di Condivisione applicazioni per tutta la durata della sessione di visualizzazione. Tale metrica non contempla la latenza della rete.</p>
<p>Una media elevata è sintomo di un ritardo superiore nell'esperienza di visualizzazione. In un server per conferenze sovraccarico possono verificarsi ritardi medi superiori. Il valore predefinito è 200 ms.</p>
<p>La colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RDPTileProcessingLatencyAverageAcceptable</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Latenza accettabile di elaborazione delle sezioni RDP nel server per conferenze di Condivisione applicazioni per tutta la durata della sessione di visualizzazione. Tale metrica non contempla la latenza della rete.</p>
<p>Una media elevata è sintomo di un ritardo superiore nell'esperienza di visualizzazione. In un server per conferenze sovraccarico possono verificarsi ritardi medi superiori. Il valore predefinito è 200 ms.</p>
<p>La colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

