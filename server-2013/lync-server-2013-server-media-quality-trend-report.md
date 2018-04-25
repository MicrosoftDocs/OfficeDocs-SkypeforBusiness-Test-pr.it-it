---
title: Rapporto tendenze qualità multimediale server in Lync Server 2013
TOCTitle: Rapporto tendenze qualità multimediale server in Lync Server 2013
ms:assetid: 8a51fd13-1487-4632-b5ec-f7ae2abe8ed4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205071(v=OCS.15)
ms:contentKeyID: 49301252
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto tendenze qualità multimediale server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto tendenze qualità multimediale server offre un modo per confrontare graficamente fino a 5 server relativamente a metriche QoE quali il volume di chiamata, la percentuale di chiamate di livello insufficiente, la perdita di pacchetti e l'instabilità. Ciò agevola attività quali l'identificazione dei server con prestazioni insufficienti, sottoutilizzati o sovrautilizzati.

## Accesso al Rapporto tendenze qualità multimediale server

Il Rapporto tendenze qualità multimediale server è accessibile da uno o l'altro dei rapporto seguenti:

  - [Rapporto prestazioni dei server in Lync Server 2013](lync-server-2013-server-performance-report.md) (facendo clic sulla metrica Tendenza)

  - [Rapporto dettagli chiamata in Lync Server 2013](lync-server-2013-call-detail-report.md) (facendo clic sulla metrica A/V Edge Server; se il chiamante o il chiamato è un server, è anche possibile raggiungere il Rapporto tendenze qualità multimediale server facendo clic sul nome dell'endpoint)

## Uso ottimale del Rapporto tendenze qualità multimediale server

Quando si fa clic sulla metrica Tendenza nel [Rapporto prestazioni dei server in Lync Server 2013](lync-server-2013-server-performance-report.md) per un server specifico, viene aperto il Rapporto tendenze qualità multimediale server. Tuttavia, verrà visualizzata solo un'istanza vuota del rapporto; il server selezionato nel Rapporto prestazioni dei server non verrà visualizzato. Sarà invece necessario selezionare il server dal menu a discesa Server. Tenere presente che l'elenco a discesa Server include anche un'opzione Seleziona tutto. Questa opzione non funziona se sono presenti più di 5 server; il Rapporto tendenze qualità multimediale server è in grado di visualizzare dati per un massimo di 5 server alla volta.

Nei grafici visualizzati dal Rapporto tendenze qualità multimediale server, i punti con etichetta Volume chiamata e Percentuale di chiamate di livello insufficiente sono collegamenti consigliati; facendo clic su un punto del grafico viene aperta un'istanza del [Rapporto Elenco chiamate in Lync Server 2013](lync-server-2013-call-list-report.md) che illustra il numero totale di chiamate (o di chiamate di livello insufficiente) per il periodo di tempo specificato.

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto tendenze qualità multimediale server.

### Filtri del Rapporto tendenze qualità multimediale server

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
<td><p>Data/ora di inizio per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di inizio come segue:</p>
<p>7/7/2012 13.00</p>
<p>Se non si immette una data/ora di inizio, il rapporto inizia automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>3/7/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>7/7/2012 13.00</p>
<p>Se non si immette una data/ora di fine, il rapporto termina automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>3/7/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo Giornaliero con la data di inizio 07.07.12 e la data di fine 28.02.12, verranno visualizzati i dati relativi ai giorni da 07.08.12 alle 00.00 a 07.09.12 alle 00.00, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di server</strong></p></td>
<td><p>Tipo di server coinvolto nella chiamata. Valori consentiti:</p>
<ul>
<li><p>Mediation Server</p></li>
<li><p>A/V Conferencing Server</p></li>
<li><p>A/V Edge Server</p></li>
<li><p>Gateway (Mediation Server)</p></li>
<li><p>Gateway (bypass a Mediation Server)</p></li>
<li><p>AS Conferencing Server</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Servers</strong></p></td>
<td><p>Nome del server coinvolto nella sessione; questo elenco a discesa viene automaticamente popolato in base al valore del filtro Tipo di server. È possibile selezionare fino a 5 diversi server per la compilazione di un rapporto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di accesso</strong></p></td>
<td><p>Indica se il partecipante era connesso alla rete interna o dalla rete esterna. Valori consenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Interna</p></li>
<li><p>Esterna</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di rete</strong></p></td>
<td><p>Indica il tipo di rete a cui era connesso il partecipante. Valori consentiti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Cablata</p></li>
<li><p>Wireless</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>VPN</strong></p></td>
<td><p>Indica se un partecipante esterno utilizzava una connessione di rete privata virtuale (VPN) durante la sessione. Valori consentiti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>VPN</p></li>
<li><p>Non VPN</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente sono elencate le informazioni disponibili nel Rapporto tendenze qualità multimediale server.

### Metriche del Rapporto tendenze qualità multimediale server

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
<td><p><strong>Volume chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate</p></td>
</tr>
<tr class="even">
<td><p><strong>Degradazione (MOS)</strong></p></td>
<td><p>No</p></td>
<td><p>Degradazione MOS (Mean Opinion Score) media sperimentata durante una chiamata. I valori di degradazione possono oscillare da un minimo di 0,0 a un massimo di 5,0. Un valore di 0,5 o inferiore rappresenta una degradazione accettabile. In passato questo valore veniva calcolato chiedendo agli utenti di valutare la qualità di una chiamata in una scala da 1 a 5. In Lync Server si usa un set di algoritmi per prevedere in che modo gli utenti avrebbero valutato la chiamata.</p>
<p>Valori di degradazione elevati possono essere causati da congestione, mancanza di larghezza di banda, interferenze o congestione della rete wireless o da un endpoint o un server di contenuti multimediali sovraccarico. Una degradazione elevata genera audio distorto o perdita di audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Percentuale chiamate di livello insufficiente</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di chiamate classificate come di livello insufficiente. In una chiama di livello insufficiente almeno una delle metriche misurate supera il valore consentito, ad esempio viene rilevato un livello di instabilità eccessivo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Roundtrip (ms)</strong></p></td>
<td><p>No</p></td>
<td><p>Tempo medio (in millisecondi) richiesto per il roundtrip di un pacchetto RTP (Real-Time Transport Protocol) verso e da un altro endpoint. I roundtrip che non superano i 200 millisecondi vengono considerati accettabili.</p>
<p>Valori alti di tempo di roundtrip possono essere dovuti a routing delle chiamate internazionali, errata configurazione del routing o sovraccarico del server dei contenuti multimediali con conseguenti difficoltà nelle conversazioni audio bidirezionali in tempo reale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Perdita di pacchetti</strong></p></td>
<td><p>No</p></td>
<td><p>Frequenza media di perdita di pacchetti RTP (Real-Time Transport Protocol). La perdita di pacchetti si verifica quando i pacchetti RTP, un protocollo utilizzato per la trasmissione di audio e video su Internet, non raggiungono la destinazione. Valori alti di perdita sono in genere dovuti a congestione, superamento della larghezza di banda disponibile, congestione/interferenze wireless o sovraccarico del server dei contenuti multimediali con conseguente audio distorto o perdita di audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Instabilità (ms)</strong></p></td>
<td><p>No</p></td>
<td><p>Instabilità media rilevata tra gli arrivi di pacchetti RTP. L'instabilità è una misura dell'inattendibilità di una chiamata. Valori elevati di instabilità sono in genere causati da congestione o da un server di contenuti multimediali sovraccarico e generano audio distorto o perdita di audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporto campioni nascosti utilità di ripristino</strong></p></td>
<td><p>No</p></td>
<td><p>Rapporto medio tra i campioni audio nascosti e il numero totale di campioni. Un campione audio nascosto è una tecnica utilizzata per mitigare le transazioni improvvise generalmente causate dall'eliminazione di pacchetti di rete. Valori elevati indicano l'applicazione di livelli significativi di soppressione della perdita applicata dovuti a perdita di pacchetti o instabilità, con conseguente audio distorto o perdita di audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto campioni estesi utilità di ripristino</strong></p></td>
<td><p>No</p></td>
<td><p>Rapporto medio tra i campioni audio estesi e il numero totale di campioni. Con audio esteso si intende l'audio che è stato espanso per garantire la qualità delle chiamate quando viene rilevato un pacchetto di rete eliminato. Valori elevati indicano livelli significativi di estensione dei campioni dovuti a instabilità, con conseguente riproduzione di audio robotico o distorto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporto campioni compressi utilità di ripristino</strong></p></td>
<td><p>No</p></td>
<td><p>Rapporto medio tra i campioni audio compressi e il numero totale di campioni. L'audio compresso è audio che è stato compresso per mantenere la qualità della chiamata quando è stato rilevato un pacchetto di rete eliminato. Valori alti indicano livelli significativi di compressione dei campioni dovuti a instabilità con conseguente riproduzione di audio accelerato o distorto.</p></td>
</tr>
</tbody>
</table>

