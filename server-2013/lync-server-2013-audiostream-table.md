---
title: 'Lync Server 2013: Tabella AudioStream'
TOCTitle: Tabella AudioStream
ms:assetid: 49ccbbc3-2f73-45fc-80a6-e612535cbc10
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425961(v=OCS.15)
ms:contentKeyID: 49300423
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella AudioStream in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta un flusso audio. In una linea multimediale audio in genere sono inclusi due flussi audio.


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
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-medialine-table.md">Tabella MediaLine in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>StreamID</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>ID univoco in una linea multimediale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>JitterInterArrival</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Instabilità media della rete dalle statistiche RTCP (Real Time Control Protocol).</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Instabilità di rete massima durante la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketLossRate</strong></p></td>
<td><p>decimal(5,4)</p></td>
<td><p> </p></td>
<td><p>Frequenza media di perdita di pacchetti durante la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>PacketLossRateMax</strong></p></td>
<td><p>decimal(5,4)</p></td>
<td><p> </p></td>
<td><p>Perdita massima di pacchetti osservata durante la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BurstDensity</strong></p></td>
<td><p>decimal(9,4)</p></td>
<td><p> </p></td>
<td><p>Densità media di perdita pacchetti durante burst di perdite durante la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>BurstDuration</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Durata media della perdita di pacchetti durante burst di perdite durante la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BurstGapDensity</strong></p></td>
<td><p>decimal(9,4)</p></td>
<td><p> </p></td>
<td><p>Densità media della perdita di pacchetti durante le pause tra burst della perdita di pacchetti.</p></td>
</tr>
<tr class="even">
<td><p><strong>BurstGapDuration</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Durata media delle pause tra burst della perdita di pacchetti.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PacketUtilization</strong></p></td>
<td><p>Int</p></td>
<td><p> </p></td>
<td><p>Numero di pacchetti per il flusso audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEst</strong></p></td>
<td><p>Int</p></td>
<td><p> </p></td>
<td><p>Stime di larghezza di banda per il flusso audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DegradationAvg</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Degradazione MOS di rete per l'intera chiamata. L'intervallo è compreso tra 0,0 e 5,0. Questa metrica indica la quantità di MOS di rete ridotta a causa della dispersione e della perdita di pacchetti. Per un livello di qualità accettabile, questo valore deve essere minore di 0,5.</p></td>
</tr>
<tr class="even">
<td><p><strong>DegradationMax</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Degradazione MOS di rete massima durante la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DegradationJitterAvg</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Degradazione MOS di rete causata dall'instabilità.</p></td>
</tr>
<tr class="even">
<td><p><strong>DegradationPacketLossAvg</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Degradazione MOS di rete causata dalla perdita di pacchetti.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioPayloadDescription</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Il codec audio utilizzato per la chiamata, con riferimento dalla tabella PayloadDescription.</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioSampleRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Frequenza di campionamento per il flusso audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RoundTrip</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Tempo di round trip dalle statistiche RTCP. Per un livello di qualità accettabile, questo valore deve essere minore di 100 ms.</p></td>
</tr>
<tr class="even">
<td><p><strong>RoundTripMax</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Tempo di round trip massimo per il flusso audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>OverallAvgNetworkMOS</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>MOS di rete a banda larga medio per la chiamata. Questa metrica dipende dalla perdita di pacchetti, dalla dispersione e dal codec utilizzato. L'intervallo valido è compreso tra 1,0 e 5,0.</p></td>
</tr>
<tr class="even">
<td><p><strong>OverallMinNetworkMOS</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>MOS di rete a banda larga minimo per la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendListenMOS</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Punteggio Listening MOS a banda larga previsto medio per l'audio inviato, inclusi il livello parlato, il livello rumore e le caratteristiche del dispositivo di acquisizione.</p></td>
</tr>
<tr class="even">
<td><p><strong>SendListenMOSMin</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Valore SendListenMOS minimo per la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvListenMOS</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Punteggio Listening MOS a banda larga previsto medio per l'audio ricevuto dalla rete, inclusi il livello parlato, il livello rumore, il codec, le condizioni della rete e le caratteristiche del dispositivo di acquisizione.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvListenMOSMin</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Valore RecvListenMOS minimo per la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioFECUsed</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Flag che indica se per la chiamata è stata usata la correzione FEC audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>RatioConcealedSamplesAvg</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Rapporto medio tra i campioni nascosti risultanti dalla correzione audio e i campioni tipici.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RatioStretchedSamplesAvg</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Rapporto medio tra i campioni estesi risultanti dalla correzione audio e i campioni tipici.</p></td>
</tr>
<tr class="even">
<td><p><strong>RatioCompressedSamplesAvg</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Rapporto medio tra i campioni compressi risultanti dalla correzione audio e i campioni tipici.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Dati del flusso ricevuti sul lato del ricevitore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Outbound</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Dati del flusso ricevuti sul lato del mittente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SenderIsCallerPAI</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 indica che la direzione del flusso va dal chiamante al destinatario della chiamata.</p>
<p>0 indica che la direzione del flusso va dal destinatario della chiamata al chiamante.</p></td>
</tr>
<tr class="even">
<td><p><strong>JitterInterArrivalSD</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Deviazione standard per instabilità ore di arrivo.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConcealRatioMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Rapporto massimo dei pacchetti nascosti dall'utilità di ripristino.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConcealRatioSD</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Deviazione standard per il rapporto dei pacchetti nascosti dall'utilità di ripristino.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HealerPacketDropRatio</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Rapporto dei pacchetti non elaborati dall'utilità di ripristino rispetto al numero totale dei pacchetti ricevuti.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>HealerFECPacketUsedRatio</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Rapporto dei pacchetti di correzione degli errori di inoltro usati rispetto al numero totale dei pacchetti ricevuti.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCompressedSamples</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Numero massimo di pacchetti audio compressi dall'utilità di ripristino.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>LossCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Indica la percentuale di tempo trascorso dalla chiamata in uno stato di perdita a causa di una congestione.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelayCongestionPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Indica la percentuale di tempo della chiamata in cui si è verificata la congestione a causa dell'arrivo in ritardo dei pacchetti di rete.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>ContentionDetectedPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Indica la percentuale di tempo impiegato dalla chiamata per ottenere le risorse di rete.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstMin</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Quantità minima della stima della larghezza di banda misurata durante la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstMax</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Quantità massima della stima della larghezza di banda misurata durante la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BandwidthEstStdDev</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Deviazione standard della stima della larghezza di banda misurata durante la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>BandwidthEstAvge</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Quantità media della stima della larghezza di banda misurata durante la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayTotal</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Quantità complessiva di latenza unidirezionale. La latenza unidirezionale relativa misura il ritardo tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayAverage</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Quantità complessiva di latenza unidirezionale. La latenza unidirezionale relativa misura il ritardo tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayMax</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Quantità massima di latenza unidirezionale. La latenza unidirezionale relativa misura il ritardo tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Occorrenze burst unidirezionali totali. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayBurstDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Densità burst unidirezionale totale. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayBurstDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Durata burst unidirezionale totale. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayGapOccurrences</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Occorrenze gap unidirezionali totali. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RelativeOneWayGapDensity</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Densità gap unidirezionale totale. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. I gap indicano i ritardi tra questi burst. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RelativeOneWayGapDuration</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Durata gap unidirezionale totale. In una trasmissione di tipo burst il flusso di dati non è prevedibile, diversamente dal flusso stabile. I gap indicano i ritardi tra questi burst. Questa metrica misura il flusso di dati tra il client e il server.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>DecodeStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Percentuale della chiamata decodificata come stereo.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AecRenderStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Percentuale della chiamata resa come stereo dall'utilità di annullamento dell'eco acustico.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioPostFECPLR</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Frequenza di perdita dei pacchetti dopo l'applicazione della correzione degli errori di inoltro.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EncodeStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Percentuale della chiamata codificata come stereo.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>AecCaptureStereoPercent</strong></p></td>
<td><p>float</p></td>
<td><p></p></td>
<td><p>Percentuale della chiamata acquisita come stereo dall'utilità di annullamento dell'eco acustico.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

