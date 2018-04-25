---
title: Indicatori chiave per l'integrità
TOCTitle: "Poster: Indicatori chiave per l'integrità"
ms:assetid: 8367dccf-adaa-4a0b-a4ed-bc9570cc5e24
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn593599(v=OCS.15)
ms:contentKeyID: 61084844
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Indicatori chiave per l'integrità

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Questo articolo contiene informazioni a corredo del poster [Indicatori chiave per l'integrità come base per garantire l'integrità dei server di Lync](http://go.microsoft.com/fwlink/?linkid=391838), che è possibile scaricare dall'Area download.

![Poster relativo alla risoluzione dei problemi con i dati KHI](images/Dn594589.b6fe82bd-d70f-4c1f-a812-b615ac5fa7d7(OCS.15).jpg "Poster relativo alla risoluzione dei problemi con i dati KHI")

È possibile utilizzare questo poster per ottenere informazioni sugli indicatori chiave per l'integrità (KHI, Key Health Indicators), ovvero contatori delle prestazioni che prevedono soglie grazie alle quali individuare possibili problemi di esperienza utente. La raccolta dei dati degli indicatori chiave per l'integrità costituisce in genere il primo passaggio per implementare la metodologia per il controllo della qualità delle chiamate, il cui scopo è di garantire un'esperienza audio di qualità per gli utenti di Lync.

In caso di domande relative alle modalità d'uso della metodologia per il controllo della qualità delle chiamate, è possibile inviarle a cqmfeedback@microsoft.com.

Nel poster vengono fornite informazioni sulle seguenti aree:

  - Indicatori chiave per l'integrità

  - Raccolta dei dati degli indicatori chiave per l'integrità

  - Flusso di risoluzione dei problemi per tutti i ruoli server

  - Glossario

  - Server Front End

  - Server SQL di back-end

  - Mediation Server

  - Server perimetrali

## Indicatori chiave per l'integrità

Gli indicatori chiave per l'integrità sono contatori delle prestazioni che prevedono soglie grazie alle quali individuare possibili problemi di esperienza utente. La raccolta dei dati degli indicatori chiave per l'integrità costituisce in genere il primo passaggio per implementare la metodologia per il controllo della qualità delle chiamate, il cui scopo è di garantire un'esperienza audio di qualità per gli utenti di Lync.

Gli indicatori chiave per l'integrità vengono utilizzati in aggiunta alle soluzioni di monitoraggio standard di Lync (es. System Center Operations Manager, Transazioni sintetiche, Monitoring Server) e non in sostituzioni a tali soluzioni.

È possibile raccogliere i contatori delle prestazioni degli indicatori chiave per l'integrità e compilare il foglio di calcolo fornito con la Guida ai servizi di rete per ottenere una scorecard che consente di determinare lo stato di integrità del server di una distribuzione di Lync. Una volta compilato, il foglio offre indicazioni utili per il ripristino dell'ambiente e fornisce ulteriori dettagli ad altre parti interessate. È consigliabile valutare gli indicatori chiave per l'integrità su base mensile e incorporarli nei processi operativi in corso di qualsiasi distribuzione.

Per un elenco completo degli indicatori chiave per l'integrità e per ottenere i fogli di calcolo correlati, scaricare la [Guida ai servizi di rete di Lync Server](http://go.microsoft.com/fwlink/p/?linkid=390677).

## Raccolta dei dati degli indicatori chiave per l'integrità

1.  Eseguire lo script degli indicatori chiave per l'integrità incluso con la Guida ai servizi di rete di Lync Server in ogni server Lync. In questo modo all'interno di Performance Monitor verrà creato un agente di raccolta dati al quale verrà assegnato il nome KHI. Per impostazione predefinita, il polling dei dati verrà eseguito ogni 15 secondi.

2.  Prima dell'inizio della giornata lavorativa in azienda, passare a ogni server Lync e avviare l'agente di raccolta dati KHI.

3.  Alla fine della giornata arrestare l'agente di raccolta dati KHI e copiare i dati in una posizione centralizzata.

4.  Dopo aver utilizzato Performance Monitor per compilare il foglio di calcolo KHI incluso con la Guida ai servizi di rete di Lync Server, confrontare i risultati con i valori target consigliati.

## Flusso di risoluzione dei problemi per tutti i ruoli server

Per ogni server dell'implementazione di Lync iniziare a verificare lo stato di integrità dei componenti del server e assicurarsi che le prestazioni del sistema siano pari o superiori al livello desiderato. Solo dopo aver effettuato questa verifica esaminare gli indicatori correlati al ruolo del server nell'implementazione globale di Lync.

Per iniziare, raccogliere i dati relativi alle prestazioni degli indicatori chiave per l'integrità per tutti i server. Per ognuno dei ruoli del sistema (su cui verranno fornite ulteriori informazioni più avanti in questo documento) stabilire se i componenti di base del sistema sono conformi ai valori target consigliati. In caso contrario, eseguire la procedura di risoluzione dei problemi per le prestazioni del sistema. Raccogliere quindi nuovamente i dati sugli indicatori chiave per le prestazioni e verificare lo stato di integrità del sistema prima di esaminare le metriche specifiche del ruolo del server nell'implementazione di Lync. Lo stato di integrità dei componenti per tutti i ruoli viene definito nel modo seguente:

  - Utilizzo della CPU \< 80%

  - Tempo medio per la scrittura sul disco \< 10 ms

  - Tempo medio per la lettura dal disco \< 10 ms

  - Memoria disponibile \>20% del totale di sistema in MB

  - Lunghezza della coda di rete \< 2

  - Pacchetti eliminati (ingresso/uscita) = 0

## Glossario

Di seguito sono elencati i termini e gli acronimi utilizzati nel poster:

AS MCU = Unità di controllo multipoint per la condivisione di applicazioni

AV MCU = MCU audio/video

IM MCU = MCU per la messaggistica istantanea

UCWA = API Web Unified Communications

AV Edge = Attraversamento di audio/video tramite server perimetrale

AV Auth = Autenticazione audio/video

SIP Stack = Contiene l'implementazione SIP di base di Lync

Data Proxy = Utilizzato per le conferenze telefoniche con server perimetrale

LySS = Servizio di archiviazione di Lync

## Server Front End

I seguenti valori target degli indicatori chiave per l'integrità sono specifici dei server Front End, oltre a quelli dei componenti di base:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area funzionale</th>
<th>Metriche target</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MCU AS/AV/IM</p></td>
<td><p>Stato integrità MCU &lt;2</p></td>
</tr>
<tr class="even">
<td><p>Componenti Web</p></td>
<td><p>Timeout AD espansione lista di distribuzione &lt;0</p>
<p>Errori ABWQ = 0</p>
<p>Errori LIS = 0</p>
<p>Errori di autenticazione &lt; 1/sec</p>
<p>Richieste di ASP.NET 4 rifiutate = 0</p></td>
</tr>
<tr class="odd">
<td><p>Stack SIP</p></td>
<td><p>Tempo medio di elaborazione messaggi in arrivo &lt; 1 sec</p>
<p>Risposte in arrivo non elaborate &lt; 1/sec Richieste in arrivo non elaborate &lt; 1/sec</p>
<p>Latenza coda &lt; 100 ms</p>
<p>Latenza Sproc &lt; 100 ms</p>
<p>Richieste limitate = 0</p>
<p>Errori di autenticazione &lt; 1/sec</p>
<p>Timeout messaggi in arrivo &lt; 2</p>
<p>Tempo medio di conservazione messaggi in arrivo &lt; 1 sec</p>
<p>Connessioni controllate da flusso &lt; 2</p>
<p>Ritardo medio coda in uscita &lt; 2 sec</p></td>
</tr>
<tr class="even">
<td><p>LySS</p></td>
<td><p>% di spazio utilizzato dal database del servizio di archiviazione &lt; 80</p>
<p>N. di errori di replica della replica = 0</p>
<p>N. di eventi di perdita dati = 0</p></td>
</tr>
<tr class="odd">
<td><p>SQL</p></td>
<td><p>Durata prevista pagina &gt; 300 Sec.</p>
<p>Richieste batch/sec &lt; 2500</p></td>
</tr>
</tbody>
</table>


## Server SQL di back-end

I seguenti valori target degli indicatori chiave per l'integrità sono specifici dei server SQL, oltre a quelli dei componenti di base:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area funzionale</th>
<th>Metriche target</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SQL</p></td>
<td><p>Durata prevista pagina &gt; 300 Sec.</p>
<p>Richieste batch/sec &lt; 2500</p></td>
</tr>
</tbody>
</table>


## Mediation Server

I seguenti valori target degli indicatori chiave per l'integrità sono specifici dei Mediation Server, oltre a quelli dei componenti di base:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area funzionale</th>
<th>Metriche target</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servizio Mediation Server</p></td>
<td><p>Indice di errore caricamento chiamata = 0</p>
<p>Chiamate non riuscite a causa del proxy &lt;10</p>
<p>Chiamate non riuscite a causa del gateway &lt;10</p>
<p>Chiamate (ingresso o uscita) rifiutate = 0</p>
<p>Candidati server multimediali mancanti = 0</p>
<p>Errori di verifica connettività server multimediali = 0</p></td>
</tr>
</tbody>
</table>


## Server perimetrali

I seguenti valori target degli indicatori chiave per l'integrità sono specifici dei server perimetrali, oltre a quelli dei componenti di base:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area funzionale</th>
<th>Metriche target</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticazione A/V</p></td>
<td><p>Richieste errate &lt; 20/sec</p></td>
</tr>
<tr class="even">
<td><p>A/V Edge</p></td>
<td><p>Errori di autenticazione &lt;20/sec</p>
<p>Errori di allocazione &lt;20/sec</p>
<p>Pacchetti non elaborati &lt;300/sec</p></td>
</tr>
<tr class="odd">
<td><p>Proxy di dati</p></td>
<td><p>Connessioni al server con limitazioni delle richieste &lt; 3</p>
<p>Sistema con limitazione delle richieste &lt;1</p></td>
</tr>
<tr class="even">
<td><p>Stack SIP</p></td>
<td><p>Connessioni superiori al limite non elaborate &lt; 1</p>
<p>Timeout invii &lt;10</p>
<p>Connessioni controllate da flusso &lt;100</p>
<p>Richieste in arrivo non elaborate &lt; 1/sec</p>
<p>Tempo medio di elaborazione messaggi &lt; 3 sec</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Guida ai servizi di rete di Lync Server](http://go.microsoft.com/fwlink/p/?linkid=390677)  
[Indicatori chiave per l'integrità come base per garantire l'integrità dei server di Lync](http://go.microsoft.com/fwlink/?linkid=391838)  
[Metodologia per il controllo della qualità delle chiamate Lync](http://go.microsoft.com/fwlink/?linkid=391841)

