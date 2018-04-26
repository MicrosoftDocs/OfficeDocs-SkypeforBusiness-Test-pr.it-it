---
title: 'Lync Server 2013: Rapporto di diagnostica conferenze'
TOCTitle: Rapporto di diagnostica conferenze
ms:assetid: e9edc23c-8ce8-4ab8-8786-9d22e1e51e14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615042(v=OCS.15)
ms:contentKeyID: 49302332
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto di diagnostica conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto di diagnostica conferenze fornisce informazioni sull'esito positivo o negativo di tutte le sessioni di conferenza. Si noti che Microsoft Lync Server distingue tra diversi tipi di errore:

  - **Errore previsto** . Un errore previsto è tipicamente un errore solo in senso strettamente tecnico. Si immagini ad esempio che qualcuno avvii una conferenza, ma poi riagganci prima che qualcuno possa parteciparvi. Tecnicamente parlando, si tratta di un errore: la conferenza è stata avviata, ma non completata. Si tratta tuttavia di un errore previsto: se l'organizzatore annulla la conferenza prima che qualcuno possa parteciparvi, non ci si può aspettare che la conferenza venga completata.

  - **Errore imprevisto** . Un errore imprevisto è esattamente tale, ovvero un errore che, in determinate circostanze, non ci si aspetterebbe. Si immagini ad esempio una conferenza che non possa essere tenuta perché non è possibile recuperare il criterio riunione dell'organizzatore. Questo è un errore imprevisto: dopotutto, dovrebbe essere sempre possibile recuperare il criterio riunione di un utente.

Si noti che le metriche di successo, errore previsto ed errore imprevisto potrebbero non sommarsi alla metrica totale delle sessioni. È ad esempio possibile che il report contenga i valori seguenti:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Esiti positivi</th>
<th>Errori previsti</th>
<th>Errori imprevisti</th>
<th>Totale sessioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2024</p></td>
<td><p>469</p></td>
<td><p>16</p></td>
<td><p>2521</p></td>
</tr>
</tbody>
</table>


Se si somma 2024 + 469 + 16 si ottiene un totale di 2.509 sessioni, tuttavia, nella colonna Totale sessioni viene indicato un totale di 2.521 sessioni. Le 12 sessioni "mancanti" sono quelle il cui esito non è stato definito come positivo o negativo. È ad esempio il caso di un prodotto di terze parti che introduce nuovo codice diagnostico ignoto a Monitoring Server. In questi casi le chiamate fatte utilizzando tale prodotto, che presentano quel codice diagnostico, non possono essere categorizzate con Esito positivo, Errore previsto o Errore imprevisto.

## Accesso al Rapporto di diagnostica conferenze

È possibile accedere al Rapporto di diagnostica conferenze dalla home page di Relazioni monitoraggio. È possibile accedere al [Rapporto distribuzione errori in Lync Server 2013](lync-server-2013-failure-distribution-report.md) facendo clic su una delle metriche seguenti:

  - Quantità di errori imprevisti

  - Quantità di errori previsti

## Utilizzare al meglio il Rapporto di diagnostica conferenze

Il Rapporto di diagnostica conferenze include una serie di grafici. Ogni colonna del grafico è un collegamento ipertestuale. Se si fa clic su una colonna viene visualizzato l'approfondimento del [Rapporto distribuzione errori in Lync Server 2013](lync-server-2013-failure-distribution-report.md) per quell'arco temporale e quel tipo di conferenza.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il Rapporto di diagnostica conferenze consente di filtrare in base al tipo di conferenza condotto (ad esempio, una conferenza basata su Focus) o al server perimetrale utilizzato nella conferenza. È inoltre possibile scegliere la modalità di raggruppamento dei dati. In questo caso le conferenze sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella che segue sono elencati i filtri applicabili al Rapporto di diagnostica conferenze.

### Filtri del Rapporto di diagnostica conferenze

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
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutti]</strong> per visualizzare dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni conferenza</strong></p></td>
<td><p>Indica il tipo di sessione di conferenza. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Sessioni Focus</p></li>
<li><p>Tutte le sessioni MCU</p></li>
<li><p>IM Conferencing</p></li>
<li><p>Condivisione applicazioni</p></li>
<li><p>Conferenze audio/video</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metriche

La tabella seguente elenca le informazioni disponibili nel Rapporto di diagnostica conferenza per tipo di sessione.

### Metriche del Rapporto di diagnostica conferenze

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
<td><p><strong>Volume di successo</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze riuscite.</p></td>
</tr>
<tr class="even">
<td><p><strong>Percentuale di successo</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di conferenze completate con problemi significativi. Questo valore viene calcolato dividendo la quantità di conferenze con esito positivo per il numero totale delle sessioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Volume di errori previsti</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze in cui si è verificato un errore previsto.</p>
<p>Per errore previsto si intende un errore che è previsto che si verifichi. Se ad esempio un utente imposta il proprio stato su Non disturbare, è previsto che qualsiasi chiamata effettuata a tale utente non riesca.</p></td>
</tr>
<tr class="even">
<td><p><strong>Percentuale di errori previsti</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di conferenze in cui si è verificato un errore previsto. Questo valore viene calcolato dividendo la quantità totale di errori previsti per il numero totale di sessioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Volume di errori imprevisti</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze in cui si è verificato un errore non previsto.</p>
<p>Per errore non previsto si intende un errore che si verifica in un sistema che sembrerebbe altrimenti integro. Ad esempio, una chiamata non dovrebbe essere terminata se il chiamante la mette in attesa. Se questo errore si verifica, viene contrassegnato come imprevisto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Percentuale di errori imprevisti</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di conferenze in cui si è verificato un errore imprevisto. Questo valore viene calcolato dividendo la quantità totale di errori imprevisti per il numero totale di sessioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze, incluse quelle riuscite, non riuscite (per errori previsti e imprevisti) e non categorizzate.</p></td>
</tr>
</tbody>
</table>

