---
title: 'Lync Server 2013: Rapporto voce e video peer-to-peer'
TOCTitle: Rapporto voce e video peer-to-peer
ms:assetid: e17c36b5-5a2f-4673-9696-3b2d31c2bb2f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615040(v=OCS.15)
ms:contentKeyID: 49302241
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto voce e video peer-to-peer in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto voce e video peer-to-peer consente di esaminare in modo dettagliato la distribuzione delle chiamate voce e video per un periodo di tempo specificato, ad esempio le chiamate per ora o per giorno. Il rapporto offre inoltre la possibilità di visualizzare tutte le chiamate voce e video effettuate oppure solo quelle riuscite o non riuscite. Le informazioni sulle chiamate nel rapporto sono suddivise nei raggruppamenti seguenti:

  - Chiamate per pool

  - Chiamate per tipo (ad esempio una chiamata da Lync a Lync o una chiamata da Lync a una persona sulla rete PSTN)

  - Chiamate per tipo di accesso (utenti connessi alla rete interna o alla rete esterna)

  - Chiamate per Mediation Server

## Per accedere al rapporto voce e video peer-to-peer

L'unico modo per accedere al Rapporto voce e video peer-to-peer consiste nell'aprire il Rapporto riepilogativo attività peer-to-peer e fare clic su una delle metriche seguenti:

  - Totale sessioni audio peer-to-peer

  - Totale minuti sessioni audio peer-to-peer

  - Totale sessioni audio peer-to-peer

  - Totale minuti sessioni video peer-to-peer

## Per utilizzare in modo ottimale il rapporto voce e video peer-to-peer

È possibile filtrare il Rapporto voce e video peer-to-peer in vari modi. Le opzioni di filtro, tuttavia, sono nascoste dalla visualizzazione per impostazione predefinita. Per visualizzare le opzioni di filtro disponibili, fare clic sul pulsante **Mostra/Nascondi parametri** nell'angolo in alto a destra della finestra Rapporto.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati. Nella tabella seguente sono elencati i filtri che è possibile utilizzare con il Rapporto voce e video peer-to-peer.

### Filtri per il rapporto voce e video peer-to-peer

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
<td><p>Data e ora di inizio per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di inizio come segue:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo giornaliero con la data di inizio 07/08/2012 e la data di fine 28/09/2012, verranno visualizzati i dati relativi ai giorni dal 07/08/2012 alle 00.00 al 07/09/2012 alle 00.00, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di supporto</strong></p></td>
<td><p>Indica il tipo di supporto utilizzato nella sezione. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Entrambi</p></li>
<li><p>Audio</p></li>
<li><p>Video</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Disposizione chiamata</strong></p></td>
<td><p>Indica l'esito positivo o negativo della sezione. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Chiamate riuscite</p></li>
<li><p>Chiamate non riuscite</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di</strong></p></td>
<td><p>Indica i valori da utilizzare nel rapporto. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Numero di sessioni</p></li>
<li><p>Minuti chiamata</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metriche per le attività voce e video peer-to-peer per pool

Nella tabella seguente sono elencate le informazioni fornite nel Rapporto voce e video peer-to-peer per ogni pool.

### Metriche per le attività voce e video peer-to-peer per pool

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
<td><p><strong>Pool</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del pool di registrazione o del server perimetrale utilizzato per la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata effettuata la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>


## Metriche per le attività voce e video peer-to-peer per tipo di chiamata

Nella tabella seguente sono elencate le informazioni fornite nel Rapporto voce e video peer-to-peer per ogni tipo di chiamata effettuata.

### Metriche per le attività voce e video peer-to-peer per tipo di chiamata

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
<td><p><strong>Tipo di chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Indica il tipo di chiamata che è stata effettuata. I valori sono uno dei seguenti:</p>
<ul>
<li><p>Da UC a UC</p></li>
<li><p>Da UC a PSTN</p></li>
<li><p>Da PSTN a UC</p></li>
<li><p>Da PSTN a PSTN</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata effettuata la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>


## Metriche per le attività voce e video peer-to-peer per tipo di accesso

Nella tabella seguente sono elencate le informazioni fornite nel Rapporto voce e video peer-to-peer per ogni tipo di accesso di rete.

### Metriche per le attività voce e video peer-to-peer per tipo di accesso

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
<td><p><strong>Tipo di attività</strong></p></td>
<td><p>No</p></td>
<td><p>Indica se al momento dell'esecuzione della chiamata i client sono connessi alla rete interna o a quella esterna. I valori sono in genere i seguenti:</p>
<ul>
<li><p>Interna</p></li>
<li><p>Esterna</p></li>
<li><p>Misto</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata effettuata la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>


## Metriche per le attività voce e video peer-to-peer per Mediation Server

Nella tabella seguente sono elencate le informazioni fornite nel Rapporto voce e video peer-to-peer per ogni Mediation Server.

### Metriche per le attività voce e video peer-to-peer per Mediation Server

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
<td><p><strong>Mediation Server</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata effettuata la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>

