---
title: 'Lync Server 2013: requisiti video del client Lync'
TOCTitle: Requisiti video del client Lync
ms:assetid: 8f68f4c2-3194-487c-bd2f-fbe71ba8ad70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688132(v=OCS.15)
ms:contentKeyID: 49887653
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti video del client Lync per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione viene descritto il supporto hardware video per le videochiamate di Lync 2013 nonché le modalità per determinare la qualità video prevista per le diverse configurazioni di computer, tablet e dispositivi mobili.

## Funzionalità e requisiti video per tablet e computer desktop Windows

In Lync 2013 è stata introdotta l'accelerazione hardware per la codifica e la decodifica video in base allo standard H.264/MPEG-4 Part 10 Advanced Video Coding. Questa caratteristica consente ai computer con velocità di clock della CPU inferiori di codificare e decodificare video a risoluzioni più elevate. I requisiti hardware video variano a seconda della configurazione del computer e alla risoluzione video desiderata.

## Requisiti hardware video


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Decodifica H.264 con accelerazione hardware mediante DirectX Video Acceleration (DXVA)</p></td>
<td><ul>
<li><p>La scheda video deve supportare DirectX 9.0 ed esporre la modalità di decodifica DXVA2_ModeH264_VLD_NoFGT.</p></li>
<li><p>Deve essere installato il driver più recente della scheda video.</p></li>
</ul>

> [!NOTE]
> Per dettagli sulle modalità di decodifica, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=268530">http://go.microsoft.com/fwlink/p/?LinkId=268530</A>.


</td>
</tr>
<tr class="even">
<td><p>Codifica H.264 con accelerazione hardware: requisiti del chipset</p></td>
<td><p>Sono supportate le soluzioni di codifica con accelerazione hardware Intel seguenti:</p>
<ul>
<li><p>Chipset Intel HD Graphics 2000, 2500, 3000 e 4000 di seconda e terza generazione (o versioni successive) con codificatori video hardware integrati. È richiesta l'installazione del driver Intel HD Graphics 15.28.9.2884 o del driver più recente che include le funzionalità seguenti:</p>
<ul>
<li><p>Driver video 9.17.10.2884 o più recente</p></li>
<li><p>HMFT (Hardware Media Foundation Transform) versione 3.12.10.31 o più recente</p></li>
</ul></li>
</ul>
<p>Sono supportate le soluzioni di codifica con accelerazione hardware AMD seguenti (richiesti gli aggiornamenti cumulativi 1 per Lync Server 2013):</p>
<ul>
<li><p>AMD Video Codec Engine, disponibile in diverse schede video non integrate e in unità di elaborazione accelerate integrate dei processori accelerati AMD A-Series. È necessario installare il driver AMD Video Codec Engine 9.12.0.0 o versione successiva.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Codifica H.264 con accelerazione hardware: requisiti fotocamera</p></td>
<td><p>Fotocamere video USB con codificatore H.264 integrato conforme alla specifica USB Video Class (UVC) versione 1.5.</p>


> [!NOTE]
> Lync 2013 supporta fotocamere UVC 1.5 con Windows 8 o Windows 8.1, il che include il supporto per UVC 1.5. Poiché Windows 7 non include il supporto per UVC 1.5, Lync 2013 tratta le fotocamere UVC 1.5 come fotocamere normali senza supporto per la codifica hardware.


</td>
</tr>
<tr class="even">
<td><p>Decodifica H.264 con accelerazione hardware mediante DirectX Video Acceleration (DXVA)</p></td>
<td><ul>
<li><p>La scheda video deve supportare DirectX 9.0 ed esporre la modalità di decodifica DXVA2_ModeH264_VLD_NoFGT.</p></li>
<li><p>Deve essere installato il driver più recente della scheda video.</p></li>
</ul>

> [!NOTE]
> Per dettagli sulle modalità di decodifica, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=268530">http://go.microsoft.com/fwlink/p/?LinkId=268530</A>.


