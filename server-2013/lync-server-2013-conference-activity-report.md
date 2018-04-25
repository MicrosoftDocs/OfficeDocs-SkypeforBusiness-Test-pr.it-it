---
title: 'Lync Server 2013: Rapporto attività conferenza'
TOCTitle: Rapporto attività conferenza
ms:assetid: 22ddb509-af16-4fc8-9b98-6f58caa6f37e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558627(v=OCS.15)
ms:contentKeyID: 49299930
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto attività conferenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Con il Rapporto attività conferenza è semplice rispondere a domande come queste: quante conferenze si tengono ogni giorno e quando hanno luogo? Informazioni di questo tipo non sono solo utili di per sé, ma anche come strumenti di risoluzione dei problemi. Si supponga ad esempio che gli utenti si lamentino del fatto che la rete sia particolarmente lenta a metà giornata. Dando un'occhiata ai Rapporti attività conferenza è possibile individuarne il motivo: vengono programmate molte più conferenze tra le 10.00 e le 14.00 che in qualsiasi altro orario.

Se la lentezza della rete crea problemi, è possibile chiedere agli utenti di riprogrammare alcune delle conferenze in orari di minor traffico.

## Accesso al Rapporto attività conferenza

Al Rapporto attività conferenza si accede dal [Rapporto riepilogativo conferenze in Lync Server 2013](lync-server-2013-conference-summary-report.md) facendo clic su una delle metriche seguenti:

  - Totale conferenze

  - Totale partecipanti

## Utilizzo ottimale del Rapporto attività conferenza

Per impostazione predefinita, il Rapporto attività conferenza mostra il numero totale di conferenze per il periodo di tempo specificato (ad esempio il numero totale di conferenze al giorno oppure il numero totale di conferenze all'ora). È tuttavia anche possibile scegliere di visualizzare il numero totale di partecipanti per il periodo di tempo specificato o il numero totale di minuti partecipante. A tale scopo, fare clic sul pulsante Mostra/Nascondi parametri per visualizzare le opzioni di filtro, quindi selezionare una delle seguenti opzioni dall'elenco a discesa Rapporto di:

  - Numero partecipanti

  - Minuti partecipante

  - Numero conferenze

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto attività conferenza.

### Filtri per il Rapporto attività conferenza

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
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla 12:00 AM del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla 12:00 AM del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo giornaliero con la data di inizio 7/7/2012 e la data di fine 2/28/2012, verranno visualizzati i dati relativi ai giorni dal 8/7/2012 12:00 AM al 9/7/2012 12:00 AM, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di</strong></p></td>
<td><p>Indica i valori da utilizzare nel rapporto. È possibile selezionare uno dei valori seguenti:</p>
<ul>
<li><p>Numero partecipanti</p></li>
<li><p>Minuti partecipante</p></li>
<li><p>Numero conferenze</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metrica delle conferenze per pool

Nella tabella riportata di seguito vengono elencate le informazioni contenute nel Rapporto attività conferenza per ogni pool.

### Metrica delle conferenze per pool

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
<td><p>Nome del pool di registrazione o del server perimetrale utilizzato nella conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata tenuta la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di partecipanti, minuti totali dei partecipanti o numero di conferenze.</p></td>
</tr>
</tbody>
</table>


## Metrica delle conferenze per tipo di server

Nella tabella riportata di seguito vengono elencate le informazioni contenute nel Rapporto attività conferenza per ogni tipo di server.

### Metrica delle conferenze per tipo di server

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
<td><p><strong>Tipo server per conferenze</strong></p></td>
<td><p>No</p></td>
<td><p>Tipo di server utilizzato nella conferenza, in genere uno dei tipi seguenti:</p>
<ul>
<li><p>Web Conferencing Server</p></li>
<li><p>IM Conferencing Server</p></li>
<li><p>Telephony Conferencing Server</p></li>
<li><p>AV Conferencing Server</p></li>
<li><p>Condivisione applicazioni</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui è stata tenuta la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di partecipanti, minuti totali dei partecipanti o numero di conferenze.</p></td>
</tr>
</tbody>
</table>

