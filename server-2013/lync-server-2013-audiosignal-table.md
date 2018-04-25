---
title: 'Lync Server 2013: Tabella AudioSignal'
TOCTitle: Tabella AudioSignal
ms:assetid: 0013c8c6-cdf9-4d70-bc2a-cddd1560f66b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398064(v=OCS.15)
ms:contentKeyID: 49299475
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella AudioSignal in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta la metrica di segnale audio per un endpoint. A ogni chiamata in genere sono associati due record, uno per il chiamante e uno per il destinatario della chiamata.


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
<td><p><strong>SendSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Rappresenta il livello di segnale audio dopo il controllo guadagno analogico. L'unità di misura per questa metrica è dBmo. Per una qualità accettabile, il valore deve essere almeno pari a 30 dBmo. Questa metrica non è riportata da telefoni IP o A/V Conferencing Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Vedere SendSignalLevel.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Rappresenta il livello di rumore audio dopo il controllo guadagno analogico. L'unità di misura per questa metrica è dBmo. Per una qualità accettabile, il valore deve essere inferiore a 35 dBmo. Questa metrica non è riportata da telefoni IP o A/V Conferencing Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Vedere SendNoiseLevel.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoReturn</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Metrica ERLE (Echo Return Loss Enhancement). L'unità di misura per questa metrica è dB. I valori più bassi rappresentano un'eco minore. Questa metrica non è riportata da telefoni IP o A/V Conferencing Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioSpeakerGlitchRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Media dei problemi di rendering dell'altoparlante ogni 5 minuti. Per una buona qualità, il valore deve essere inferiore a 1 ogni 5 minuti. Questa metrica non è riportata da A/V Conferencing Server, Mediation Server o telefoni IP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioMicGlitchRate</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Media dei problemi di acquisizione del microfono ogni 5 minuti. Per una buona qualità, il valore deve essere inferiore a 1 ogni 5 minuti. Questa metrica non è riportata da A/V Conferencing Server, Mediation Server o telefoni IP.</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioTimestampDriftRateMic</strong></p></td>
<td><p>decimal(9,2)</p></td>
<td><p> </p></td>
<td><p>Deviazione del clock del dispositivo microfono rispetto al clock della CPU.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioTimestampDriftRateSpk</strong></p></td>
<td><p>decimal(9,2)</p></td>
<td><p> </p></td>
<td><p>Deviazione del clock del dispositivo altoparlante rispetto al clock della CPU.</p></td>
</tr>
<tr class="even">
<td><p><strong>AudioTimestampErrorMicMs</strong></p></td>
<td><p>decimal(9,2)</p></td>
<td><p> </p></td>
<td><p>Deviazione del clock del dispositivo altoparlante rispetto al clock della CPU.</p>
<p>Media di errore del timestamp, in millisecondi, del flusso di acquisizione del microfono negli ultimi 20 secondi della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AudioTimestampErrorSpkMs</strong></p></td>
<td><p>decimal(9,2)</p></td>
<td><p> </p></td>
<td><p>Media di errore del timestamp, in millisecondi, del flusso di rendering dell'altoparlante negli ultimi 20 secondi della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>VsEntryCauses</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>La commutazione voce è una modalità half-duplex con possibilità di interruzione ridotta. Cause del passaggio alla commutazione vocale:</p>
<p>ENTER_VS_BADTS 0x01</p>
<p>ENTER_VS_ECHO 0x02</p>
<p>ENTER_VS_FORCEORCONVERGENCE 0x04</p>
<p>ENTER_VS_DNLP 0x08</p>
<p>La causa può essere rappresentata da una combinazione di queste singole cause. ENTER_VS_FORCEORCONVERGENCE può essere abilitato solo da regkey a scopo di testing.</p>
<p>Il tipo di dati per questa colonna è stato modificato in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoEventCauses</strong></p></td>
<td><p>tinyint</p></td>
<td><p> </p></td>
<td><p>Cause di un evento eco:</p>
<p>ECHO_EVENT_BAD_TIMESTAMP 0x01</p>
<p>ECHO_EVENT_POSTAEC_ECHO 0x02</p>
<p>ECHO_EVENT_ANLP 0x04</p>
<p>ECHO_EVENT_DNLP 0x08</p>
<p>ECHO_EVENT_MIC_CLIPPING 0x10</p>
<p>ECHO_EVENT_BAD_STATE 0x20</p>
<p>La causa può essere rappresentata da una combinazione di queste singole cause.</p></td>
</tr>
<tr class="even">
<td><p><strong>EchoPercentMicIn</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p> </p></td>
<td><p>Percentuale di tempo in cui viene rilevata l'eco nel flusso di acquisizione del microfono. In genere sono presenti valori ridotti per cuffie o ricevitori e valori più elevati per telefoni vivavoce o altoparlanti autonomi. Per i dispositivi che supportano l'eliminazione dell'eco acustica su scheda, i valori elevati indicano una perdita di eco. Per altri dispositivi, questa metrica non deve utilizzata per valutare la qualità del dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EchoPercentSend</strong></p></td>
<td><p>decimal(5,2)</p></td>
<td><p></p></td>
<td><p>Percentuale di tempo in cui viene rilevata l'eco nel flusso inviato. Un'elevata percentuale di eco nei flussi di invio è un'indicazione della perdita di eco.</p></td>
</tr>
<tr class="even">
<td><p><strong>RxAGCSignalLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Livello di segnale ricevuto nel Mediation Server dal gateway. Si applica solo al Mediation Server. L'unità di misura per questa metrica è dBoV. Per una buona qualità, l'intervallo accettabile deve essere compreso tra [-30 e -18] dBoV.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RxAGCNoiseLevel</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Livello di rumore ricevuto nel Mediation Server dal gateway. Si applica solo al Mediation Server. L'unità di misura per questa metrica è dBoV. Per una buona qualità, il valore deve essere inferiore a -50 dBoV.</p></td>
</tr>
<tr class="even">
<td><p><strong>RxAvgAGCGain</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Controllo guadagno automatico (AGC) sul lato Mediation Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InitialSignalLevelRMS</strong></p></td>
<td><p>float</p></td>
<td><p> </p></td>
<td><p>Radice della media dei quadrati (RMS) del segnale in arrivo fino ai primi 30 secondi della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvSignalLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di segnale ricevuto sul canale 1.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvSignalLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di segnale ricevuto sul canale 2.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RecvNoiseLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di rumore ricevuto sul canale 1.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RecvNoiseLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di rumore ricevuto sul canale 2.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>SendSignalLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di segnale trasmesso sul canale 1.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendSignalLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di segnale trasmesso sul canale 2.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>SendNoiseLevelCh1</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di rumore trasmesso sul canale 1.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SendNoiseLevelCh2</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Livello di rumore trasmesso sul canale 2.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