</td>
</tr>
<tr class="odd">
<td><p>Codifica H.264 con accelerazione hardware: requisiti del chipset</p></td>
<td><p>Sono supportate le soluzioni di codifica con accelerazione hardware Intel seguenti:</p>
<ul>
<li><p>Chipset Intel HD Graphics 2000, 2500, 3000 e 4000 di seconda e terza generazione (o versioni successive) con codificatori video hardware integrati. È richiesta l'installazione del driver Intel HD Graphics 15.28.9.2884 o del driver più recente che include le funzionalità seguenti:</p>
<ul>
<li><p>Driver video 9.17.10.2884 o più recente</p></li>
<li><p>HMFT (Hardware Media Foundation Transform) versione 3.12.10.31 o più recente</p></li>
</ul></li>
</ul>
<p>Sono supportate le soluzioni di codifica con accelerazione hardware AMD seguenti (richiesti gli aggiornamenti cumulativi 1 per Lync Server 2013):</p>
<ul>
<li><p>AMD Video Codec Engine, disponibile in diverse schede video non integrate e in unità di elaborazione accelerate integrate dei processori accelerati AMD A-Series. È necessario installare il driver AMD Video Codec Engine 9.12.0.0 o versione successiva.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Codifica H.264 con accelerazione hardware: requisiti fotocamera</p></td>
<td><p>Fotocamere video USB con codificatore H.264 integrato conforme alla specifica USB Video Class (UVC) versione 1.5.</p>


> [!NOTE]
> Lync 2013 supporta fotocamere UVC 1.5 con Windows 8 o Windows 8.1, il che include il supporto per UVC 1.5. Poiché Windows 7 non include il supporto per UVC 1.5, Lync 2013 tratta le fotocamere UVC 1.5 come fotocamere normali senza supporto per la codifica hardware.


</td>
</tr>
</tbody>
</table>


## Individuazione delle funzionalità di codifica e decodifica video H.264

In generale, esistono quattro fattori principali che determinano la capacità di codifica e decodifica massima di una particolare configurazione di computer:

  - Supporto per decodifica con accelerazione hardware mediante DXVA

  - Supporto per la codifica con accelerazione hardware

  - Numero di core fisici

  - Indice prestazioni Windows

Lo strumento Valutazione sistema Windows (WinSAT) determina l'Indice prestazioni Windows. Quando si esegue lo strumento Valutazione sistema Windows, viene generato un documento XML Formal.Assessment nella directory %windir%\\Performance\\WinSAT\\DataStore del computer. Questo file XML contiene i due punteggi indicati di seguito di particolare importanza per determinare le funzionalità di codifica e decodifica:

  - VideoEncodeScore indica le capacità di codifica video basata su software del computer.

  - Il valore GraphicsScore indica la capacità di codifica con accelerazione hardware del computer.

Nelle tre tabelle seguenti sono indicate le capacità massime di codifica e decodifica per diversi tipi di PC a seconda dell'accelerazione hardware supportata. Per risoluzioni pari a 640x360 e superiori, la massima frequenza dei fotogrammi supportata è pari a 30 fotogrammi al secondo (fps). Per risoluzioni inferiori a 640x360, la massima velocità dei fotogrammi supportata è pari a 15 fps.

### Computer senza DXVA e senza codificatore con accelerazione hardware

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Risoluzione codificatore</th>
<th>Risoluzione decodificatore</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>424x240</p></td>
<td><p>424x240 (640x360 a 15 fps solo per scenari di ricezione)</p></td>
<td><p>1 core e VideoEncodeScore ≥ 4,0</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>640x360</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1280x720</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1280x720</p></td>
<td><p>4 core e VideoEncodeScore ≥ 7,3</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 7,3</p></td>
</tr>
<tr class="odd">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>424x240</p></td>
<td><p>424x240 (640x360 a 15 fps solo per scenari di ricezione)</p></td>
<td><p>1 core e VideoEncodeScore ≥ 4,0</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>640x360</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1280x720</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1280x720</p></td>
<td><p>4 core e VideoEncodeScore ≥ 7,3</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 7,3</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


