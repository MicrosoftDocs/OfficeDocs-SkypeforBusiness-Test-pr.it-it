---
title: 'Lync Server 2013: Rapporto Elenco chiamate'
TOCTitle: Rapporto Elenco chiamate
ms:assetid: 9739f9f0-7a37-4844-91d5-f089d2011013
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615020(v=OCS.15)
ms:contentKeyID: 49301411
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto Elenco chiamate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il rapporto Elenco chiamate offre metriche QoE (Quality of Experience) per le singole chiamate effettuate e ricevute nell'organizzazione. Tenere presente che le metriche effettive riportate dipendono dalla modalità di accesso al rapporto Elenco chiamate. Se ad esempio si apre il rapporto dal [Rapporto dispositivi in Lync Server 2013](lync-server-2013-device-report.md), verranno visualizzate metriche quali le seguenti, le quali sono incluse anche nel rapporto sui dispositivi:

  - Microfono del chiamante

  - Altoparlante del chiamante

  - Microfono del chiamato

  - Altoparlante del chiamato

  - Rapporto di tempo commutazione vocale

Se tuttavia si apre il rapporto Elenco chiamate dal [Rapporto percorsi in Lync Server 2013](lync-server-2013-location-report.md), queste metriche non verranno visualizzate mentre saranno disponibili le seguenti:

  - Roundtrip (ms)

  - Degradazione (MOS)

  - Perdita di pacchetti

  - Instabilità (ms)

Si tratta delle metriche riportate nel Rapporto percorsi. Tuttavia, nel rapporto Elenco chiamate è sempre possibile fare clic sulla metrica Dettagli per ottenere informazioni di QoE complete per qualsiasi chiamata.

## Accesso al rapporto Elenco chiamate

Il rapporto Elenco chiamate è accessibile da qualsiasi dei rapporti seguenti:

  - [Rapporto percorsi in Lync Server 2013](lync-server-2013-location-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale di chiamate di livello insufficiente)

  - [Rapporto dispositivi in Lync Server 2013](lync-server-2013-device-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale di chiamate di livello insufficiente)

  - [Rapporto riepilogativo qualità multimediale in Lync Server 2013](lync-server-2013-media-quality-summary-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale di chiamate di livello insufficiente)

  - [Rapporto prestazioni dei server in Lync Server 2013](lync-server-2013-server-performance-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale di chiamate di livello insufficiente)

Nel rapporto Elenco chiamate è possibile accedere al [Rapporto dettagli chiamata in Lync Server 2013](lync-server-2013-call-detail-report.md) facendo clic sulla metrica Dettagli.

## Uso ottimale del rapporto Elenco chiamate

Se non si è certi del tipo di misurazioni offerte dalle metriche del rapporto Elenco chiamate (ad esempio il rapporto di tempo di commutazione vocale), tenere il puntatore del mouse sull'etichetta per visualizzare una descrizione comandi con informazioni sintetiche sulla metrica in questione.

## Filtri

Nessuno. Non è possibile filtrare il rapporto Elenco chiamate.

## Metriche

La tabella seguente elenca le informazioni disponibili nel rapporto Elenco chiamate per ogni chiamata.

