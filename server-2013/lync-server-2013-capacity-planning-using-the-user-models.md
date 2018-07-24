---
title: 'Lync Server 2013: Pianificazione della capacità tramite modelli utente'
TOCTitle: Pianificazione della capacità tramite modelli utente
ms:assetid: 902ab23e-94d6-482a-9d6e-c0b28dc3e03d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615015(v=OCS.15)
ms:contentKeyID: 49887655
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della capacità per Lync Server 2013 tramite modelli utente

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione sono disponibili informazioni sul numero di server necessari in un sito per il numero di utenti di tale sito, in base all'uso descritto in [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).

## Piattaforma hardware testata

Tutti i risultati in termini di prestazioni e le indicazioni sulla distribuzione illustrati in questa sezione si basano sui test effettuati su server provvisti dell'hardware descritto nella tabella seguente. È consigliabile usare hardware analogo. Se si usa hardware meno potente, potrebbero verificarsi problemi di funzionalità o riduzioni delle prestazioni. Tenere presente che le indicazioni sull'hardware sono di ordine superiore rispetto alle versioni precedenti di Lync Server.

### Hardware usato per i test delle prestazioni

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Scelta consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>Processore doppio a 64 bit, hex-core, 2,26 GHz o superiore</p>
<p>I processori Intel Itanium non sono supportati per i ruoli del server di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>32 gigabyte (GB)</p></td>
</tr>
<tr class="odd">
<td><p>Disco</p></td>
<td><ul><li><p>8 o più unità disco rigido a 10.000 rpm con almeno 72 GB di spazio libero.</p>
<p>Due dei dischi dovrebbero utilizzare RAID 1 e sei dovrebbero utilizzare RAID 10.</p>
<p>-OPPURE-</p></li><li><p>Unità SSD (Solid State Drive) con prestazioni simili a otto unità disco meccanico da 10.000 RPM.</p></li></ul></td>
</tr>
<tr class="even">
<td><p>Rete</p></td>
<td><ul><li><p>Una scheda di rete dual port, 1 Gbps o superiore (due consigliate, da associare a un singolo indirizzo MAC e a un singolo indirizzo IP)</p></li></ul></td>
</tr>
</tbody>
</table>


## Riepilogo dei risultati

Nella tabella seguente sono riepilogate queste indicazioni.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo del server</th>
<th>Numero massimo di utenti supportati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>pool Front End con dodici Front End Server e un server back-end o una coppia di server back-end con mirroring.</p></td>
<td><p>80.000 utenti univoci connessi simultaneamente, più il 50% con più punti di presenza (MPOP) che rappresentino le istanze non mobili, più il 40% di utenti abilitati per i servizi per dispositivi mobili per un totale di 152.000 endpoint.</p></td>
</tr>
<tr class="even">
<td><p>A/V Conferencing</p></td>
<td><p>Il servizio A/V Conferencing fornito da un pool Front End supporta le conferenze del pool presupponendo un numero massimo di utenti pari a 250 e un'unica grande conferenza in esecuzione alla volta.</p>
<div class="alert">

> [!NOTE]
> È inoltre possibile supportare grandi conferenza con un numero di utenti compreso tra 250 e 1000 utenti distribuendo un pool Front End distinto con due Front End Server per ospitare le conferenze. Per informazioni dettagliate, vedere <A href="lync-server-2013-supporting-large-meetings.md">Supporto di riunioni di grandi dimensioni tramite Lync Server 2013</A>.


