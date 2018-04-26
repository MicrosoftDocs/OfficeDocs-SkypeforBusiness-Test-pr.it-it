---
title: 'Lync Server 2013: Rapporto riepilogativo conferenze'
TOCTitle: Rapporto riepilogativo conferenze
ms:assetid: 62f54812-5700-45a3-8526-8f58b0f77fbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558656(v=OCS.15)
ms:contentKeyID: 49300773
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto riepilogativo conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto riepilogativo conferenze offre una visuale generale delle sessioni di conferenza online. Una conferenza coinvolge in genere più di 2 utenti e richiede l'utilizzo dei servizi di conferenza di Microsoft Lync Server 2013. Una sessione peer-to-peer, invece, coinvolge in genere solo 2 utenti e non richiede l'utilizzo dei servizi di conferenza di Lync Server. Le attività peer-to-peer sono riepilogate nel [Rapporto riepilogativo attività peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-activity-summary-report.md).

Il Rapporto riepilogativo conferenze non solo indica il numero di conferenze tenutesi durante un periodo di tempo specificato (giornaliere, settimanali o mensili), ma indica anche il numero totale di persone che hanno partecipato a tali conferenze e il numero totale di organizzatori univoci.

Con organizzatore "univoco” si intende qualsiasi utente che pianifica almeno una conferenza. Se Pilar Ackerman pianifica una conferenza, ad esempio, sarà conteggiata come organizzatore univoco. Se Ken Myer pianifica 148 conferenze, anche lui sarà conteggiato come singolo organizzatore univoco. La tabella seguente, ad esempio, indica 8 conferenze pianificate ma solo tre organizzatori univoci, ovvero Ken Myer, Pilar Ackerman e David Ahs.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Organizzatore conferenza</th>
<th>Data conferenza</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>David Ahs</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 1:00 PM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 2:00 PM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
</tbody>
</table>


Il Rapporto riepilogativo conferenze indica inoltre il numero di conferenze con audio e video.

## Accesso al rapporto riepilogativo conferenze

È possibile accedere al rapporto riepilogativo conferenze dalla home page Relazioni monitoraggio. È possibile eseguire il drill-down al Rapporto attività conferenza facendo clic su una delle metriche seguenti:

  - Totale conferenze

  - Totale partecipanti

## Utilizzo ottimale del rapporto riepilogativo conferenze

I valori totali per la maggior parte delle metriche utilizzate nel Rapporto riepilogativo conferenze sono disponibili nella parte inferiore del rapporto. Scorrere verso il basso per visualizzare valori come il numero totale di conferenze tenutesi durante il periodo di tempo specificato e il numero totale di persone che hanno partecipato a tali conferenze. Una metrica per la quale non è disponibile il totale nella parte inferiore del rapporto è Totale organizzatori conferenza univoci. Uno dei motivi è questo: si supponga di voler esaminare i dati mensili. Nel giorno 1 sono stati rilevati 34 organizzatori di conferenza univoci, nel giorno 2 gli organizzatori univoci sono 27. Ciò non significa tuttavia che per i due giorni il totale degli organizzatori univoci sia 61. Tutte le 27 persone che hanno organizzato conferenze nel giorno 2 potrebbero essere infatti incluse nei 34 organizzatori univoci del giorno 1. In questo semplice rapporto, ad esempio, notare che Ken Myer e Pilar Ackerman hanno pianificato conferenze sia in data 7/7/2012 che in data 7/2/2012:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Organizzatore conferenza</th>
<th>Data conferenza</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>David Ahs</p></td>
<td><p>7/7/2012 10:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 11:00 AM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/7/2012 1:00 PM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/7/2012 2:00 PM</p></td>
</tr>
<tr class="odd">
<td><p>Ken Myer</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
<tr class="even">
<td><p>Pilar Ackerman</p></td>
<td><p>7/2/2012 10:00 AM</p></td>
</tr>
</tbody>
</table>


Per ottenere un'indicazione più precisa del numero totale di utenti univoci che hanno organizzato conferenze, modificare l'intervallo di tempo, ad esempio esaminare i dati su base mensile anziché giornaliera.

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il rapporto riepilogativo conferenze consente di scegliere la modalità di raggruppamento dei dati. In questo caso le conferenze sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella seguente sono elencati i filtri applicabili al rapporto riepilogativo conferenze.

### Filtri del rapporto riepilogativo conferenze

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
<p>7/3/12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/12</p>
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
<p>Se le date di inizio e fine superano il numero massimo di valori consentiti per l'intervallo specificato, verrà visualizzato solo il numero massimo di valori a partire dalla data di inizio. Se ad esempio si seleziona l'intervallo giornaliero con data di inizio 7/7/2012 e data di fine 2/28/2012, verranno visualizzati i dati per i giorni da 8/7/2012 ore 12:00 AM a 9/7/2012 ore 12:00 AM (per un totale di 31 giorni).</p></td>
</tr>
</tbody>
</table>


## Metriche

La tabella seguente elenca le informazioni disponibili nel rapporto riepilogativo conferenze.

### Metriche del rapporto riepilogativo conferenze

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
<td><p><strong>Orario</strong></p>
<p><strong>Giornaliero</strong></p>
<p><strong>Settimanale</strong></p>
<p><strong>Mensile</strong></p></td>
<td><p>No</p></td>
<td><p>Indica l'intervallo di tempo selezionato sulla barra degli strumenti dei filtri. Ove applicabile, è possibile fare clic su un determinato intervallo di tempo per visualizzare informazioni dettagliate relative a tale intervallo. Se ad esempio si sta utilizzando l'intervallo giornaliero e si fa clic su 7/7/2012, verranno visualizzate le attività di registrazione degli utenti per tale data, suddivise per ore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale conferenze</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze eseguite, indipendentemente dal tipo di conferenza. Facendo clic su questo elemento viene visualizzato il rapporto attività conferenza per il periodo di tempo selezionato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale partecipanti</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di persone che hanno partecipato alle conferenze. Facendo clic su questo elemento viene visualizzato il rapporto attività conferenza per il periodo di tempo selezionato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Numero medio di partecipanti per conferenza</strong></p></td>
<td><p>No</p></td>
<td><p>Numero medio di persone che hanno preso parte a una specifica conferenza, determinato dividendo il numero totale di conferenze per il numero totale di partecipanti.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale conferenze audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze con audio o video.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale minuti di conferenza audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di minuti dedicati alle conferenze audio/video.</p>
<p>La metrica Totale minuti di conferenza audio/video riepiloga tutti i tipi di conferenza audio/video, tra cui: conferenze audio/video, conferenze di messaggistica istantanea, conferenze di condivisione applicazioni, conferenze dati e conferenze PSTN.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale minuti partecipante di conferenza audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di minuti partecipante dedicati alle conferenze audio/video. Si supponga, ad esempio, che un utente dedichi 5 minuti a una conferenza audio/video e che un secondo utente ne dedichi 3 nella stessa conferenza. Si ottiene così un totale di 8 minuti partecipante (5+3).</p></td>
</tr>
<tr class="even">
<td><p><strong>Media minuti di conferenza audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Numero medio di minuti per conferenza audio/video.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale organizzatori conferenza univoci</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di utenti che hanno organizzato almeno una conferenza. Gli utenti che hanno organizzato più conferenze vengono considerati come un organizzatore unico, come gli utenti che hanno organizzato una sola conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale messaggi conferenza</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di messaggi istantanei inviati durante le conferenze.</p></td>
</tr>
</tbody>
</table>