### Metriche del rapporto Elenco chiamate

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
<td><p><strong>Dettagli</strong></p></td>
<td><p>No</p></td>
<td><p>Facendo clic su questo elemento è possibile visualizzare ulteriori informazioni sulla chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamante</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Destinatario chiamata</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente chiamato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora inizio</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di inizio della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora fine</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di fine della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Agente utente chiamante</strong></p></td>
<td><p>Sì</p></td>
<td><p>Software utilizzato dall'endpoint dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agente utente destinatario chiamata</strong></p></td>
<td><p>Sì</p></td>
<td><p>Software utilizzato dall'endpoint dell'utente che è stato chiamato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Roundtrip (ms)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Tempo medio di roundtrip (in millisecondi) richiesto per il viaggio di andata e ritorno di un pacchetto RTP (Real-Time Transport Protocol) verso e da un altro endpoint. I roundtrip che non superano i 100 millisecondi vengono considerati accettabili.</p>
<p>Valori di roundtrip elevati possono essere causati dal routing di chiamate internazionali, da una configurazione errata del routing o da un server di contenuti multimediali sovraccarico. Tempi di roundtrip elevati generano difficoltà nelle conversazioni audio in tempo reale bidirezionali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Degradazione (MOS)</strong></p></td>
<td><p>Sì</p></td>
<td><p>Valore medio di degradazione MOS (Mean Opinion Score) osservata durante una chiamata. I valori di degradazione possono essere compresi tra un minimo di 0 e un massimo di 5. Il valore 0,5 o inferiore rappresenta una degradazione accettabile. In passato, i valori MOS venivano calcolati chiedendo agli utenti di valutare la qualità di una chiamata su una scala da 1 a 5. In Lync Server viene utilizzato un set di algoritmi per prevedere in che modo gli utenti valuteranno una chiamata di Lync Server.</p>
<p>Valori di degradazione elevati possono essere causati da congestione, mancanza di larghezza di banda, interferenze o congestione della rete wireless o da un endpoint o un server di contenuti multimediali sovraccarico. Una degradazione elevata genera audio distorto o perdita di audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Perdita di pacchetti</strong></p></td>
<td><p>Sì</p></td>
<td><p>Frequenza media di perdita di pacchetti RTP. La perdita di pacchetti si verifica quando i pacchetti RTP, ovvero un protocollo utilizzato per la trasmissione audio e video su Internet, non riescono a raggiungere la destinazione. Frequenze di perdita elevate sono in genere causate da congestione, mancanza di larghezza di banda, interferenze o congestione della rete wireless o da un server di contenuti multimediali sovraccarico. La perdita di pacchetti di solito genera audio distorto o perdita di audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Instabilità</strong></p></td>
<td><p>Sì</p></td>
<td><p>Instabilità media rilevata tra gli arrivi dei pacchetti RTP (Real-Time Transport Protocol). L'instabilità è un indice della qualità di una chiamata. Valori di instabilità elevati sono generalmente dovuti a congestione o overload di un server di contenuti multimediali e comportano distorsione o perdita di audio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto campioni nascosti utilità di ripristino</strong></p></td>
<td><p>Sì</p></td>
<td><p>Rapporto medio tra i campioni audio nascosti e il numero totale di campioni. Un campione audio nascosto è una tecnica utilizzata per mitigare le transazioni improvvise generalmente causate dall'eliminazione di pacchetti di rete. Valori elevati indicano l'applicazione di livelli significativi di soppressione della perdita applicata dovuti a perdita di pacchetti o instabilità, con conseguente audio distorto o perdita di audio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporto campioni estesi utilità di ripristino</strong></p></td>
<td><p>Sì</p></td>
<td><p>Rapporto medio tra i campioni audio estesi e il numero totale di campioni. Con audio esteso si intende l'audio che è stato espanso per garantire la qualità delle chiamate quando viene rilevato un pacchetto di rete eliminato. Valori elevati indicano livelli significativi di estensione dei campioni dovuti a instabilità, con conseguente riproduzione di audio robotico o distorto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto campioni compressi utilità di ripristino</strong></p></td>
<td><p>Sì</p></td>
<td><p>Rapporto medio tra i campioni audio compressi e il numero totale di campioni. L'audio compresso è audio che è stato compresso per mantenere la qualità della chiamata quando è stato rilevato un pacchetto di rete eliminato. Valori alti indicano livelli significativi di compressione dei campioni dovuti a instabilità con conseguente riproduzione di audio accelerato o distorto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Connettività</strong></p></td>
<td><p>Sì</p></td>
<td><p>Tipo di collegamento di comunicazione wireless. In genere è uno dei seguenti:</p>
<ul>
<li><p>Relay</p></li>
<li><p>Diretta</p></li>
</ul></td>
</tr>
</tbody>
</table>

