---
title: 'Lync Server 2013: Tabella AudioClientEvent'
TOCTitle: Tabella AudioClientEvent
ms:assetid: fef73d8f-7261-4e5b-9769-82435b007979
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413086(v=OCS.15)
ms:contentKeyID: 49302585
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella AudioClientEvent in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In ogni record è contenuto un evento client per un endpoint in una chiamata audio. Per una chiamata esistono in genere due record, uno per il chiamante e l'altro per il destinatario della chiamata.


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
<td><p><strong>FromCaller</strong></p></td>
<td><p>bit</p></td>
<td><p>Primaria/o</p></td>
<td><p>0: dati del destinatario della chiamata</p>
<p>1: dati del chiamante</p></td>
</tr>
<tr class="odd">
<td><p><strong>NetworkSendQualityEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento NetworkSendQuality ha generato l'avviso di stato non valido.</p>
<p>I problemi di qualità di rete in termini di instabilità o perdita di pacchetti sono gravi e incidono sulla qualità dell'audio inviato.</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkReceiveQualityEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento ReceiveSendQuality ha generato l'avviso di stato non valido.</p>
<p>I problemi di qualità di rete in termini di instabilità o perdita di pacchetti sono gravi e incidono sulla qualità dell'audio ricevuto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NetworkDelayEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento Delay ha generato l'avviso di stato non valido. La latenza di rete è grave e incide sull'esperienza dell'utente impedendo la comunicazione interattiva.</p></td>
</tr>
<tr class="even">
<td><p><strong>NetworkBandwidthLowEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento LowBandwidth ha generato l'avviso di stato non valido. La larghezza di banda disponibile è insufficiente per offrire un'esperienza vocale accettabile.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CPUInsufficientEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento CPU insufficiente ha generato l'avviso di stato non valido. I cicli CPU sono insufficienti per l'elaborazione delle modalità correnti e delle applicazioni in uso. Ciò causa distorsioni con il canale audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceHalfDuplexAECEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceHalfDuplexAEC ha generato l'avviso di stato non valido. Per evitare l'eco, il sistema è entrato in modalità half-duplex.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceRenderNotFunctioningEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceRenderNotFunctioning ha generato l'avviso di stato non valido. Il dispositivo di rendering attualmente utilizzato per la sessione non funziona correttamente. Ciò può causare problemi di audio unidirezionale.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceCaptureNotFunctioningEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceCaptureNotFunctioning ha generato l'avviso di stato non valido. Il dispositivo di acquisizione attualmente utilizzato per la sessione non funziona correttamente. Ciò può causare problemi di audio unidirezionale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceGlitchesEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceGlitches ha generato l'avviso di stato non valido. Sono presenti gravi problemi di rendering dell'audio che causano distorsioni. Questi problemi possono essere causati da problemi di driver, DPC (Deferred Procedure Call) storm (driver) ed elevato uso della CPU.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceLowSNREventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceLowSNR ha generato l'avviso di stato non valido. La qualità di acquisizione è molto bassa, l'audio è molto disturbato o l'utente parla troppo lontano dal microfono con conseguenti distorsioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceLowSpeechLevelEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceLowSpeechLevel ha generato l'avviso di stato non valido. Il livello parlato dell'utente è troppo basso e il sistema non può aumentarlo ulteriormente. Ciò può causare distorsioni o essere percepito come audio unidirezionale.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceClippingEventRatio</strong></p></td>
<td><p>Decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceClipping ha generato l'avviso di stato non valido.</p>
<p>Quando si esegue il clip del microfono near-end, l'utente far-end sente una distorsione dovuta al clip. È importante evitare il clip del microfono near-end.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceEchoEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceEchoEvent ha generato l'avviso di stato non valido. Il dispositivo o l'impostazione causa eco oltre il livello compensabile dal sistema.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceNearEndToEchoRatioEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceNearEndToEchoRatio ha generato l'avviso di stato non valido. Il livello parlato dell'utente è troppo basso rispetto all'eco acquisito con impatto sull'esperienza dell'utente poiché limita la semplicità di interruzione di un utente. Ridurre il volume degli altoparlanti, spostare il microfono più vicino al parlante.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceMultipleEndpointsEventCount</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Numero di volte durante la sessione in cui l'evento DeviceMultipleEndpoints ha generato l'avviso di stato non valido. Sono stati rilevati più endpoint audio nella stessa sessione e il sistema ha effettuato la compensazione riducendo il volume di rendering.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceHowlingEventCount</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Numero di volte durante la sessione in cui l'evento DeviceHowlingEvent ha generato l'avviso di stato non valido. Rilevato loop di feedback audio (causato da più endpoint che condividono il percorso audio).</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceRenderZeroVolumeEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceRenderZeroVolume ha generato l'avviso di stato non valido. Il dispositivo di rendering è stato impostato su volume zero.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceRenderMuteEventRatio</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Percentuale della sessione in cui l'evento DeviceRenderMute ha generato l'avviso di stato non valido. Il dispositivo di rendering è stato disattivato.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