</div></td>
</tr>
<tr class="odd">
<td><p>Un server perimetrale</p></td>
<td><p>12.000 utenti remoti simultanei</p></td>
</tr>
<tr class="even">
<td><p>Un Server Director</p></td>
<td><p>12.000 utenti remoti simultanei</p></td>
</tr>
<tr class="odd">
<td><p>Monitoraggio e archiviazione</p></td>
<td><p>In Lync Server 2013, i servizi font-end di monitoraggio e archiviazione vengono ora eseguiti su ogni Front End Server, invece che su ruoli server separati.</p>
<p>Il monitoraggio e l'archiviazione richiedono comunque ognuno i proprio archivi di database. Se si esegue anche Exchange 2013, è possibile mantenere i dati di archiviazione in Exchange, invece che in un database SQL dedicato.</p></td>
</tr>
<tr class="even">
<td><p>Un Mediation Server</p></td>
<td><p>Il Mediation Server collocato insieme al Front End Server viene eseguito su ogni Front End Server in un pool e deve fornire sufficiente capacità per gli utenti nel pool. Per il Mediation Server autonomo, vedere la sezione &quot;Mediation Server&quot; più avanti in questo argomento.</p></td>
</tr>
<tr class="odd">
<td><p>Un server Standard Edition</p></td>
<td><p>Nel caso in cui si utilizzino server Standard Edition per ospitare utenti, è consigliabile utilizzare sempre due server accoppiati in base alle raccomandazioni descritte in <a href="lync-server-2013-planning-for-high-availability-and-disaster-recovery.md">Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013</a>. Ogni server della coppia può ospitare fino a 2.500 utenti e, in caso di errore di uno dei server, l'altro può supportare 5.000 utenti in uno scenario di failover.</p>
<p>Se la distribuzione include un notevole traffico audio o video, le prestazioni del server potrebbero risentirne in presenza di più di 2.500 utenti per server. In questo caso, è consigliabile aggiungere ulteriori server Standard Edition o passare a Lync ServerEnterprise Edition.</p></td>
</tr>
</tbody>
</table>


## Front End Server


> [!NOTE]
> I pool estesi non sono supportati per questo ruolo server.



In un pool Front End, è necessario avere un Front End Server per ogni 6.660 utenti nel pool, presupponendo che l'hyperthreading sia abilitato in tutti i server del pool e che l'hardware dei server rispetti le indicazioni in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md). Il numero massimo di utenti in un pool Front End è 80.000, presupponendo che l'hyperthreading sia abilitato in tutti i server del pool. Se si dispone di più di 80.000 utenti in un sito, è possibile distribuire più pool Front End.

Per il calcolo del numero di utenti in un pool Front End, includere gli utenti ospitati in Survivable Branch Appliance e Survivable Branch Server nelle succursali associate al pool Front End.

Quando un server attivo non è disponibile, le relative connessioni vengono trasferite automaticamente a tutti gli altri server nel pool. Se ad esempio si dispone di 30.000 utenti e di cinque Front End Server, se un server non è disponibile, le connessioni di 6000 utenti devono essere trasferite ad altri quattro server. I restanti quattro server avranno 7500 utenti ciascuno, ovvero una quantità superiore a quella consigliata.

Se invece si è iniziato con sei Front End Server per 30.000 utenti e uno diventa non disponibile, un totale di 5000 utenti verranno spostati ai cinque server rimanenti . Questi ultimi ospiteranno 6000 utenti ciascuno, ovvero una quantità compresa nell'intervallo consigliato.

Il numero massimo di utenti in un pool Front End è 80.000. Il numero massimo di Front End Server in un pool è pari a 12.

Per un pool Front End con 80.000 utenti, dodici Front End Server sono sufficienti per le prestazioni in distribuzioni tipiche conformi a quanto illustrato in [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md). Le distribuzioni progettate per supportare il failover in caso di ripristino di emergenza presuppongono che possano essere ospitati massimo 40.000 utenti in ognuno dei due pool Front End accoppiati, in cui ogni pool presenta un numero di Front End Server sufficiente per gli utenti di entrambi i pool qualora risultasse necessario il failover da un pool all'altro.

Il numero di utenti supportati da un determinato pool Front End assicurando un livello di prestazioni soddisfacente può differire da tali cifre per i motivi seguenti:

  - L'hardware dei Front End Server non soddisfa le indicazioni illustrate in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md).

  - L'utilizzo dell'organizzazione si discosta notevolmente dai modelli utente, ad esempio il traffico delle conferenze è molto superiore.

> [!important]  
> In Lync Server 2013, i database delle presenze sono ora ospitati in Front End Server, a differenza di Lync Server 2010 in cui sono ospitati nel server back-end. Ciò significa che le prestazioni e la capacità dei dischi dei Front End Server non devono essere compromessi dalle indicazioni elencate in precedenza in questa sezione e in <a href="lync-server-2013-server-hardware-platforms.md">Piattaforme hardware server per Lync Server 2013</a>, indipendentemente dal numero di utenti ospitati dai Front End Server.

