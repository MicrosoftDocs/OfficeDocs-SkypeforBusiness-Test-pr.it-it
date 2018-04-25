---
title: Metodologia per il controllo della qualità delle chiamate Lync
TOCTitle: 'Poster: Metodologia per il controllo della qualità delle chiamate Lync'
ms:assetid: a069f4e5-4f80-4f0f-8657-2e07276b6b41
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn593600(v=OCS.15)
ms:contentKeyID: 61084845
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Metodologia per il controllo della qualità delle chiamate Lync

 

_**Ultima modifica dell'argomento:** 2014-03-19_

Questo articolo contiene informazioni a corredo del poster [Metodologia per il controllo della qualità delle chiamate Lync](http://go.microsoft.com/fwlink/?linkid=391841), che è possibile scaricare dall'Area download.

![Poster in cui viene descritto il processo CQM](images/Dn594589.d239e04a-1c3b-4f0e-93af-88b85198615a(OCS.15).jpg "Poster in cui viene descritto il processo CQM")

È possibile utilizzare il poster per ottenere informazioni sulla metodologia per il controllo della qualità delle chiamate (CQM, Call Quality Methodology) per Lync 2013 e 2010, che consente di individuare e risolvere i problemi che influiscono sulla qualità delle chiamate e sull'esperienza utente per le implementazioni di Lync che includono funzionalità VoIP aziendali. CQM è un nuovo framework per la risoluzione dei problemi e la gestione dei servizi che consente di concentrare l'attenzione sulle soluzioni per migliorare i servizi VoIP aziendali in Lync. In questo articolo vengono fornite ulteriori informazioni su CQM e sui tipi di server e soluzioni sottoposti a monitoraggio. Viene inoltre indicato come procedere con i dati di telemetria raccolti.

In caso di domande relative alle modalità d'uso della metodologia per il controllo della qualità delle chiamate, è possibile inviarle a cqmfeedback@microsoft.com.

Nel poster vengono fornite informazioni sulle seguenti aree:

  - Cos'è Lync CQM?

  - Definire le priorità: esecuzione di query relative alle tendenze

  - PCD

  - Spazio gestito/non gestito

  - Server Plant Road

  - Last Mile Road

  - End Points Road

  - Service Management

  - Regole del gioco da tavolo

## Cos'è Lync CQM?

CQM è un nuovo framework per la risoluzione dei problemi e la gestione dei servizi che consente di concentrare l'attenzione sulle soluzioni per migliorare i servizi VoiP aziendali in Lync. L'uso di CQM consente di garantire una migliore qualità delle chiamate e una maggior soddisfazione degli utenti in relazione ai servizi VoIP aziendali. Per ulteriori informazioni su CQM, vedere la [Guida ai servizi di rete di Lync Server](http://go.microsoft.com/fwlink/p/?linkid=390677). Il presente articolo e il poster costituiscono un riepilogo del contenuto di tale guida.

In CQM la procedura di risoluzione dei problemi del sistema viene suddivisa in tre percorsi o "Road", ovvero Server Plant Road, che esamina i server e i collegamenti tra loro, End Points Road, che esamina i dispositivi utente e i media utilizzati per effettuare chiamate, e infine Last Mile Road, che si occupa dell'integrazione delle chiamate PSTN tradizionali.

Ogni percorso è suddiviso in diversi segmenti correlati a un'area o a un argomento specifico. Per ogni segmento vengono inoltre definiti i livelli di qualità accettabili e le azioni da intraprendere per raggiungere il livello di qualità indicato. Viene inoltre predisposto un piano di gestione dei servizi per garantire il livello di qualità prima di passare all'argomento successivo.

Nel poster Lync CQM è raffigurato come una tavola da gioco per tre giocatori, ciascuno dei quali prende uno dei tre percorsi disponibili. Le carte incluse con il download vengono utilizzate per simulare i fattori che possono incidere sulla qualità delle chiamate che si intende ottenere. Lungo i tre percorsi sono previsti suggerimenti e consigli sui valori target e su come raggiungerli, oltre a linee guida per definire le priorità e individuare il percorso da intraprendere per primo nelle applicazioni effettive. Nel gioco i tre percorsi procedono in parallelo.

Come funziona CQM con le versioni precedenti di Lync? CQM rappresenta una novità di Lync 2013, tuttavia la maggior parte delle funzionalità può essere adattata per l'uso con Lync 2010. È anche possibile che CQM funzioni con Microsoft Office Communicator, ma tale soluzione non è stata testata, pertanto non è supportata.

In caso di domande relative alle modalità d'uso della metodologia per il controllo della qualità delle chiamate, è possibile inviarle a cqmfeedback@microsoft.com.

## Definire le priorità: esecuzione di query relative alle tendenze

Il primo passaggio della metodologia CQM consiste nell'eseguire ognuna delle query relative alle tendenze per due settimane e quindi analizzare i risultati. Assegnare priorità all'azione correttiva in base a chi utilizza maggiormente il flusso, al rapporto di flusso più insufficiente e alle aree gestite (ovvero quelle su cui si esercita il controllo). Se le query su AV MCU (Audio/Video Multi-point Control Unit) o sui Mediation Server restituiscono risultati insufficienti, iniziare con il percorso rosso, ovvero quello Server Plant. Se le query sulle connessioni cablate o wireless restituiscono risultati insufficienti, iniziare con il percorso blu, ovvero Last Mile Road. Se infine le query su VPN o server esterni restituiscono risultati insufficienti, iniziare con il percorso verde, ovvero End Points Road.

Dopo aver scelto un percorso da cui iniziare, definire un valore target per ciascuna area (Assert), operare in modo da raggiungere il valore target (Achieve) e quindi implementare procedure per garantire nel tempo i valori target (Maintain). È anche possibile utilizzare il poster come gioco per assimilare meglio i principi della metodologia CQM.

## PCD

Lo strumento PreCall Diagnostics (PCD) consente di identificare e diagnosticare i problemi nella rete perimetrale (il database QoE non raccoglie informazioni sulla rete perimetrale), nonché di risolvere i problemi relativi alle connessioni nel percorso Last Mile Road. Lo strumento è disponibile sia come app di Windows 8 che come app di Windows Desktop all'indirizzo http://apps.microsoft.com/windows/en-us/app/lync-2013-precall-diagnostics/9607fe33-2b51-403d-9615-c23f248e7c88.

## Spazio gestito/non gestito

L'infrastruttura di rete e la distribuzione di Lync Server possono in genere essere suddivisi in spazi gestiti e non gestiti. Lo spazio gestito include l'intera rete cablata e l'infrastruttura server. Lo spazio non gestito è costituito dall'infrastruttura wireless e dall'infrastruttura della rete esterna.

Questa distinzione contribuisce a una maggiore chiarezza dei dati e consente all'organizzazione di concentrare l'attenzione sui carichi di lavoro che avranno un impatto misurabile sulla qualità audio e video degli utenti. L'aspettativa degli utenti in relazione alla qualità varia a seconda che la chiamata venga effettuata tramite un'infrastruttura di cui si è proprietari (gestita) o tramite un'infrastruttura parzialmente controllata da altre entità (non gestita). Non è quindi pensabile che l'esperienza con Lync Server degli utenti wireless debba avvenire esclusivamente con dispositivi mobili.

Per migliorare la qualità dell'audio nello spazio non gestito è necessario garantire una qualità elevato nello spazio gestito. A seconda dell'organizzazione, la connessione wireless (Wi-Fi) può essere considerata uno spazio gestito o non gestito. Le tecniche e le soluzioni per ottenere un ambiente ottimale variano in funzione degli spazi.

## Server Plant Road

Il segmento 1 del percorso Server Plant Road è dedicato ai server effettivi presenti nell'implementazione di Lync. Raccogliere i dati sugli indicatori KHI relativi al server e al suo ruolo nell'implementazione, quindi analizzare i risultati. Se è necessario intervenire, correggere gli eventuali problemi rilevati. Per ulteriori informazioni su questo argomento, vedere l'articolo [Indicatori chiave per l'integrità](lync-server-2013-poster-key-health-indicators.md) a corredo del poster sugli indicatori KHI.

Il segmento successivo è dedicato ai flussi multimediali tra il server AV MCU e il Mediation Server. Per iniziare, stabilire i valori target per le soglie di flusso insufficienti. I flussi insufficienti corrispondono in genere a PacketLossRate \> .01 o PacketLossRateMax \> .05. Un altro valore target da considerare è PoorStreamsRatio \< 2%. A questo punto, utilizzare query dettagliate per individuare le coppie di server AVMCU e Mediation Server con flussi insufficienti, analizzare la causa del problema, esaminare i componenti di rete nei percorsi dei flussi insufficienti, risolvere i problemi e definire la configurazione ottimale o "aurea" per i componenti di rete. Per mantenere nel tempo i risultati raggiunti, implementare processi e strumenti per gestire la nuova configurazione e segnalare nuove aree problematiche.

A questo punto esaminare i flussi multimediali tra Mediation Server e il gateway PSTN (Public Switched Telephone Network). Per iniziare, stabilire i valori target per le soglie di flusso insufficienti. I flussi insufficienti corrispondono in genere a PacketLossRate \> .01 o PacketLossRateMax \> .05. Un altro valore target da considerare è PoorStreamsRatio \< 2%. Utilizzare quindi query dettagliate per individuare le coppie di Mediation Server e gateway con flussi insufficienti, analizzare la causa del problema, esaminare i componenti di rete nei percorsi dei flussi insufficienti, risolvere i problemi e definire la configurazione ottimale o "aurea" per i componenti di rete. Per mantenere nel tempo i risultati raggiunti, implementare processi e strumenti per gestire la nuova configurazione e segnalare nuove aree problematiche.

Esaminare infine le metriche relative allo stato di integrità del gateway PSTN. Identificare le statistiche dello stato di integrità e definire appositi valori target. In questo documento non vengono fornite indicazioni specifiche in quanto è possibile utilizzare il numero di gateway desiderato. Una volta definiti i valori target, risolvere i problemi in modo da raggiungere il valore target. Nel corso di questo processo è probabile che venga definita la configurazione ottimale o "aurea" per il gateway. Per mantenere nel tempo i risultati raggiunti, implementare processi e strumenti per gestire la nuova configurazione e segnalare nuove aree problematiche. Tenere presente che gli aggiornamenti firmware e software possono alterare la configurazione o comportare l'adeguamento della configurazione ottimale, pertanto prestare particolare attenzione con queste attività.

## Last Mile Road

Tra i due modi con cui i client si connettono alla rete, la connessione cablata è quella che in genere garantisce la migliore qualità, di conseguenza si partirà da questa per i problemi di questo percorso. Utilizzare la query della connessione cablata CQM (LastMile\_0\_Wired) e i dati relativi al rapporto tra flussi insufficienti da essa forniti. È consigliabile definire un valore target PoorStreamsRatio \< 5% per i siti con più di 300 flussi. Per ottenere i valori target, risolvere i problemi relativi alle subnet a partire dalla peggiore fino alla migliore e implementare QoS.

Dopo aver ottimizzato la qualità delle connessioni cablate, risulta più semplice migliorare quella delle connessioni wireless dal momento che l'infrastruttura wireless si basa su quella cablata in ogni posizione. I problemi di flussi wireless insufficienti in un sito in cui la qualità della rete cablata è adeguata dipendono dagli specifici componenti della rete wireless. La query della rete wireless CQM (LastMile\_1\_Wireless) opera su un intervallo di date e restituisce tutti i flussi wireless interni all'ambiente in uso provenienti da client Lync e indirizzati a Conferencing Server o Mediation Server. È consigliabile definire un valore target PoorStreamsRatio \< 5% per i siti con più di 300 flussi. Per ottenere i valori target, risolvere i problemi relativi alle subnet a partire dalla peggiore fino alla migliore e implementare QoS.

## End Points Road

Per le indagini nel percorso End Points Road iniziare con le cuffie e altri dispositivi che in genere garantiscono una qualità accettabile quando vengono utilizzati con Lync. È consigliabile un valore target AvgSendListen MOS \> 3.6 per le implementazioni con oltre 100 flussi. Per ottenere il valore target, identificare i dispositivi problematici e correggerli o sostituirli.

Esaminare a questo punto il dispositivo o il PC che elabora l'audio per le chiamate degli utenti finali. La metrica per la qualità target consigliata è AudioMic GlitchRate \> 1. Quando si identificano configurazioni di sistema ottimali per i sistemi utente, definire una configurazione "aurea" del PC, includendo le versioni dei driver.

Esaminare ora il percorso di rete di un flusso audio proveniente da un sistema endpoint di Lync, che può causare una qualità audio insufficiente. Se per la trasmissione dell'audio viene utilizzata una connessione VPN, potrebbero verificarsi problemi di latenza. Se un client Lync interno non è in grado di stabilire un flusso multimediale diretto con un altro client Lync interno per una chiamata tra due interlocutori o peer-to-peer, eseguirà il fallback a un percorso instradato tramite un server perimetrale Lync, causando anche in questo caso problemi di latenza, oltre a comportare possibili rischi di perdita di dati e instabilità. È consigliabile definire una metrica di qualità pari a 0% per flussi multimediali tramite VPN. Dopo aver risolto i problemi e aver ottenuto il valore target impostato, identificare le subnet problematiche ed esaminare le regole firewall, gli shaper di pacchetti e la configurazione di altri componenti di rete pertinenti.

Con i pacchetti IP è possibile utilizzare il protocollo TCP (Transmission Control Protocol) o UDP (User Datagram Protocol). Il protocollo TCP è per i flussi di dati, mentre UDP non dipende dalla connessione ed è più efficiente per gli elementi multimediali poiché i meccanismi di ripristino TCP non riescono a gestire tali elementi in tempo reale. In Lync viene sempre preferito UDP, tuttavia nel caso in cui non sia possibile stabilire una sessione UDP, viene effettuato il passaggio a TCP. La qualità delle sessioni multimediali tramite TCP è inferiore rispetto a quella ottenuta con TCP. Dopo aver risolto i problemi e aver ottenuto il valore target impostato, identificare le subnet problematiche ed esaminare le regole firewall, gli shaper di pacchetti e la configurazione di altri componenti di rete pertinenti.

## Service Management

Service Management costituisce lo stato finale di CQM e la destinazione dei tre percorsi. Per garantire livelli elevati di qualità delle chiamate, monitorare le aree seguenti:

1.  **Utenti:** nelle attività di correzione si dovrebbe notare un miglioramento nel livello di soddisfazione degli utenti. È possibile misurare questo fattore in base al numero di ticket aperti o ad altri meccanismi per ottenere commenti e suggerimenti. È anche possibile pubblicare le metriche relative alla qualità.

2.  **Processo:** definire processi giornalieri, settimanali e mensili per rendere operativa la metodologia CQM. la frequenza del monitoraggio sarà maggiore all'inizio, ad esempio giornaliera, quando si apportano le correzioni e diminuirà diventando mensile via via che il sistema diventa più stabile.

3.  **Strumenti:** identificare gli strumenti per la misurazione e la correzione. Può essere utile automatizzare l'esecuzione delle query CQM per supportare i processi. Per la correzione potrebbero essere necessari ulteriori strumenti, ad esempio per applicare configurazioni standardizzate per elementi di rete oppure per risolvere i problemi relativi alle perdite in flussi insufficienti.

## Regole del gioco da tavolo

È possibile utilizzare questo poster come riferimento di un'implementazione della metodologia CQM oppure come gioco per mettere in pratica i concetti. Per giocare, sono necessari un dado a sei facce e le carte fornite. È disponibile una versione scaricabile delle carte da stampare su biglietti da visita in formato standard Avery 5871.

Il gioco è per tre giocatori. I percorsi disponibili per ottenere la qualità desiderata e raggiungere lo stato Service Management per il centro sono: Server Plant, End Point e Last Mile Road. Per ogni percorso sono presenti delle soste che consentono di definire valori target di qualità (Assert), raggiungere obiettivi (Achieve) e garantire lo stato di un aspetto del sistema (Maintain). Sistemare le carte nell'area indicata in precedenza e prendere cinque carte. Esaminare le carte prese e metterle nell'apposito segmento della tavola da gioco. Ogni giocatore si sposta tra le carte lungo il percorso passo dopo passo, definendo valori target di qualità, ottenendo tali valori target e garantendo i livelli di servizio. Il gioco finisce quando tutti i giocatori raggiungono lo stato Service Management centrale. Regole più dettagliate sono incluse con il download delle carte da gioco.

Per definire un valore target di qualità **(Assert)**, esaminare i parametri applicabili a tale valore e dire ad alta voce cosa si intende o meno accettare. Sono disponibili i punti consigliati per iniziare, ma la scelta spetta al giocatore. L'unica eccezione è costituita dai dati KHI, in cui è necessario utilizzare i dati definiti da Microsoft. Vedere il poster sugli indicatori KHI a corredo.

Per ottenere i valori target **(Achieve)** nel gioco, utilizzare le carte fornite anziché i dati KHI e le query di sistema. Se all'inizio del gioco non è stata presa una carta correlata a un dato aspetto, è possibile andare avanti, Se invece si dispone di una certa carta, lanciare il dato. Se il valore del dado è inferiore al numero indicato sulla carta, si vince. Se invece il valore del dado è uguale o superiore al numero indicato, è necessario prendere un'altra carta dal mazzo. Se la carta indica che due o più giocatori devono lanciare il dado, questi dovranno tutti effettuare questa operazione.

Per passare alla fase **(Maintain)** nel gioco, pronunciare ad alta voce il nome del piano di Service Management relativo a tale aspetto dell'ambiente di Lync.

## Vedere anche

#### Ulteriori risorse

[Guida ai servizi di rete di Lync Server](http://go.microsoft.com/fwlink/p/?linkid=390677)  
[Indicatori chiave per l'integrità come base per garantire l'integrità dei server di Lync](http://go.microsoft.com/fwlink/?linkid=391838)  
[Metodologia per il controllo della qualità delle chiamate Lync](http://go.microsoft.com/fwlink/?linkid=391841)