### Computer con DXVA ma senza codificatore con accelerazione hardware

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Risoluzione codificatore</th>
<th>Risoluzione decodificatore</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>424x240</p></td>
<td><p>1920x1080</p></td>
<td><p>1 core e VideoEncodeScore ≥ 3,0</p></td>
</tr>
<tr class="even">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="odd">
<td><p>960x540</p></td>
<td><p>1920x1080</p></td>
<td><p>2 core e VideoEncodeScore ≥ 6,0</p></td>
</tr>
<tr class="even">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 6,7</p></td>
</tr>
<tr class="odd">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 8,2</p></td>
</tr>
<tr class="even">
<td><p>424x240</p></td>
<td><p>1920x1080</p></td>
<td><p>1 core e VideoEncodeScore ≥ 3,0</p></td>
</tr>
<tr class="odd">
<td><p>640x360</p></td>
<td><p>1920x1080</p></td>
<td><p>2 core e VideoEncodeScore ≥ 4,5</p></td>
</tr>
<tr class="even">
<td><p>960x540</p></td>
<td><p>1920x1080</p></td>
<td><p>2 core e VideoEncodeScore ≥ 6,0</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 6,7</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>4 core e VideoEncodeScore ≥ 8,2</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Il punteggio dello strumento Valutazione sistema Windows su Windows 7 è limitato a un massimo di 7,9, pertanto la capacità di codifica per un computer senza codificatore con accelerazione hardware può essere raggiunta solo su Windows 8 o Windows 8.1, in cui il punteggio dello strumento Valutazione sistema Windows è 9,9.



### Computer con DXVA e con codificatore con accelerazione hardware Intel HD Graphics

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Risoluzione codificatore</th>
<th>Risoluzione decodificatore</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>Tutti i driver Intel HD Graphics di seconda e terza generazione</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>Driver Intel HD Graphics di seconda e terza generazione e GraphicsScore ≥ 5,0</p></td>
</tr>
<tr class="odd">
<td><p>1280x720</p></td>
<td><p>1920x1080</p></td>
<td><p>Tutti i driver Intel HD Graphics di seconda e terza generazione</p></td>
</tr>
<tr class="even">
<td><p>1920x1080</p></td>
<td><p>1920x1080</p></td>
<td><p>Driver Intel HD Graphics di seconda e terza generazione e GraphicsScore ≥ 5,0</p></td>
</tr>
</tbody>
</table>


## Funzionalità video dei dispositivi mobili

Nella tabella seguente sono raffigurate le funzionalità video massime dei dispositivi mobili supportati. Per ulteriori informazioni sul supporto per dispositivi mobili, vedere [Pianificazione dei client mobili](lync-server-2013-planning-for-mobile-clients.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Windows Phone</th>
<th>iPhone e iPad</th>
<th>Android</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Risoluzione massima decodifica H.264</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 4: 192x144</p>
<p>iPad e tutti gli altri modelli iPhone supportati: 352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione massima decodifica H.264</p></td>
<td><p>640x480</p></td>
<td><p>iPhone e iPad: 352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="odd">
<td><p>Risoluzione massima decodifica H.264</p></td>
<td><p>640x480</p></td>
<td><p>iPhone 4: 192x144</p>
<p>iPad e tutti gli altri modelli iPhone supportati: 352x288</p></td>
<td><p>320x2401</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione massima decodifica H.264</p></td>
<td><p>640x480</p></td>
<td><p>iPhone e iPad: 352x288</p></td>
<td><p>320x2401</p></td>
</tr>
</tbody>
</table>


1Per i dispositivi Android con processore Qualcomm Snapdragon S3 o S4 che utilizza un chipset 8x60, sono supportati sia l'invio sia la ricezione a una risoluzione di 640x480.

