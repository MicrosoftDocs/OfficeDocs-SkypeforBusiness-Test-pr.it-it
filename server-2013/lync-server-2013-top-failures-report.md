---
title: 'Lync Server 2013: Rapporto errori principali'
TOCTitle: Rapporto errori principali
ms:assetid: 438942e2-580a-4b67-9d42-f116111fb26a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558640(v=OCS.15)
ms:contentKeyID: 49300369
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto errori principali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel Rapporto errori principali vengono esaminati gli errori rilevati più di frequente con la relativa tendenza nel tempo. Gli errori sono basati su una combinazione delle due metriche seguenti:

  - **ID diagnostica** . Identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi relativi alle chiamate.

  - **Codice di risposta** . I codici di risposta vengono utilizzati nelle sessioni di comunicazione SIP per rispondere a richieste SIP. Si supponga ad esempio che Ken invii la richiesta INVITE a Pilar Ackerman (in altre parole si supponga che Ken Myer chiami Pilar Ackerman). Se Pilar risponde, il suo telefono invia il codice di risposta 200 (OK) per informare il telefono di Ken che lei ha risposto. Il Rapporto errori principali include solo i codici di risposta inviati in risposta a un errore di chiamata. Lync Server non tiene traccia di tutti i codici di risposta inviati nel corso di una telefonata.

Le informazioni vengono registrate nel rapporto non solo per il numero totale di sessioni in cui si è verificato un errore, ma anche per il numero totale di utenti che hanno subito l'errore.

## Accesso al Rapporto errori principali

È possibile accedere al Rapporto errori principali dalla home page Relazioni monitoraggio. Facendo clic sulla metrica Sessioni segnalate sarà possibile accedere al [Rapporto distribuzione errori in Lync Server 2013](lync-server-2013-failure-distribution-report.md).

## Utilizzo ottimale del Rapporto errori principali

Il Rapporto errori principali è insolito per un aspetto: consente di applicare un filtro che può includere fino a 5 ID diagnostica alla volta, laddove in genere può includere un solo elemento, ad esempio un indirizzo SIP utente alla volta. Per applicare un filtro in base a più ID diagnostica, è sufficiente immettere i singoli ID nella casella apposita separandoli tramite virgole. Se si vuole, è possibile lasciare uno spazio bianco dopo ogni virgola, come nell'esempio:

1011, 2412, 1033, 52116, 1008

Così facendo verranno visualizzate solo le chiamate non riuscite che hanno riportato almeno uno dei cinque ID diagnostica indicati.

Se si tiene il mouse posizionato su un codice di risposta, viene visualizzata una descrizione comando che ne spiega il significato. Se ad esempio si tiene il mouse posizionato sul codice di risposta 486, verrà visualizzato il messaggio seguente:

Non disponibile qui.

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Il Rapporto errori principali ad esempio consente di filtrare i dati restituiti in base a fattori come il tipo di attività, ovvero sessione peer-to-peer o di conferenza, oppure in base al codice di risposta SIP associato alla sessione in cui si è verificato l'errore. È inoltre possibile scegliere come raggruppare i dati. In questo caso, gli utilizzi vengono raggruppati per ora, giorno, settimana o mese.

Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto errori principali.

### Filtri del Rapporto errori principali

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
<td><p><strong>Tipo di attività</strong></p></td>
<td><p>Tipo di attività. Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Peer-to-peer</p></li>
<li><p>Conferenza</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Modalità</strong></p></td>
<td><p>L'unica opzione disponibile attualmente è <strong>[Tutto]</strong> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutti]</strong> per visualizzare dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
<tr class="even">
<td><p><strong>Categoria</strong></p></td>
<td><p>Tipo di errore. Selezionare uno dei tipi seguenti:</p>
<ul>
<li><p>Errore sia previsto che imprevisto</p></li>
<li><p>Errore imprevisto</p></li>
</ul>
<p>Per &quot;errore previsto&quot; si intende un errore che si prevede si verificherà. Se ad esempio un utente ha impostato il proprio stato su Non disturbare, è previsto che le chiamate effettuate per tale utente abbiano esito negativo. Per &quot;errore imprevisto&quot; si intende un errore che si verifica in un sistema considerato integro. Una chiamata ad esempio non dovrebbe interrompersi quando il chiamante viene messo in attesa. Se la chiamata si interrompe, l'evento verrà contrassegnato come errore imprevisto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Codice di risposta</strong></p></td>
<td><p>Codice di risposta SIP inviato quando si è verificato l'errore di conferenza. Immettere l'intero codice di risposta, ad esempio:</p>
<p>400</p></td>
</tr>
<tr class="even">
<td><p><strong>ID diagnostica</strong></p></td>
<td><p>Identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi. Le intestazioni di diagnostica sono facoltative (è possibile che in alcune sessioni SIP non siano incluse queste intestazioni) e gli ID diagnostica sono spesso indicati solo per sessioni in cui si sono verificati problemi di un determinato tipo.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente vengono elencate le informazioni fornite nel Rapporto errori principali.

### Metrica del Rapporto errori principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>Sì</p></td>
<td><p>Classificazione relativa basata sul numero di sessioni segnalate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni segnalate</strong></p></td>
<td><p>Sì</p></td>
<td><p>Numero totale di sessioni non riuscite in base all'ID diagnostica e al codice di risposta SIP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Utenti interessati</strong></p></td>
<td><p>Sì</p></td>
<td><p>Numero totale di utenti interessati dalla sessione non riuscita.</p></td>
</tr>
<tr class="even">
<td><p><strong>Informazioni sull'errore</strong></p></td>
<td><p>No</p></td>
<td><p>Informazioni dettagliate sull'errore, tra cui l'ID diagnostica, il codice di risposta SIP e la descrizione del motivo per cui la sessione ha avuto esito negativo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tendenza passato</strong></p></td>
<td><p>No</p></td>
<td><p>Rappresentazione grafica delle sessioni non riuscite nel tempo.</p></td>
</tr>
</tbody>
</table>

