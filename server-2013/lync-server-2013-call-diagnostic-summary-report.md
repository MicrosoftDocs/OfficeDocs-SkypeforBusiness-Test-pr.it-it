---
title: 'Lync Server 2013: Rapporto riepilogativo di diagnostica chiamate'
TOCTitle: Rapporto riepilogativo di diagnostica chiamate
ms:assetid: 9091de56-13e6-440e-9353-f57c10c906fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615016(v=OCS.15)
ms:contentKeyID: 49301320
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto riepilogativo di diagnostica chiamate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto riepilogativo di diagnostica chiamate offre un quadro generale delle sessioni di conferenza e peer-to-peer non riuscite. Il rapporto illustra la percentuale generale degli errori per entrambi i tipi di sessioni e ulteriori dettagli sui problemi in base al tipo di modalità della sessione:

  - Messaggistica istantanea

  - Condivisione applicazioni

  - Trasferimento file

  - Audio

  - Video

## Accesso al Rapporto riepilogativo di diagnostica chiamate

Il Rapporto riepilogativo di diagnostica chiamate è accessibile dalla home page Rapporti di monitoraggio. Dal Rapporto riepilogativo di diagnostica chiamate è possibile accedere al [Rapporto di diagnostica attività peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-activity-diagnostic-report.md) facendo clic sulla metrica Frequenza errori nella sezione di riepilogo delle sessioni peer-to-peer del rapporto. È inoltre possibile accedere al [Rapporto di diagnostica conferenze in Lync Server 2013](lync-server-2013-conference-diagnostic-report.md) facendo clic su una o più delle metriche seguenti sulle conferenze:

  - Frequenza generale errori sessione

  - Frequenza errori Focus

  - Frequenza errori MCU

## Uso ottimale del Rapporto riepilogativo di diagnostica chiamate

Il Rapporto riepilogativo di diagnostica chiamate include grafici che consentono di confrontare le frequenze di errori per le diverse modalità usate in Microsoft Lync Server 2013. Le colonne dei grafici sono in effetti collegamenti consigliati, ad esempio se si fa clic sulla colonna Messaggistica istantanea per le sessioni peer-to-peer si esegue il drill-down a un'istanza del [Rapporto di diagnostica attività peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-activity-diagnostic-report.md), il quale offre ulteriori dettagli sulle sessioni di messaggistica istantanea incluse nel Rapporto riepilogativo di diagnostica chiamate.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il rapporto riepilogativo di diagnostica chiamate consente di filtrare in base al pool di registrazione o al server perimetrale utilizzato nella sessione. È inoltre possibile scegliere la modalità di raggruppamento dei dati. In questo caso le chiamate sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella seguente sono elencati i filtri applicabili al rapporto riepilogativo di diagnostica chiamate.

### Filtri del Rapporto riepilogativo di diagnostica chiamate

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
<p>7/7/12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>3/7/12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>3/7/12</p>
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
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo giornaliero con la data di inizio 7/8/2012 e la data di fine 28/9/2012, verranno visualizzati i dati relativi ai giorni dal 7/8/2012 alle 00.00 al 7/9/2012 alle 00.00, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutti]</strong> per visualizzare dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
</tbody>
</table>


## Metriche per le sessioni peer-to-peer

La tabella seguente elenca le informazioni disponibili nel Rapporto riepilogativo di diagnostica chiamate per le sessioni peer-to-peer di conferenza, ovvero le sessioni che coinvolgono solo due partecipanti.

### Metriche per le sessioni peer-to-peer

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
<td><p><strong>Totale sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni peer-to-peer condotte.</p></td>
</tr>
<tr class="even">
<td><p><strong>Frequenza errori</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale delle sessioni peer-to-peer non riuscite. Facendo clic su questo elemento verrà visualizzato il Rapporto di diagnostica attività peer-to-peer, che mostra informazioni più dettagliate sulle sessioni peer-to-peer non riuscite.</p></td>
</tr>
</tbody>
</table>


## Metriche per le sessioni di conferenza

La tabella seguente elenca le informazioni disponibili nel rapporto di diagnostica chiamate per le sessioni di conferenza, ovvero le sessioni che coinvolgono tre o più partecipanti.

### Metriche per le sessioni di conferenza

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
<td><p><strong>Totale conferenze</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze condotte.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale sessioni conferenza</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni di conferenza condotte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza generale errori sessione</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale del totale di sessioni di conferenza non riuscite.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni Focus</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni di conferenza basate su Focus non riuscite.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza errori Focus</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale delle sessioni di conferenza basate su Focus non riuscite.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni MCU</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze basate su server per conferenze (in precedenza MCU, Multipoint Control Unit) non riuscite.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza errori MCU</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di totale di conferenze basate su server per conferenze (in precedenza MCU, Multipoint Control Unit) non riuscite.</p></td>
</tr>
</tbody>
</table>

