---
title: 'Lync Server 2013: Rapporto di diagnostica attività peer-to-peer'
TOCTitle: Rapporto di diagnostica attività peer-to-peer
ms:assetid: 025e8ab4-2e64-4a6b-8f52-caf756a5cac3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558602(v=OCS.15)
ms:contentKeyID: 49299498
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto di diagnostica attività peer-to-peer in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto di diagnostica attività peer-to-peer fornisce informazioni sull'esito positivo o negativo delle sessioni di comunicazione peer-to-peer. Tenere presente che Microsoft Lync Server 2013 distingue tra diversi tipi di errore:

  - **Errore previsto** . Un errore previsto è in genere un errore solo nel senso più tecnico del termine. Si supponga ad esempio di chiamare un utente, che però non è in ufficio e dunque non può rispondere al telefono. Poiché la chiamata non ha ricevuto risposta, tecnicamente viene considerata un errore. D'altra parte, l'errore è previsto in quanto Microsoft Lync Server 2013 non si aspetta necessariamente una risposta da un utente non disponibile. Analogamente, si verificherà un errore previsto se si tenta di inviare un messaggio istantaneo a un utente offline, oppure connesso a un telefono che non supporta la messaggistica istantanea.

  - **Errore imprevisto** . Un errore imprevisto è, come indicato dal nome, un errore che in base alle circostanze non avrebbe dovuto verificarsi. Si supponga ad esempio di chiamare un utente e che quest'ultimo sia disponibile per rispondere alla chiamata. Quando tuttavia Lync Server 2013 tenta di instradare la chiamata alla segreteria telefonica, la chiamata non riesce perché la connettività alla messaggistica unificata di Exchange è stata persa. Questo è un errore imprevisto, in quanto dovrebbe essere sempre possibile instradare le chiamate alla segreteria telefonica. Come regola generale, gli errori imprevisti sono veri errori, problemi che probabilmente non è possibile risolvere attraverso la formazione degli utenti o adottando provvedimenti analoghi.

Tenere presente che la somma delle metriche relative a esiti positivi, errori previsti ed errori imprevisti potrebbe non corrispondere al valore della metrica Totale sessioni. Ad esempio, nell'illustrazione precedente sono presenti i valori seguenti:


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


Sommando 2024 + 469 + 16 si ottiene un totale di 2.509 sessioni, ma la colonna Totale sessioni mostra un totale di 2.521 sessioni. Le 12 sessioni "mancanti" sono quelle che il sistema non è riuscito a classificare come riuscite o non riuscite. Questo a volte si verifica quando un prodotto di terze parti introduce un nuovo codice diagnostico sconosciuto a Lync Server. Quando ciò accade, le chiamate effettuate usando tale prodotto e contrassegnate da tale codice diagnostico non sempre possono essere correttamente classificate come un esito positivo, un errore previsto o un errore imprevisto.

## Accesso al Rapporto di diagnostica attività peer-to-peer

Il rapporto di diagnostica peer-to-peer è accessibile dalla home page dei rapporti di monitoraggio. Per accedere al [Rapporto distribuzione errori in Lync Server 2013](lync-server-2013-failure-distribution-report.md) fare clic su una delle metriche seguenti:

  - Quantità di errori imprevisti

  - Quantità di errori previsti

## Uso ottimale del Rapporto di diagnostica attività peer-to-peer

È possibile filtrare il Rapporto di diagnostica attività peer-to-peer in vari modi, ma per impostazione predefinita le impostazioni di filtro sono nascoste. Per visualizzare le opzioni di filtro disponibili, fare clic sul pulsante Mostra/Nascondi parametri nell'angolo superiore destro della finestra del rapporto. Fatto questo, le opzioni di filtro saranno disponibili per l'utilizzo.

## Filtri

I filtri consentono di ottenere un set di dati più mirato o di visualizzare i dati restituiti in diversi modi. Il rapporto di diagnostica attività peer-to-peer ad esempio consente di filtrare i dati in base ad aspetti come la modalità della sessione, ovvero messaggistica istantanea, trasferimento di file o condivisione applicazioni. È inoltre possibile scegliere la modalità di raggruppamento dei dati. In tal caso, le chiamate vengono raggruppate in base all'ora, al giorno, alla settimana o al mese.

Nella tabella seguente sono riportati i filtri che è possibile utilizzare con il rapporto di diagnostica attività peer-to-peer.

### Filtri per il rapporto di diagnostica attività peer-to-peer

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
<td><p>Intervallo di tempo. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo giornaliero con la data di inizio 7/7/2012 e la data di fine 2/28/2012, verranno visualizzati i dati relativi ai giorni dal 8/7/2012 12:00 AM al 9/7/2012 12:00 AM, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutti]</strong> per visualizzare dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Modalità</strong></p></td>
<td><p>Indica il tipo di attività di comunicazione verificatasi. Selezionare una delle impostazioni seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Messaggistica istantanea</p></li>
<li><p>Trasferimento file</p></li>
<li><p>Condivisione applicazioni</p></li>
<li><p>Audio</p></li>
<li><p>Video</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metrica (per modalità)

Nella tabella seguente sono riportate le informazioni fornite nel rapporto di diagnostica attività peer-to-peer per le singole modalità.

### Metrica (per modalità)

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
<td><p><strong>Success volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni peer-to-peer con esito positivo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Success percentage</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni peer-to-peer completate con problemi significativi. Viene calcolata dividendo il valore Success volume per il valore Total sessions.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected failure volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni in cui si è verificato un &quot;errore previsto&quot;.</p>
<p>Per errore previsto si intende un errore che è previsto che si verifichi. Se ad esempio un utente imposta il proprio stato su Non disturbare, è previsto che qualsiasi chiamata effettuata a tale utente non riesca.</p></td>
</tr>
<tr class="even">
<td><p><strong>Expected failure percentage</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni peer-to-peer in cui si è verificato un errore previsto. Viene calcolata dividendo il valore Expected failure volume per il valore Total sessions.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Unexpected failure volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni in cui si è verificato un &quot;errore imprevisto&quot;.</p>
<p>Per errore non previsto si intende un errore che si verifica in un sistema che sembrerebbe altrimenti integro. Ad esempio, una chiamata non dovrebbe essere terminata se il chiamante la mette in attesa. Se questo errore si verifica, viene contrassegnato come imprevisto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Unexpected failure percentage</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni peer-to-peer in cui si è verificato un errore imprevisto. Viene calcolata dividendo il valore Unexpected failure volume per il valore Total sessions.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni, comprendente le sessioni con esito positivo, le sessioni con esito negativo (per errori sia previsti che imprevisti) e le sessioni senza categoria.</p></td>
</tr>
</tbody>
</table>

