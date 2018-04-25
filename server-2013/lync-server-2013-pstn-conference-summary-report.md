---
title: 'Lync Server 2013: Rapporto riepilogativo conferenze PSTN'
TOCTitle: Rapporto riepilogativo conferenze PSTN
ms:assetid: 8e2f0862-4dfa-4c2b-bf8d-ad71419f15d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615014(v=OCS.15)
ms:contentKeyID: 49301280
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto riepilogativo conferenze PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Lync Server 2013, una conferenza PSTN è una qualsiasi conferenza in cui almeno un partecipante accede alla parte audio mediante un telefono di rete PSTN (Public Switched Telephone Network). Un telefono PSTN è una "linea di telefonia fissa", un telefono cellulare o qualsiasi altro telefono che non si avvale del VoIP. Sebbene vi si faccia riferimento come conferenze PSTN nei rapporti di monitoraggio, queste conferenze sono più comunemente note come conferenze telefoniche con accesso esterno.

Il Rapporto riepilogativo conferenze PSTN offre informazioni su tutte le conferenze PSTN tenutesi nell'organizzazione, ovvero tutte le conferenze con almeno un utente in accesso esterno. Il rapporto include informazioni sul numero totale di conferenze PSTN, il numero totale di utenti che vi hanno preso parte e (probabilmente il dato più importante) il numero totale di utenti con accesso esterno (metrica Totale partecipanti PSTN).

## Accesso al Rapporto riepilogativo conferenze PSTN

Il Rapporto riepilogativo conferenze PSTN è accessibile solo dalla home page Rapporti di monitoraggio. Questo rapporto non è collegato ad altri rapporti. Tenere presente che non è possibile recuperare informazioni dettagliate sulle chiamate per una conferenza PSTN, in parte perché i singoli endpoint sono responsabili dell'invio di tali informazioni. I telefoni PSTN non sono in grado di registrare o inviare informazioni dettagliate sulle chiamate.

## Uso ottimale del Rapporto riepilogativo conferenze PSTN

Per determinare la percentuale di tutte le conferenze che includono utenti con accesso esterno, confrontare il valore della metrica Totale conferenze PSTN con la metrica Totale conferenze disponibile nel [Rapporto riepilogativo conferenze in Lync Server 2013](lync-server-2013-conference-summary-report.md).

Se non è disponibile il dato previsto sul numero di conferenze PSTN, tenere presente che la capacità di organizzare una conferenza che consenta gli utenti con accesso esterno dipende dai criteri di conferenza assegnati a un utente: se a un numero estremamente esiguo di utenti è consentito tenere conferenze PSTN di conseguenza vi saranno poche conferenze PSTN. È possibile verificare rapidamente gli eventuali criteri di conferenza che consentono agli utenti di pianificare conferenze PSTN eseguendo il comando seguente dalla shell di gestione di Lync Server:

    Get-CsConferencingPolicy | Select-Object Identity, EnableDialInConferencing

Verranno restituiti dati simili ai seguenti:

    Identity                                EnableDialInConferencing
    --------                                ------------------------
    Global                                                      True
    site:Redmond                                               False
    site:Dublin                                                False
    Tag:RedmondDialInUsers                                      True
    Tag:DublinDialInUsers                                       True

Verranno restituiti dati simili ai seguenti:

## Filtri

I filtri consentono di ottenere un set di dati più specifico o di visualizzare in modo diverso i dati restituiti. Ad esempio, il rapporto riepilogativo conferenze PSTN consente di scegliere la modalità di raggruppamento dei dati. In questo caso le conferenze sono raggruppabili per ora, giorno, settimana o mese.

Nella tabella seguente sono elencati i filtri applicabili al Rapporto riepilogativo conferenze PSTN.

### Filtri del Rapporto riepilogativo conferenze PSTN

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
</tbody>
</table>


## Metriche

La tabella seguente elenca le informazioni disponibili nel Rapporto riepilogativo conferenze PSTN.

### Metriche del Rapporto riepilogativo conferenze PSTN

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
<td><p>Indica l'intervallo di tempo selezionato. Ove applicabile, è possibile fare clic su un determinato intervallo di tempo per visualizzare informazioni dettagliate relative a tale intervallo. Se ad esempio si sta utilizzando l'intervallo giornaliero e si fa clic su 7/7/2012, verranno visualizzate le attività di registrazione degli utenti per tale data, suddivise per ore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale conferenze PSTN</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze telefoniche con accesso esterno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale partecipanti</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di persone che hanno partecipato a conferenze telefoniche con accesso esterno.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale minuti di conferenza audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Durata totale delle conferenze audio/video.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale minuti partecipante di conferenza audio/video</strong></p></td>
<td><p>No</p></td>
<td><p>Totale minuti di partecipazione a conferenze audio/video. Ad esempio, se un partecipante ha trascorso cinque minuti in una conferenza audio/video e un altro partecipante ha trascorso tre minuti nella stessa conferenza, il totale sarà otto minuti.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale partecipanti PSTN</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di utenti che si sono connessi a conferenze telefoniche con accesso esterno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale minuti partecipante PSTN</strong></p></td>
<td><p>No</p></td>
<td><p>Tempo totale trascorso in conferenza da utenti connessi tramite chiamata in ingresso. Ad esempio, se un partecipante connesso tramite chiamata in ingresso ha trascorso cinque minuti in una conferenza e un altro partecipante ha trascorso tre minuti nella stessa conferenza, il totale sarà otto minuti.</p></td>
</tr>
<tr class="even">
<td><p><strong>Organizzatori conferenza univoci</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di utenti che hanno organizzato almeno una conferenza telefonica con accesso esterno. Gli utenti che hanno organizzato più conferenze vengono considerati come un organizzatore unico, come gli utenti che hanno organizzato una sola conferenza.</p></td>
</tr>
</tbody>
</table>

