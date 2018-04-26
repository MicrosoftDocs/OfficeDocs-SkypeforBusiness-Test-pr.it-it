---
title: Rapporto distribuzione metriche di qualità multimediale in Lync Server 2013
TOCTitle: Rapporto distribuzione metriche di qualità multimediale
ms:assetid: d07996e6-b0a5-4ff8-9512-ab707762b4e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205262(v=OCS.15)
ms:contentKeyID: 49302040
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto distribuzione metriche di qualità multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto distribuzione metriche di qualità multimediale consente di visualizzare un grafico con i valori di distribuzione per una metrica di qualità percepita dagli utenti (QoE), ad esempio l'instabilità o la perdita di pacchetti. Si supponga ad esempio che gli utenti eseguano un totale di 10 chiamate telefoniche per le quali vengono segnalati i tempi di roundtrip seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero chiamata</th>
<th>Tempo di roundtrip (millisecondi)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p>50</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>4550</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p>50</p></td>
</tr>
</tbody>
</table>


La media di questi tempi di roundtrip è di 500 millisecondi (5000 diviso per 10). Poiché si tratta di un tempo di roundtrip estremamente elevato, è plausibile supporre un problema grave di congestione della rete. Valori di tempi di roundtrip elevati infatti in genere sono il risultato di reti sovraccariche.

In realtà per il 90% delle chiamate sono stati registrati tempi di roundtrip eccellenti. Solo una chiamata con tempi pessimi ha alterato i risultati globali. Esaminando solo il tempo medio di roundtrip è possibile che si giunga a una conclusione errata.

Il Rapporto distribuzione metriche di qualità multimediale consente di evitare di giungere a conclusioni errate poiché mostra una distribuzione grafica di una determinata metrica, ad esempio il tempo di roundtrip. Da questi grafici risulta chiaramente che la qualità è stata ottima per nove chiamate e pessima solo per una chiamata. Pur essendo opportuno analizzare la chiamata con problemi di qualità, il fatto che nove chiamate su dieci siano state di qualità ottima indica che non è necessario apportare modifiche drastiche alla rete, almeno non in questo momento.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto distribuzione metriche di qualità multimediale.

### Filtri del Rapporto distribuzione metriche di qualità multimediale

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
<p>07/07/2012 13.00</p>
<p>Se non si immette una data/ora di inizio, il rapporto inizia automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>07/07/2012 13.00</p>
<p>Se non si immette una data/ora di fine, il rapporto termina automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Valore minimo nell'asse x</strong></p></td>
<td><p>Valore minimo da visualizzare sull'asse X del grafico.</p></td>
</tr>
<tr class="even">
<td><p><strong>Valore massimo nell'asse x</strong></p></td>
<td><p>Valore massimo da visualizzare sull'asse X del grafico.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di accesso</strong></p></td>
<td><p>Indica se al momento dell'esecuzione della chiamata il client era connesso alla rete interna o alla rete esterna. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>[Tutte]</p></li>
<li><p>Interne</p></li>
<li><p>Esterne</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>VPN</strong></p></td>
<td><p>Indica se un client esterno utilizzava una connessione di rete privata virtuale (VPN) quando è stata effettuata la chiamata. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>[Tutte]</p></li>
<li><p>VPN</p></li>
<li><p>Non VPN</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di rete</strong></p></td>
<td><p>Indica il tipo di rete a cui il client era connesso quando è stata effettuata la chiamata. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>[Tutte]</p></li>
<li><p>Cablate</p></li>
<li><p>Wireless</p></li>
</ul></td>
</tr>
</tbody>
</table>

