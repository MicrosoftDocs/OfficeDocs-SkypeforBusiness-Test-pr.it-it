---
title: Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013
TOCTitle: Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013
ms:assetid: 83e83b16-0f0e-4d87-901a-0faa4618cdc2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688118(v=OCS.15)
ms:contentKeyID: 49887634
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Una parte importante della pianificazione di rete consiste nell'assicurarsi che la rete sia in grado di gestire il traffico multimediale generato da Lync Server. Questa sezione fornisce supporto alla pianificazione per il traffico multimediale.

## Utilizzo della rete per il traffico multimediale

L'utilizzo della larghezza di banda per il traffico multimediale può essere difficile da calcolare per la quantità di variabili diverse, ad esempio l'utilizzo di codec, la risoluzione e i livelli di attività. L'utilizzo della larghezza di banda dipende dal codec utilizzato e dall'attività del flusso, entrambi variabili a seconda degli scenari. Nella tabella seguente vengono elencati i codec audio utilizzati comunemente in scenari di Lync Server 2013.

### Larghezza di banda del codec audio

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec audio</th>
<th>Scenari</th>
<th>Velocità in bit di payload audio (Kbps)</th>
<th>Larghezza di banda solo per payload audio e intestazione (Kbps)</th>
<th>Larghezza di banda per payload audio, intestazione IP, UDP, RTP e SRTP (Kbps)</th>
<th>Larghezza di banda per payload audio, intestazione IP, UDP, RTP, SRTP e correzione degli errori di inoltro (FEC) (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Banda larga RTAudio</p></td>
<td><p>Peer-to-peer</p></td>
<td><p>29,0</p></td>
<td><p>45,0</p></td>
<td><p>57,0</p></td>
<td><p>86,0</p></td>
</tr>
<tr class="even">
<td><p>Banda stretta RTAudio</p></td>
<td><p>Peer-to-peer, PSTN</p></td>
<td><p>11,8</p></td>
<td><p>27,8</p></td>
<td><p>39,8</p></td>
<td><p>51,6</p></td>
</tr>
<tr class="odd">
<td><p>G.722</p></td>
<td><p>Servizi di conferenza</p></td>
<td><p>64,0</p></td>
<td><p>80,0</p></td>
<td><p>95,6</p></td>
<td><p>159,6</p></td>
</tr>
<tr class="even">
<td><p>G.722 Stereo</p></td>
<td><p>Peer-to-peer, Servizi di conferenza</p></td>
<td><p>128,0</p></td>
<td><p>144,0</p></td>
<td><p>159,6</p></td>
<td><p>223,6</p></td>
</tr>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>PSTN</p></td>
<td><p>64,0</p></td>
<td><p>80,0</p></td>
<td><p>92,0</p></td>
<td><p>156,0</p></td>
</tr>
<tr class="even">
<td><p>Siren</p></td>
<td><p>Servizi di conferenza</p></td>
<td><p>16,0</p></td>
<td><p>32,0</p></td>
<td><p>47,6</p></td>
<td><p>63,6</p></td>
</tr>
</tbody>
</table>


I numeri relativi alla larghezza di banda nella tabella precedente sono basati sulla pacchettizzazione a 20 ms (50 pacchetti al secondo) e per Siren e G.722 includono l'overhead aggiuntivo del protocollo SRTP (Secure Real Time Transport Protocol) degli scenari di conferenza e presuppongono che il flusso sia attivo al 100%. La correzione degli errori di inoltro (FEC, Forward Error Correction) viene utilizzata dinamicamente in caso di perdita di pacchetti sul collegamento per preservare la qualità del flusso audio.

La versione stereo del codec G.722 è utilizzata dai sistemi basati su Lync Room System, che abilita l'acquisizione in stereo dal microfono per consentire ai partecipanti di distinguere meglio i relatori nella sala riunioni.

Per il video, il codec predefinito è lo standard H.264/MPEG-4 Part 10 Advanced Video Coding insieme alle estensioni di codifica video scalabile per la scalabilità provvisoria. Per mantenere l'interoperabilità con i client Lync 2010 o Office Communicator 2007 R2, il codec RTVideo viene utilizzato ancora per le chiamate peer-to-peer tra i client Lync 2013 e legacy. Nelle sessioni di conferenza con entrambi i client Lync 2013 e legacy, l'endpoint di Lync 2013 può codificare il video utilizzando entrambi i codec video, e inviare il flusso H.264 al client Lync 2013 e il flusso di bit RTVideo ai client Lync 2010 o Office Communicator 2007 R2.

I requisiti di larghezza di banda dipendono da aspetti quali la risoluzione, la qualità e la frequenza frame. Per ogni risoluzione, sono disponibili due velocità in bit interessanti:

  - **Velocità in bit massima di payload**   Si tratta delle velocità in bit che verrà utilizzata da un endpoint di Lync 2013 per la risoluzione alla massima frequenza frame supportata per questa risoluzione. Questo valore è interessante perché consente di ottenere video con i massimi livelli di qualità e frequenza frame.

  - **Velocità in bit minima di payload**   La velocità in bit che verrà utilizzata da un endpoint di Lync 2013 per passare alla risoluzione inferiore successiva. Per garantire una data risoluzione, la velocità in bit di payload non deve scendere sotto questo valore per ottenere quella risoluzione. Questo valore è interessante perché consente di identificare il valore minimo possibile nei casi in cui la velocità in bit massima non è disponibile o praticabile. Per alcuni utenti, una risoluzione così bassa può essere considerata accettabile per l'esperienza, per cui valutare con attenzione queste velocità di payload minime. Nelle scene video in cui il movimento dell'utente è minimo o nullo, la velocità in bit potrebbe scendere, temporaneamente, sotto la velocità minima.

Lync 2013 supporta molte altre risoluzioni. Ciò consente di regolare in maniera migliore le diverse larghezze di banda della rete, e di ricevere le funzionalità del client. Inoltre, le proporzioni predefinite per Lync 2013 sono state modificate a 16:9. Le proporzioni 4:3 sono ancora supportate per le webcam che non consentono l'acquisizione in 16:9.

### Larghezza di banda della risoluzione video

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec video</th>
<th>Risoluzione e proporzioni</th>
<th>Velocità in bit massima di payload (Kbps)</th>
<th>Velocità in bit minima di payload (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>320x180 (16:9)</p>
<p>212x160 (4:3)</p></td>
<td><p>250</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>H.264/RTVideo</p></td>
<td><p>424x240 (16:9))</p>
<p>320x240 (4:3</p></td>
<td><p>350</p></td>
<td><p>100</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>480x270 (16:9)</p>
<p>424x320 (4:3)</p></td>
<td><p>450</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>H.264/RTVideo</p></td>
<td><p>640x360 (16:9)</p>
<p>640x480 (4:3)</p></td>
<td><p>800</p></td>
<td><p>300</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>848x480 (16:9)</p></td>
<td><p>1500</p></td>
<td><p>400</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>960x540 (16:9)</p></td>
<td><p>2000</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>H.264/RTVideo</p></td>
<td><p>1280x720 (16:9)</p></td>
<td><p>2500</p></td>
<td><p>700</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>1920x1080 (16:9)</p></td>
<td><p>4000</p></td>
<td><p>1500</p></td>
</tr>
<tr class="odd">
<td><p>H.264/RTVideo</p></td>
<td><p>960x144 (20:3)</p></td>
<td><p>500</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>H.264</p></td>
<td><p>1280x192 (20:3)</p></td>
<td><p>1000</p></td>
<td><p>250</p></td>
</tr>
<tr class="odd">
<td><p>H.264</p></td>
<td><p>1920x288 (20:3)</p></td>
<td><p>2000</p></td>
<td><p>500</p></td>
</tr>
</tbody>
</table>


La correzione FEC video è inclusa nella velocità in bit di payload video quando viene utilizzata, quindi non sono disponibili valori separati con e senza FEC video.

Gli endpoint non inviano flussi continui di pacchetti audio o video. A seconda dello scenario, esistono livelli diversi di attività di flusso che indicano la frequenza dell'invio di pacchetti per un flusso. L'attività di un flusso dipende dal contenuto multimediale e dallo scenario e non dal codec utilizzato. In uno scenario peer-to-peer:

  - Gli endpoint inviano flussi audio solo quando l'utente parla.

  - Entrambi i partecipanti ricevono flussi audio.

  - Se si utilizzano funzionalità video, entrambi gli endpoint inviano e ricevono flussi video durante l'intera chiamata.

  - Nelle scene video con movimento minimo o nullo, la velocità in bit potrebbe raggiungere picchi molto bassi, poiché il codec video non codifica le regioni del video in cui non avvengono cambiamenti.

In uno scenario di conferenza:

  - Gli endpoint inviano flussi audio solo quando l'utente parla.

  - Tutti i partecipanti ricevono flussi audio.

  - Se è utilizzato il video, tutti i partecipanti possono ricevere fino a cinque flussi video, e un flusso video panoramico (ad esempio, con proporzioni 20:3). Per impostazione predefinita, i cinque flussi video di ricezione si basano sulla cronologia dell'oratore attivo, ma gli utenti possono selezionare manualmente i partecipanti dai quali desiderano ricevere il flusso video.

  - Ciascun partecipante che attiva il flusso video di invio dell'utente, invierà uno o più flussi video. Lync 2013 consente di inviare fino a cinque flussi video al fine di ottimizzare la qualità video per tutti i client di ricezione. Il numero effettivo di flussi video inviati è determinato dal mittente sulla base della capacità del CPU, della larghezza di banda disponibile, e del numero di client in ricezione che richiedono un determinato flusso video. Il caso più comune è quello in cui un flusso video H.264 e un flusso video RTVideo sono inviati se un client legacy partecipa alla conferenza. Un altro scenario comune è quello in cui diversi flussi video H.264 (ad esempio, con risoluzioni video diverse) vengono inviati al fine di soddisfare diverse richieste.

Oltre che per il traffico RTP (Real-time Transport Protocol) per il contenuto multimediale audio e video, la larghezza di banda è necessaria anche per RTCP (Real-time Transport Control Protocol), un protocollo utilizzato per la segnalazione di statistiche e per il controllo statistiche e per il controllo fori banda del flusso RTP. Per la pianificazione, utilizzare i numeri relativi alla larghezza di banda riportati nella tabella seguente per il traffico RTCP. Questi valori rappresentano la larghezza di banda massima utilizzata per RTCP e sono diversi tra flussi audio e video a causa delle differenze nei dati di controllo.

### Larghezza di banda per RTCP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento multimediale</th>
<th>Larghezza di banda massima per RTCP (Kbps)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Audio</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>Video (solo H.264 o RTVideo inviati/ricevuti)</p></td>
<td><p>10</p></td>
</tr>
<tr class="odd">
<td><p>Video (H.264 e RTVideo inviati/ricevuti)</p></td>
<td><p>15</p></td>
</tr>
</tbody>
</table>


Per la pianificazione della capacità, sono importanti le due larghezze di banda seguenti:

  - **Larghezza di banda massima senza FEC**   La larghezza di banda massima che verrà utilizzata da un flusso, includendo la tipica attività del flusso e il tipico codec utilizzato nello scenario senza FEC. Si tratta della larghezza di banda utilizzata quando l'attività del flusso corrisponde al 100% e non si verificano perdite di pacchetti che attivano l'utilizzo di FEC.  Questo valore è interessante per calcolare la quantità di larghezza di banda da allocare per consentire l'utilizzo del codec in un determinato scenario. 

  - **Larghezza di banda massima con FEC**   La larghezza di banda massima utilizzata da un flusso, includendo la tipica attività del flusso e il tipico codec utilizzato nello scenario con FEC. Si tratta della larghezza di banda utilizzata quando l'attività del flusso corrisponde al 100% e si verifica una perdita di pacchetti che attiva l'utilizzo di FEC per migliorare la qualità. Questo valore è interessante per calcolare la quantità di larghezza di banda da allocare per consentire l'utilizzo del codec in un determinato scenario e l'utilizzo di FEC per preservare la qualità in condizioni di perdita di pacchetti. 

Nella tabella seguente viene riportato anche un altro valore di larghezza di banda, la **larghezza di banda tipica**, ovvero quella utilizzata in media da un flusso, includendo la tipica attività del flusso e il tipico codec utilizzato nello scenario. Questo valore può essere utilizzato per calcolare la quantità approssimativa di larghezza di banda utilizzata in un dato momento dal traffico multimediale, ma non è consigliabile utilizzarlo per la pianificazione della capacità, perché le singole chiamate supereranno questo valore quando il livello di attività è maggiore della media. La larghezza di banda tipica del flusso video nelle tabelle seguenti si basa su diverse risoluzioni video osservate nei dati misurati presso i clienti. Ad esempio, nelle sessioni peer-to-peer la maggior parte dei clienti utilizzerebbe una finestra video predefinita, mentre alcuni utenti aumenterebbero o massimizzerebbero l'applicazione di Lync per consentire risoluzioni video più elevate.

Nella tabella seguente vengono riportati questi tre valori di larghezza di banda per i vari scenari possibili.

### Pianificazione della capacità audio/video per sessioni peer-to-peer

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento multimediale</th>
<th>Codec</th>
<th>Larghezza di banda tipica del flusso (Kbps)</th>
<th>Larghezza di banda massima del flusso senza FEC</th>
<th>Larghezza di banda massima del flusso con FEC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Audio</p></td>
<td><p>Banda larga RTAudio</p></td>
<td><p>39,8</p></td>
<td><p>62</p></td>
<td><p>91</p></td>
</tr>
<tr class="even">
<td><p>Audio</p></td>
<td><p>Banda stretta RTAudio</p></td>
<td><p>29,3</p></td>
<td><p>44,8</p></td>
<td><p>56,6</p></td>
</tr>
<tr class="odd">
<td><p>Video principale quando si chiamano gli endpoint di Lync 2013</p></td>
<td><p>H.264</p></td>
<td><p>460</p></td>
<td><p>4010 (per una risoluzione massima di 1920x1080)</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Video principale quando si chiamano gli endpoint di Lync 2010 o di Office Communicator 2007 R2</p></td>
<td><p>RTVideo</p></td>
<td><p>460</p></td>
<td><p>2510 (per una risoluzione massima di 1280x720)</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Video panoramico quando si chiamano gli endpoint di Lync 2013</p></td>
<td><p>H.264</p></td>
<td><p>190</p></td>
<td><p>2010 (per una risoluzione massima di 1920x288)</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Video panoramico quando si chiamano gli endpoint di Lync 2010 o Office Communicator 2007 R2 endpoints</p></td>
<td><p>RTVideo</p></td>
<td><p>190</p></td>
<td><p>510 (per una risoluzione massima di 960x144)</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


### Pianificazione della capacità audio/video per conferenze

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento multimediale</th>
<th>Codec tipico</th>
<th>Larghezza di banda tipica del flusso (Kbps)</th>
<th>Larghezza di banda massima del flusso senza FEC</th>
<th>Larghezza di banda massima del flusso con FEC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Audio</p></td>
<td><p>G.722</p></td>
<td><p>46.1</p></td>
<td><p>100,6</p></td>
<td><p>164,6</p></td>
</tr>
<tr class="even">
<td><p>Audio</p></td>
<td><p>Siren</p></td>
<td><p>25,5</p></td>
<td><p>52,6</p></td>
<td><p>68,6</p></td>
</tr>
<tr class="odd">
<td><p>Ricezione video principale</p></td>
<td><p>H.264 e/o RTVideo</p></td>
<td><p>260</p></td>
<td><p>8015</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Invio video principale</p></td>
<td><p>H.264 e/o RTVideo</p></td>
<td><p>270</p></td>
<td><p>8015</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Ricezione video panoramico</p></td>
<td><p>H.264 e/o RTVideo</p></td>
<td><p>190</p></td>
<td><p>2010 (per una risoluzione massima di 1920x288)</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Invio video panoramico</p></td>
<td><p>H.264 e/o RTVideo</p></td>
<td><p>190</p></td>
<td><p>2515 (per l'invio di flusso di bit utilizzando risoluzioni/codec multipli</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


Per il video principale, la larghezza di banda massima del flusso è rappresentata dalla larghezza di banda aggregata di tutti i flussi video ricevuti e tutti i flussi video inviati, rispettivamente. Anche con flussi video multipli, la larghezza di banda video tipica è inferiore rispetto a quella dello scenario peer-to-peer, poiché molte conferenze video utilizzano una condivisione di contenuto che porta a finestre video più piccole, e pertanto a risoluzioni video inferiori. La larghezza di banda di payload massima supportata è pari a 8000 Kbps per entrambi i flussi di invio e ricezione che sarebbero utilizzati, ad esempio, nel caso di due flussi video da 1920x1080p in ingresso.

La larghezza di banda tipica per il flusso del video panoramico si basa sui dispositivi attualmente disponibili, in grado di eseguire video panoramico fino a 960x144. Quando divengono disponibili dispositivi con video panoramico da 1920x288, la larghezza di banda tipica dovrebbe aumentare.

### Pianificazione della capacità audio per PSTN

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento multimediale</th>
<th>Codec tipico</th>
<th>Larghezza di banda tipica del flusso (Kbps)</th>
<th>Larghezza di banda massima del flusso senza FEC</th>
<th>Larghezza di banda massima del flusso con FEC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Audio</p></td>
<td><p>G.711</p></td>
<td><p>64,8</p></td>
<td><p>97</p></td>
<td><p>161</p></td>
</tr>
<tr class="even">
<td><p>Audio</p></td>
<td><p>Banda stretta RTAudio</p></td>
<td><p>30,9</p></td>
<td><p>44,8</p></td>
<td><p>56,6</p></td>
</tr>
</tbody>
</table>


I numeri relativi alla larghezza di banda di rete riportati in queste tabelle rappresentano solo il traffico unidirezionale e includono 5 Kbps per l'overhead del traffico RTCP per ogni flusso. Per i video viene utilizzata la velocità in bit massima per il calcolo del flusso massimo.