Nella tabella seguente è illustrata la larghezza di banda media per messaggistica istantanea e presenza, dato il modello utente definito in [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Larghezza di banda media per utente</th>
<th>Requisiti di larghezza di banda per Front End Server con 6.660 utenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1,3 Kpbs</p></td>
<td><p>13 Mbps</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Per migliorare le prestazioni multimediali delle caratteristiche A/V Conferencing e Mediation Server entrambe collocate nei Front End Server, è necessario abilitare l'RSS (Receive-Side Scaling) sulle schede di rete dei Front End Server. RSS consente la gestione dei pacchetti in arrivo in parallelo da parte di più processori nel server. Per informazioni dettagliate, vedere l'articolo sui miglioramenti al Receive-Side Scaling in Windows Server 2008 all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268731">http://go.microsoft.com/fwlink/?linkid=268731</A>. Per informazioni dettagliate su come abilitare l'RSS, vedere la documentazione sulla scheda di rete.



## Valori massimi per le conferenze

Dato il modello utenti che prevede che il 5% degli utenti di un pool possano essere in conferenza in un qualsiasi momento, un pool di 80.000 utenti può avere circa 4.000 utenti in conferenza in qualsiasi momento. Le conferenze saranno variabili nel tipo di contenuti multimediali (ad esempio alcune solo di messaggistica istantanea, altre di messaggistica istantanea e audio, altre audio/video) e nel numero di partecipanti. Non esiste un limite rigido per il numero effettivo di conferenze consentite e le prestazioni reali sono determinate dall'utilizzo. Se ad esempio il numero di conferenze in modalità mista dell'organizzazione è molto superiore a quello previsto nel modello utenti, può essere necessario distribuire più Front End Server o A/V Conferencing Server rispetto a quanto consigliato in questo documento. Per informazioni dettagliate sui presupposti del modello utenti, vedere [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).

Le dimensioni massime supportate per le conferenze ospitate da un normale pool Front End di Lync Server 2013 che ospita anche utenti è pari a 250 partecipanti. Mentre è in corso una conferenza con 250 utenti, il pool continua a supportare anche altre conferenze, così che un totale del 5% di utenti del pool si trovano in conferenze simultanee. Ad esempio, in un pool di dodici Front End Server e 80.000 utenti, mentre è in corso una conferenza con 250 utenti, Lync Server supporta altri 3.750 utenti partecipanti a conferenze di dimensioni inferiori.

Indipendentemente dal numero di utenti ospitati sul pool Front End o sul server Standard Edition, Lync Server supporta minimo altri 125 utenti partecipanti in conferenze più piccole nello stesso pool o un server che ospita una conferenza con 250 utenti.

Per abilitare le conferenze con un numero di partecipanti compreso tra 250 e 1000 utenti, è possibile configurare un pool Front End distinto per ospitare queste conferenze. Questo pool Front End non ospita altri utenti. Per informazioni dettagliate, vedere [Supporto di riunioni di grandi dimensioni tramite Lync Server 2013](lync-server-2013-supporting-large-meetings.md).

Se l'organizzazione dispone di un numero di conferenze in modalità mista maggiore di quello presunto nel modello utenti, potrebbe essere necessario distribuire più Front End Server rispetto alle indicazioni nel documento (fino a un limite di 12 FE). Per informazioni dettagliate sui presupposti nel modello utenti, vedere [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).

## server perimetrale


> [!NOTE]
> I pool estesi non sono supportati per questo ruolo server.



È consigliabile distribuire un server perimetrale per ogni 12.000 utenti remoti che accedono simultaneamente a un sito. È consigliabile disporre di almeno due server perimetrali per la disponibilità elevata. Queste indicazioni presuppongono che l'hardware dei server perimetrali soddisfi quanto illustrato in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md).

Per il calcolo del numero di utenti per i server perimetrali, includere gli utenti ospitati in Survivable Branch Appliances e Survivable Branch Servers nelle succursali associate a un pool Front End del sito.


> [!NOTE]
> Per migliorare le prestazioni del servizio A/V Conferencing Edge nei server perimetrali, è consigliabile abilitare il Receive-Side Scaling (RSS) nelle schede di rete sui server perimetrali. L'RSS consente la gestione dei pacchetti in arrivo in parallelo da parte di più processori nel server. Per informazioni dettagliate, vedere l'articolo sui miglioramenti al Receive-Side Scaling in Windows Server 2008 all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268731">http://go.microsoft.com/fwlink/?linkid=268731</A>. Per informazioni dettagliate su come abilitare l'RSS, vedere la documentazione della scheda di rete.



## Server Director


> [!NOTE]
> I pool estesi non sono supportati per questo ruolo server.



Se si distribuisce il ruolo server Server Director, è consigliabile distribuire un Server Director per ogni 12.000 utenti remoti che accederanno a un sito simultaneamente. Sono consigliati almeno due Director per la disponibilità elevata. Queste indicazioni presuppongono che l'hardware dei server perimetrali soddisfi quanto illustrato in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md).

Per il calcolo del numero di utenti per i Director, includere gli utenti ospitati in Survivable Branch Appliances e Survivable Branch Servers nelle succursali associate a un pool Front End del sito.

## Mediation Server


> [!NOTE]
> I pool estesi non sono supportati per questo ruolo server.



Se si colloca Mediation Server con Front End Server, il Mediation Server viene eseguito su ogni Front End Server e deve fornire capacità sufficiente per gli utenti del pool.

Se si distribuisce un pool Mediation Server autonomo, il numero di Mediation Server da distribuire dipende da numerosi fattori, incluso l'hardware usato per Mediation Server, il numero di utenti VoIP, il numero di peer gateway controllati da ogni pool di Mediation Server, il traffico nelle ore di punta in questi gateway e la percentuale di chiamate con contenuti multimediali che ignorano il Mediation Server.

Nelle tabelle seguenti sono disponibili indicazioni sul numero di chiamate simultanee gestibili da un Mediation Server, presupponendo che l'hardware per i Mediation Server soddisfi i requisiti illustrati in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) e che l'hyperthreading sia abilitato. Per informazioni dettagliate sulla scalabilità di Mediation Server, vedere [Stima dell'utilizzo e del traffico vocale Lync Server 2013](lync-server-2013-estimating-voice-usage-and-traffic.md) e [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md).

Tutte le tabelle seguenti presuppongo i livelli di uso riepilogati in [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).

### Capacità Mediation Server autonomo: 70% di utenti interni, 30% di utenti esterni con capacità di chiamata senza bypass (transcodifica multimediale eseguita da Mediation Server)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Hardware dei server</th>
<th>Numero massimo di chiamate</th>
<th>Numero massimo di linee T1</th>
<th>Numero massimo di linee E1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Doppio processore, hex-core, CPU da 2,26 GHz con hyperthreading <strong>con hyper-threading disabilitato</strong>, con 32 GB di memoria e una scheda di rete con doppia porta.</p></td>
<td><p>1100</p></td>
<td><p>46</p></td>
<td><p>35</p></td>
</tr>
<tr class="even">
<td><p>Doppio processore, hex-core, CPU da 2,26 GHz con hyperthreading, con 32 GB di memoria e una scheda di rete con doppia porta.</p></td>
<td><p>1500</p></td>
<td><p>63</p></td>
<td><p>47</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Anche se nei test delle prestazioni sono stati utilizzati server con 32 GB di memoria, i server con 16 GB di memoria sono supportati in Mediation Server autonomo e sono sufficienti a garantire le prestazioni indicate in questa tabella.



### Capacità Mediation Server ( Mediation Server collocato con Front End Server) 70% di utenti interni, 30% di utenti esterni, capacità di chiamata senza bypass (elaborazione multimediale eseguita da Mediation Server)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Hardware dei server</th>
<th>Numero massimo di chiamate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Doppio processore, hex-core, CPU da 2,26 GHz con hyper-threading, con 32 GB di memoria e 2 schede di rete da 1 GB.</p></td>
<td><p>150</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Questo numero è notevolmente inferiore a quello dei Mediation Server autonomi perché il Front End Server deve gestire altre caratteristiche e funzioni per i 6600 utenti ospitati, oltre alla transcodifica necessaria per le chiamate vocali




> [!NOTE]
> Per migliorare le prestazioni del Mediation Server, è consigliabile abilitare l'RSS (Receive-Side Scaling) nelle schede di rete dei Mediation Server. L'RSS consente la gestione dei pacchetti in arrivo da parte di più processori nel server. Per informazioni dettagliati, vedere l'articolo sui miglioramenti apportati al Receive-Side Scaling in Windows Server 2008 all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268731">http://go.microsoft.com/fwlink/?linkid=268731</A>. Per informazioni dettagliati su come abilitare l'RSS, vedere la documentazione della scheda di rete.



## server back-end

In Lync Server 2013, i database delle presenze si trovano nei Front End Server invece che nel server back-end. Ne consegue un requisito più semplice per ogni server back-end in Lync Server 2013, equivalente al requisito hardware per il Front End Server. Al contrario, in Lync Server 2010 è necessario che il server back-end sia di fascia superiore con 25 dischi. Tuttavia, il carico di lavoro dei server back-end è comunque tale da rendere necessario soddisfare le indicazioni sull'hardware elencate in precedenza in questa sezione e in [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md).

Per fornire la disponibilità elevata del server back-end, è consigliabile distribuire il mirroring del server. Per ulteriori informazioni, vedere [Disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-back-end-server-high-availability.md).

## Monitoraggio e archiviazione

In Lync Server 2013, se si distribuiscono i servizi di monitoraggio o archiviazione, le funzionalità front-end di questi servizi vengono eseguite nei Front End Server, invece che in ruoli server distinti. Per il monitoraggio e l'archiviazione di ognuno vengono comunque usati appositi archivi di database, separati dall'archivio back-end. In alternativa, se si distribuisce Exchange 2013, è possibile archiviare dati dei messaggi istantanei in Exchange invece che in un archivio SQL dedicato.

Nella tabella seguente è indicata la quantità approssimativa di spazio di archiviazione del database necessario per ogni utente al giorno relativamente ai dati di monitoraggio e archiviazione.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Registrazione dettagli chiamata (Monitoraggio)</strong></p></td>
<td><p><strong>QoE (Monitoraggio)</strong></p></td>
<td><p><strong>Archiviazione</strong></p></td>
</tr>
<tr class="even">
<td><p>Spazio su disco necessario per utente al giorno</p></td>
<td><p>49 KB</p></td>
<td><p>28 KB</p></td>
<td><p>57 KB</p></td>
</tr>
</tbody>
</table>


Durante i test delle prestazioni, Microsoft ha usato l'hardware descritto nella tabella seguente per il server di database a fini di monitoraggio e archiviazione. Durante i test sono stati raccolti i dati di due pool Front End, ognuno dei quali con 80.000 utenti.

### Hardware usato nei test sulle prestazioni di monitoraggio e archiviazione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Scelta consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>Processore doppio a 64 bit, hex-core, 2,26 GHz o superiore</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>48 gigabyte (GB)</p></td>
</tr>
<tr class="odd">
<td><p>Disco</p></td>
<td><p>25 unità disco rigido a 10.000 rpm con 300 GB su ogni disco, con la configurazione seguente</p>
<h3 id="section-3"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Unità</strong></p></td>
<td><p><strong>Configurazione RAID</strong></p></td>
<td><p><strong>Numero di dischi</strong></p></td>
</tr>
<tr class="even">
<td><p>File di dati dei database dei servizi CDR, QoE e di archiviazione su una singola unità</p></td>
<td><p>1+0</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>File di log del database CDR</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>File di log del database QoE</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>File di log del database del servizio di archiviazione</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>Rete</p></td>
<td><ul><li><p>Una scheda di rete dual port, 1 Gbps o superiore (due consigliate, da associare a un singolo indirizzo MAC e a un singolo indirizzo IP)</p></li></ul></td>
</tr>
</tbody>
</table>


## Contenuto della sezione

  - [Stima dell'utilizzo e del traffico vocale Lync Server 2013](lync-server-2013-estimating-voice-usage-and-traffic.md)

  - [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md)

