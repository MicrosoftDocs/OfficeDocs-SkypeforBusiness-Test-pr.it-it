---
title: 'Lync Server 2013: Rapporto dispositivi'
TOCTitle: Rapporto dispositivi
ms:assetid: f42e4d60-699b-4870-8bb5-13b51bb6eb2b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615049(v=OCS.15)
ms:contentKeyID: 49302474
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto dispositivi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto dispositivi potrebbe anche essere intitolato Rapporto altoparlanti e microfono perché il Rapporto dispositivi recupera le metriche relative alle chiamate (ad esempio, la percentuale di chiamate con qualità insufficiente, l'eco e il tempo commutazione vocale) raggruppate in base ai microfoni e agli altoparlanti utilizzati nella chiamata. In caso di telefoni IP (denominati comunemente "dispositivi"), utilizzare [Rapporto inventario telefoni IP in Lync Server 2013](lync-server-2013-ip-phone-inventory-report.md).

Il Rapporto dispositivi è estremamente utile agli amministratori per stabilire se un tipo specifico di dispositivo riporta volumi elevati di chiamate con qualità insufficiente rispetto ad altri. Questo può influire sulle decisioni da prendere in merito all'acquisto di nuovi dispositivi o alla sostituzione dei dispositivi esistenti.

Per impostazione predefinita, le informazioni visualizzate nel Rapporto dispositivi si basano sul microfono (il dispositivo di acquisizione) e gli altoparlanti/auricolari (il dispositivo di rendering) utilizzati nella chiamata. Ad esempio, si supponga che vari utenti debbano utilizzare il dispositivo di acquisizione e il dispositivo di rendering seguenti:

  - Dispositivo di acquisizione -- Microfono (HD Audio integrato digitale SoundMAX)

  - Dispositivo di rendering -- Auricolare e microtelefono (Microsoft LifeChat LX-3000)

Se gli utenti hanno eseguito un totale di 254 chiamate, nel rapporto verrà visualizzata una voce simile alla seguente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dispositivo di acquisizione</th>
<th>Dispositivo di rendering</th>
<th>Volume chiamata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microfono (HD Audio integrato digitale SoundMAX)</p></td>
<td><p>Auricolare e microtelefono (Microsoft LifeChat LX-3000)</p></td>
<td><p>254</p></td>
</tr>
</tbody>
</table>


Ora si supponga che un certo numero di utenti utilizzi lo stesso dispositivo di acquisizione ma un dispositivo di rendering diverso. In tal caso, nel report verrà visualizzata una voce nella seconda riga per tale combinazione univoca di dispositivo di acquisizione e dispositivo di rendering:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dispositivo di acquisizione</th>
<th>Dispositivo di rendering</th>
<th>Volume chiamata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microfono (HD Audio integrato digitale SoundMAX)</p></td>
<td><p>Auricolare e microtelefono (Microsoft LifeChat LX-3000)</p></td>
<td><p>254</p></td>
</tr>
<tr class="even">
<td><p>Microfono (HD Audio integrato digitale SoundMAX)</p></td>
<td><p>Altoparlanti (HD Audio integrato digitale SoundMAX)</p></td>
<td><p>319</p></td>
</tr>
</tbody>
</table>


Se si desidera visualizzare i totali combinati per un determinato dispositivo (ad esempio, per il dispositivo di acquisizione SoundMAX, indipendentemente dal dispositivo di rendering utilizzato), selezionare l'opzione appropriata dall'elenco a discesa Tipo di dispositivo (Dispositivo di acquisizione o Dispositivo di rendering). Se nell'esempio si seleziona Dispositivo di acquisizione, si riceverà il seguente output:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dispositivo di acquisizione</th>
<th>Volume chiamata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microfono (HD Audio integrato digitale SoundMAX)</p></td>
<td><p>573</p></td>
</tr>
</tbody>
</table>


## Accesso al Rapporto dispositivi

In genere è possibile accedere al Rapporto dispositivi dalla home page Relazioni monitoraggio. Tuttavia, se si visualizza [Rapporto dettagli chiamata in Lync Server 2013](lync-server-2013-call-detail-report.md), è possibile eseguire il drill-down al Rapporto dispositivi per un dispositivo specifico facendo clic su una delle metriche seguenti:

  - Dispositivo di acquisizione

  - Dispositivo di rendering

Nel Rapporto dispositivi è possibile eseguire il drill-down a [Rapporto Elenco chiamate in Lync Server 2013](lync-server-2013-call-list-report.md) facendo clic su una delle metriche seguenti:

  - Volume chiamata

  - Percentuale chiamate di livello insufficiente

## Utilizzo del Rapporto dispositivi

Il Rapporto dispositivi è molto dettagliato in merito ai nomi dei dispositivi. Ad esempio, si supponga di disporre dei dispositivi di acquisizione seguenti:

  - Microfono Aastra 3002 (2- Aastra 3002)

  - Microfono Aastra 3002 (3- Aastra 3002)

  - Microfono Aastra 3002 (Aastra 3002)

  - Aastra 6725ip

  - Microfono Aastra 6725ip (10- Aastra 6725ip)

  - Microfono Aastra 6725ip (10- Aastra 6725ip)-V0

  - Microfono Aastra 6725ip (2- Aastra 6725ip)

  - Microfono Aastra 6725ip (3- Aastra 6725ip)

  - Microfono Aastra 6725ip (4- Aastra 6725ip)

  - Microfono Aastra 6725ip (5- Aastra 6725ip)

  - Microfono Aastra 6725ip (6- Aastra 6725ip)

  - Microfono Aastra 6725ip (7- Aastra 6725ip)

  - Microfono Aastra 6725ip (9- Aastra 6725ip)

  - Microfono Aastra 6725ip (9- Aastra 6725ip)-V0

  - Microfono Aastra 6725ip (Aastra 6725ip)

  - Microfono Aastra 6725ip (Aastra 6725ip)-V0

  - Microfono Aastra 6725ip (dispositivo audio USB)

  - Microfono Aastra 6725ip (dispositivo audio USB)-V0


> [!NOTE]
> I nomi dei dispositivi di acquisizione potrebbero non essere gli stessi se si eseguono versioni localizzate di Lync Server 2013. Un dispositivo denominato Aastra 6725ip Microphone (Aastra 6725ip)-V0 in inglese (Stati Uniti) potrebbe avere un nome diverso in francese o spagnolo.



Anche se spesso è utile questo livello di dettaglio, a volte si potrebbe essere interessati solo al numero di chiamate che utilizzano qualsiasi microfono Aastra, indipendentemente dal numero del modello. Un modo per ottenere questo tipo di informazioni è esportare i dati del Rapporto dispositivi in Microsoft Excel e salvare i dati in un file di valori delimitati da virgole (ad esempio, C:\\Data\\Devices\_Report.csv). È possibile utilizzare un insieme di comandi simili a questi per importare il file CSV in Windows PowerShell e restituire il numero totale di chiamate eseguite utilizzando un dispositivo di acquisizione Aastra:

    $devices = Import-Csv "C:\Data\Device_Report.csv
    $sum = $devices | Where-Object {$_."Capture device" -match "Aastra"}
    $sum | foreach-object {[Int]$x = [Int]$x + [Int]$_."call volume"}
    $x

Verrà restituito un unico valore che rappresenta il numero totale di chiamate eseguite utilizzando un dispositivo di acquisizione Aastra. Ad esempio:

    384

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il Rapporto dispositivi consente di filtrare in base a elementi quali il tipo di chiamata (ossia se la chiamata è di tipo client) una conferenza telefonica o una chiamata PSTN (Public Switched Telephone Network). È inoltre possibile scegliere la modalità di raggruppamento dei dati. In questo caso i dispositivi sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella seguente sono elencati i filtri applicabili al Rapporto dispositivi.

### Filtri del Rapporto dispositivi

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Da</strong></p></td>
<td><p>Data/ora di inizio dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di inizio come indicato di seguito:</p>
<p>7/7/2012 13.00</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07.07.12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>03.07.12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 13.00</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07.07.12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>03.07.12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Causa commutazione vocale</strong></p></td>
<td><p>Motivo per cui è stato necessario effettuare una chiamata in modalità half-duplex per evitare l'eco. In modalità half-duplex la comunicazione può viaggiare in una sola direzione alla volta, in modo analogo ai turni effettuati dagli utenti in una comunicazione con un walkie-talkie. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>Nessuno</p>
</dd>
<dt><span></span></dt>
<dd><p>Timestamp non valido</p>
</dd>
<dt><span></span></dt>
<dd><p>Eco</p>
</dd>
<dt><span></span></dt>
<dd><p>DNLP (dynamic nonlinear processor)</p>
</dd>
<dt><span></span></dt>
<dd><p>Complessità bassa</p>
</dd>
<dt><span></span></dt>
<dd><p>Stato dispositivo non valido</p>
</dd>
<dt><span></span></dt>
<dd><p>Eco dopo eliminazione eco acustica</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>Causa eco</strong></p></td>
<td><p>Motivo per cui in una chiamata è stato rilevato l'eco sopra il livello accettato (nelle telecomunicazioni l'eco è un riflesso del suono, lo stesso effetto che si produce gridando verso il fondo di un pozzo). Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>Nessuno</p>
</dd>
<dt><span></span></dt>
<dd><p>Timestamp non valido</p>
</dd>
<dt><span></span></dt>
<dd><p>Eco dopo eliminazione eco acustica</p>
</dd>
<dt><span></span></dt>
<dd><p>ANLP (adaptive nonlinear processor)</p>
</dd>
<dt><span></span></dt>
<dd><p>DNLP (dynamic nonlinear processor)</p>
</dd>
<dt><span></span></dt>
<dd><p>Clip microfono</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di chiamata</strong></p></td>
<td><p>Indica il tipo di chiamata effettuata. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>Chiamata client</p>
</dd>
<dt><span></span></dt>
<dd><p>Chiamata PSTN</p>
</dd>
<dt><span></span></dt>
<dd><p>Conferenza telefonica</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di accesso</strong></p></td>
<td><p>Indica se al momento dell'esecuzione della chiamata il client era connesso alla rete interna o alla rete esterna. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>Interna</p>
</dd>
<dt><span></span></dt>
<dd><p>Esterna</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di rete</strong></p></td>
<td><p>Indica il tipo di rete a cui il client era connesso quando è stata effettuata la chiamata. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>Cablata</p>
</dd>
<dt><span></span></dt>
<dd><p>Wireless</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>VPN</strong></p></td>
<td><p>Indica se un client esterno utilizzava una connessione di rete privata virtuale (VPN) quando è stata effettuata la chiamata. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>[Tutto]</p>
</dd>
<dt><span></span></dt>
<dd><p>VPN</p>
</dd>
<dt><span></span></dt>
<dd><p>Non VPN</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di dispositivo</strong></p></td>
<td><p>Indica il tipo di dispositivo. Selezionare una delle opzioni seguenti:</p>
<dl>
<dt><span></span></dt>
<dd><p>Dispositivo di acquisizione</p>
</dd>
<dt><span></span></dt>
<dd><p>Dispositivo di rendering</p>
</dd>
<dt><span></span></dt>
<dd><p>Coppia di dispositivi di acquisizione/rendering</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>Nome dispositivo</strong></p></td>
<td><p>Nome del dispositivo di acquisizione o di rendering. È possibile immettere il nome completo del dispositivo o una parte di esso. Ad esempio, per trovare il dispositivo Microfono (Microsoft LifeCam VX-1000.), è possibile immettere il nome del dispositivo completo come segue:</p>
<p>Microfono (Microsoft LifeCam VX-1000.)</p>
<p>In alternativa, è possibile immettere solo una parte del nome, ad esempio:</p>
<p>LifeCam</p>
<p>Si noti che il filtro precedente restituisce qualsiasi dispositivo il cui nome contenga la stringa &quot;LifeCam&quot; in qualsiasi punto.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente sono elencate le informazioni fornite nel Rapporto dispositivi.

### Metriche del rapporto dispositivi

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Dispositivo di acquisizione</strong></p></td>
<td><p>Sì</p></td>
<td><p>Dispositivo (ad esempio un microfono o una webcam) utilizzato per la trasmissione dell'audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Dispositivo di rendering</strong></p></td>
<td><p>Sì</p></td>
<td><p>Dispositivo (ad esempio cuffie o altoparlanti) utilizzato per la ricezione dell'audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Volume chiamata</strong></p></td>
<td><p>Sì</p></td>
<td><p>Numero totale di chiamate effettuate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Percentuale chiamate di livello insufficiente</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale di chiamate classificate come &quot;di livello insufficiente&quot;. Una chiamata di livello insufficiente è una chiamata in cui almeno una delle metriche misurate supera il valore consentito (ad esempio una chiamata che presenta eccessiva instabilità).</p></td>
</tr>
<tr class="odd">
<td><p><strong>Utenti univoci</strong></p></td>
<td><p>Sì</p></td>
<td><p>Utenti univoci che hanno utilizzato il dispositivo. Se un utente ha utilizzato 13 volte il dispositivo, verrà conteggiato come utente univoco, come un utente che ha utilizzato il dispositivo una sola volta.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di tempo commutazione vocale</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale della chiamata che è stato necessario effettuare in modalità half-duplex per evitare l'eco. In modalità half-duplex la comunicazione può viaggiare in una sola direzione alla volta, in modo analogo ai turni effettuati dagli utenti in una comunicazione con un walkie-talkie.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporto di microfono non funzionante</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale della chiamata in cui il dispositivo di acquisizione non ha funzionato a un livello accettabile. Un valore elevato indica che i problemi di qualità della chiamata erano principalmente dovuti a un funzionamento improprio del dispositivo di acquisizione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di altoparlante non funzionante</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale della chiamata in cui il dispositivo di rendering non ha funzionato a un livello accettabile. Un valore elevato indica che i problemi di qualità della chiamata erano principalmente dovuti a un funzionamento improprio del dispositivo di rendering.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Chiamate con commutazione vocale (%)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale delle chiamate totali che è stato necessario effettuare in modalità half-duplex. In modalità half-duplex la comunicazione può viaggiare in una sola direzione alla volta, in modo analogo ai turni effettuati dagli utenti in una comunicazione con un walkie-talkie.</p></td>
</tr>
<tr class="even">
<td><p><strong>Eco microfono in ingresso (%)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale di tempo in cui viene rilevata l'eco nel flusso di acquisizione del microfono. In genere sono presenti valori ridotti per cuffie o ricevitori e valori più elevati per telefoni vivavoce o altoparlanti autonomi. Per i dispositivi che supportano l'eliminazione dell'eco acustica su scheda, i valori elevati indicano una perdita di eco. Per altri dispositivi, questa metrica non deve utilizzata per valutare la qualità del dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Invio eco (%)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale di eco trasmesso ad altri utenti.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamate con eco (%)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Percentuale delle chiamate totali con eco superiore al livello accettabile.</p>
<p></p></td>
</tr>
</tbody>
</table>

