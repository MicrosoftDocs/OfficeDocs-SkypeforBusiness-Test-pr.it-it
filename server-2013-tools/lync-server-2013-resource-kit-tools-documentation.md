---
title: Documentazione sugli strumenti del Resource Kit di Lync Server 2013
TOCTitle: Documentazione sugli strumenti del Resource Kit di Lync Server 2013
ms:assetid: b1c341f1-86fa-479d-ba4d-28df5a4c1622
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945604(v=OCS.15)
ms:contentKeyID: 52062505
ms.date: 09/30/2014
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Documentazione sugli strumenti del Resource Kit di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-09_

In questo argomento vengono descritti gli strumenti inclusi nel Lync Server 2013 Resource Kit, compresi lo scopo di ogni strumento ed esempi di utilizzo. Il Lync Server 2013, Strumenti del Resource Kit consente di semplificare le attività di routine per gli amministratori IT che distribuiscono e gestiscono Lync Server 2013. Ad esempio, lo strumento **Web Conf Data** può essere usato per semplificare il controllo dei dati caricati dagli utenti durante una riunione online. Lo strumento **SEFAUtil** può invece essere usato per configurare l'inoltro delle chiamate ai delegati e la risposta per gli utenti. Per una gestione più efficace di Lync Server 2013, gli amministratori IT sono invitati a usare questi strumenti.

## Installazione degli strumenti del Resource Kit

Per installare Lync Server 2013, Strumenti del Resource Kit, scaricare **OCSReskit.msi**. È possibile scaricare il programma di installazione di Strumenti del Resource Kit dall'Area download all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkID=330429](http://go.microsoft.com/fwlink/p/?linkid=330429).

Eseguire **OCSResKit.msi** per un'installazione semplice. Il file con estensione msi installa tutti gli strumenti nel percorso seguente: **%Program Files%\\Microsoft Lync Server 2013\\ResKit**. Gli strumenti costituiti da file eseguibili completi si trovano in questa cartella. Gli strumenti che contengono anche file, si trovano nelle relative sottocartelle.

## Ambienti supportati

Per prestazioni ottimali, Lync Server 2013, Strumenti del Resource Kit deve essere installato nello stesso ambiente e con le stesse specifiche necessari per Lync Server 2013.

## Panoramica degli strumenti del Resource Kit

Nell'elenco seguente sono descritti gli strumenti forniti nel Lync Server 2013 Resource Kit. Nella sezione seguente è riportata una descrizione di ogni strumento, inclusi i requisiti e l'utilizzo di esempio.

  - ABSConfig

  - Bandwidth Policy Service Monitor

  - Bandwidth Utilization Analyzer

  - Call Parkometer

  - CleanupStorageServiceData

  - DBAnalyze

  - ImportStorageServiceData

  - LCSSync

  - LookupUserConsole

  - MsTurnPing

  - Network Configuration Viewer

  - Response Group Agent Live

  - SEFAUtil

  - SYSPrep.ps1

  - Unassigned Number Announcements Migration

  - Web Conf Data

## ABSConfig

Lo strumento ABSConfig (Address Book Service Configuration) è uno strumento di amministrazione che consente agli amministratori di personalizzare la configurazione del Servizio Rubrica in Lync Server 2013. Questo strumento consente inoltre agli amministratori di Lync Server 2013 di ripristinare le impostazioni predefinite del Servizio Rubrica.

## Descrizione

ABSConfig è un'applicazione con interfaccia grafica che consente gli amministratori di configurare gli attributi di Servizi di dominio Active Directory correlati al Servizio Rubrica.

Di seguito sono riportati gli scenari principali per lo strumento:

  - Per consentire gli amministratori di mappare gli attributi in Servizi di dominio Active Directory agli attributi per Lync Server 2013.

  - Per consentire agli amministratori di specificare di includere o escludere l'attributo di Servizi di dominio Active Directory nei file del Servizio Rubrica.

  - Per consentire agli amministratori di ripristinare le impostazioni predefinite del Servizio Rubrica.

È possibile avviare lo strumento ABSConfig mediante il file absConfig.exe. Lo strumento si apre sulla scheda **Configure Attributes**. In questa tabella sono disponibili le opzioni per mappare gli attributi di Servizi di dominio Active Directory ai campi degli attributi per Lync Server 2013 e per includere o escludere gli utenti nei file del Servizio Rubrica in base a filtri per gli attributi specifici. Sono inoltre presenti opzioni per personalizzare il valore del numero di telefono da includere nel file Rubrica. L'opzione **Restore Defaults** consente agli amministratori di ripristinare le impostazioni del Servizio Rubrica su valori predefiniti.

## Modifiche rispetto a Lync Server 2010

Nello strumento di configurazione ABS di Lync Server 2013 è possibile rimuovere gli attributi (righe) deselezionando la casella di controllo "enable" per l'attributo. Questa operazione equivale a eliminare la riga in Lync Server 2010.


> [!NOTE]
> La casella di controllo enable si trova nella colonna all'estrema destra. Potrebbe essere necessario scorrere verso destra per visualizzarla



## Output

ABSConfig archivia la configurazione del Servizio Rubrica nel database.
```C++
    Path: %ProgramFiles%\Microsoft Lync Server 2013\Reskit
```
## Scopo

ABSConfig offre un modo semplice e veloce per personalizzare il Servizio Rubrica di Lync Server 2013.

## Requisiti

## Computer

ABSConfig può essere eseguito solo da un computer aggiunto a un dominio in cui è installato Lync Server 2013. Nel caso di Lync Server 2013, Enterprise Edition, lo strumento può essere eseguito in qualsiasi server front-end in cui è stato abilitato il Servizio Rubrica durante l'installazione.

## Rete

Il computer deve essere in grado di connettersi al pool Front End e al database back-end.

## Software

Prima di eseguire lo strumento ABSConfig è necessario installare i componenti software seguenti:

  - Microsoft Lync Server 2013

## Utenti

Amministratori che dispongono delle autorizzazioni necessarie per aggiornare la distribuzione di Lync Server 2013.

## Esempi

È possibile avviare ABSConfig digitando **ABSConfig.exe** in un prompt dei comandi. Di seguito è illustrata l'interfaccia utente dello strumento ABSConfig.

![Strumento ABSConfig.exe](images/JJ945604.6fb63a70-7b63-4b8b-b7d1-82fe9aa2028f(OCS.15).jpg "Strumento ABSConfig.exe")

## Riepilogo

Lo strumento ABSConfig offre agli amministratori un modo semplice e veloce per personalizzare il Servizio Rubrica di Lync Server 2013.

## Bandwidth Policy Service Monitor

Lo strumento Bandwidth Policy Service Monitor consente agli amministratori di visualizzare l'elenco degli elementi seguenti:

1.  Tutti i servizi criteri larghezza di banda (Autenticazione e Core) di Lync Server 2013 nella topologia

2.  Le connessioni effettuate da ogni servizio ad altri servizi criteri larghezza di banda e ai server perimetrali

3.  Tutti i collegamenti configurati nel documento di configurazione di rete e l'utilizzo della larghezza di banda in tempo reale segnalati da ognuno dei servizi criteri larghezza di banda

## Descrizione

Lo strumento Bandwidth Policy Service Monitor è implementato come applicazione con interfaccia grafica. Per avviare lo strumento, gli amministratori devono eseguire il file PDPMonUI.exe.

Quando lo strumento viene avviato, tenta di individuare l'elenco dei servizi criteri larghezza di banda nella topologia. Al termine dell'aggiornamento iniziale, il riquadro a sinistra della finestra viene popolato con un elenco di servizi raggruppati in base ai cluster a cui appartengono.

Quando gli amministratori selezionano un servizio criteri larghezza di banda specifico, nel riquadro a destra vengono visualizzate le informazioni relative al servizio in questione. Nel riquadro sono inoltre disponibili due schede principali in cui sono visualizzate altre informazioni.

## Scheda Machine Info

Nella scheda **Machine Info** vengono visualizzati i dettagli del servizio criteri larghezza di banda selezionato, l'elenco e lo stato di tutte le connessioni effettuate dal servizio criteri larghezza di banda ad altri servizi.

## Scheda Topology Info

Nella scheda **Topology Info** è visualizzato l'elenco di tutti i collegamenti configurati nelle impostazioni di configurazione di rete. Per ogni collegamento, è visualizzata la capacità della larghezza di banda audio e video. È inoltre visualizzata la larghezza di banda attualmente utilizzata, sia in Kbps sia come percentuale della capacità complessiva. Lo strumento usa una codifica a colori per evidenziare i collegamenti che presentano un utilizzo prossimo alla capacità totale per consentire agli amministratori di isolare velocemente tali collegamenti.


> [!NOTE]
> Se si verificano errori quando lo strumento Bandwidth Policy Service Monitor si connette a uno dei servizi criteri larghezza di banda configurati, le informazioni nelle schede <STRONG>Machine Info</STRONG> e <STRONG>Topology Info</STRONG> non verranno popolate. È tuttavia possibile che lo strumento riesca inizialmente a connettersi e che successivamente perda la connessione al servizio. In tal caso, le informazioni visualizzate dagli amministratori potrebbero essere non aggiornate. È disponibile un timestamp <STRONG>Last Updated</STRONG> su ognuna delle schede per consentire agli amministratori di visualizzare la data e l'ora dell'ultimo aggiornamento per un servizio criteri larghezza di banda specifico.



## Output

Non è disponibile l'output della riga di comando. L'output del programma è contenuto all'interno dell'interfaccia utente grafica principale.

## Scopo

Lo strumento Bandwidth Policy Service Monitor offre agli amministratori la visibilità sullo stato di ogni servizio criteri larghezza di banda definito nella topologia. Gli amministratori possono inoltre visualizzare l'utilizzo della larghezza di banda in tempo reale per tutti i collegamenti definiti nel documento di configurazione della rete.

## Requisiti

Lo strumento Bandwidth Policy Service Monitor deve essere eseguito in un computer appartenente alla topologia di Lync Server.

## Riepilogo

Lo strumento Bandwidth Policy Service Monitor rappresenta una risorsa preziosa per gli amministratori in quanto consente loro di verificare lo stato di tutti i servizi criteri larghezza di banda nella topologia, e soprattutto, di ottenere informazioni sull'utilizzo della larghezza di banda in tempo reale per i collegamenti definiti nelle impostazioni di configurazione della rete.

## Bandwidth Utilization Analyzer

Bandwidth Utilization Analyzer è uno strumento che consente di creare rapporti con varie visualizzazioni dell'utilizzo della larghezza di banda da parte degli endpoint UC tra collegamenti WAN nella rete aziendale. Tali rapporti possono essere usati per ottenere informazioni sullo schema di utilizzo della larghezza di banda e per supportare la pianificazione della capacità della larghezza di banda.

## Descrizione

Lo strumento Bandwidth Utilization Analyzer è implementato come applicazione con interfaccia grafica. Questo strumento genera rapporti specifici per l'utilizzo dell'audio sulla rete per supportare la pianificazione della capacità. Scorre inoltre la capacità della larghezza di banda assegnata ai vari collegamenti.

## Output

Bandwidth Utilization Analyzer fornisce tracce grafiche della capacità e dell'utilizzo della larghezza di banda per l'audio per tutti i collegamenti su configurati nel sistema.

## Scopo

In qualsiasi distribuzione voce e video, è fondamentale monitorare e ottenere informazioni sulle tendenze dell'utilizzo della larghezza di banda del traffico multimediale sulla rete aziendale. Lo strumento Bandwidth Utilization Analyzer consente agli amministratori di ottenere questo risultato. Lo strumento esegue le operazioni seguenti:

  - Genera rapporti specifici per l'utilizzo dell'audio sulla rete

  - Favorisce una pianificazione della capacità più efficace e consente di scorrere la capacità della larghezza di banda assegnata ai vari collegamenti

Bandwidth Utilization Analyzer consente di generare tracce grafiche dei rapporti relativi alla capacità e all'utilizzo della larghezza di banda, come illustrato di seguito:

  - Tutti i collegamenti WAN nella rete aziendale

  - Filtro in base ai collegamenti WAN selezionati

  - Filtro in base ai collegamenti WAN che hanno superato la capacità del collegamento

  - Filtro in base ai collegamenti WAN che hanno sottoutilizzato la larghezza di banda allocata

  - Filtro in base ai collegamenti WAN che hanno raggiunto livelli critici (utilizzo della larghezza di banda superiore al 90% della capacità della larghezza di banda del collegamento WAN)

  - Filtro in base al tipo di collegamento WAN: collegamenti rete-sito, collegamenti tra più aree di rete e collegamenti all'interno di un sito

  - Filtro in base all'area di rete

## Applicazioni

Nello strumento Bandwidth Utilization Analyzer sono incluse le due applicazioni (strumenti) seguenti:

  - **WanLinkLogCollector.exe**   Questo strumento consente all'utente di immettere le informazioni necessarie.

  - **BandwidthUtilizationAnalyzer.xlsm **  WanLinkLogCollector.exe avvia automaticamente un rapporto del software per i fogli di calcolo Microsoft Excel. Questa applicazione consente all'utente di applicare filtri al rapporto come descritto più avanti un questo articolo.

## Fasi dell'utilizzo di Bandwidth Utilization Analyzer

Per l'utilizzo dello strumento Bandwidth Utilization Analyzer sono previste due fasi:

  - Raccolta di log, eseguita mediante WanLinkLogCollector.exe

  - Personalizzazione di rapporti, eseguita mediante BandwidthUtilizationAnalyzer.xlsm

<table>
<thead>
<tr class="header">
<th><img src="images/JJ945592.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È consigliabile non fare avviare manualmente BandwidthUtilizationAnalyzer.xlsm dagli utenti finali.</td>
</tr>
</tbody>
</table>


## Avvio di Bandwidth Utilization Analyzer

Avviare WanLinkLogCollector.exe al prompt dei comandi o con Esplora risorse.

**Uso di WanLinkLogCollector.exe**

Per l'uso di WanLinkLogCollector.exe sono previsti tre passaggi:

1.  **Registrare la sequenza temporale**   Specificare la sequenza temporale in base alla quale deve essere generato il rapporto

2.  **Specificare le directory dei file**   Fornire le informazioni relative ai percorsi dei file

3.  **Raccogliere i log e avviare il visualizzatore rapporti **  Eseguire il comando per generare il rapporto

## Passaggio 1 - Registrare la sequenza temporale

La registrazione della sequenza temporale consente all'utente dello strumento di specificare gli elementi seguenti, come descritto nella figura riportata di seguito.

1.  **Start date** Si tratta della data di inizio della sequenza temporale in base alla quale deve essere generato il rapporto, ad esempio 1° agosto 2010.

2.  **End date** Si tratta della data di fine della sequenza temporale in base alla quale deve essere generato il rapporto, ad esempio 30 settembre 2010.
    
    ![Date di inizio e fine per l'analisi dell'utilizzo della larghezza di banda](images/JJ945604.2c597cfc-3372-4d41-816b-26202f607ad8(OCS.15).jpg "Date di inizio e fine per l'analisi dell'utilizzo della larghezza di banda")  

## Passaggio 2 - Specificare le directory dei file

L'utente può specificare le directory di file seguenti, come illustrato di seguito.

  - **Server log files location** Percorso della cartella in cui sono archiviati i log del server criteri larghezza di banda. In genere, in \<fileserver\>\\\<scelta di FE\>\\AppServerFiles\\PDP.

  - **Temporary file storage location ** Percorso dei file temporanei in cui vengono archiviati i file intermedi durante la fase di generazione del rapporto.

![Directory di file per l'analisi dell'utilizzo della larghezza di banda](images/JJ945604.d66daeac-1669-45e3-932d-3f6782840c2a(OCS.15).jpg "Directory di file per l'analisi dell'utilizzo della larghezza di banda")


> [!NOTE]
> Verificare che l'utente dello strumento disponga delle autorizzazioni di accesso ai file sufficienti per la cartella dei log del server e dell'archivio dei file temporanei.



## Passaggio 3 - Raccogliere i log e avviare il visualizzatore rapporti

Per raccogliere i log e avviare il visualizzatore rapporti, fare clic su **Execute** come illustrato di seguito. In questo passaggio verranno raccolti i dati necessari.

![Raccolta dei dati per l'analisi dell'utilizzo della larghezza di banda](images/JJ945604.0019cb2c-7c01-4dc9-ac90-ac47c47d1bfd(OCS.15).jpg "Raccolta dei dati per l'analisi dell'utilizzo della larghezza di banda")

Se la convalida dei dati immessi ha esito positivo, viene visualizzato il messaggio riportato di seguito.

![Notifica della raccolta dei log in Bandwidth Utili](images/JJ945604.eda91da8-3285-4eab-8ccb-c6d89c8cc221(OCS.15).jpg "Notifica della raccolta dei log in Bandwidth Utili")

Fare clic su **OK**. BandwidthUtilizationAnalyzer.xlsm viene avviato automaticamente. Seguire le istruzioni visualizzate nel messaggio. Per informazioni dettagliate, vedere **Uso di BandwidthUtilizationAnalyzer.xlsm** nella sezione successiva.


**Uso di BandwidthUtilizationAnalyzer.xlsm**

1.  Quando BandwidthUtilizationAnalyzer.xlsm viene avviato automaticamente, fare clic su **Refresh**, come illustrato di seguito.
    
    ![BandwidthUtilizationAnalyzer.xlsm](images/JJ945604.c4e675b9-1671-400e-a712-6db82d731b39(OCS.15).jpg "BandwidthUtilizationAnalyzer.xlsm")

2.  Quando viene aperta una cartella di file, selezionare consolidated.csv dal percorso specificato nel messaggio, come illustrato di seguito. Viene inoltre visualizzato il percorso **C:\\Temp**.
    
    ![Apertura di una cartella in Bandwidth Utilization Analyzer.](images/JJ945604.601cc572-cee9-45fb-9ed1-c4b96a2fa21e(OCS.15).jpg "Apertura di una cartella in Bandwidth Utilization Analyzer.")

3.  Fare clic su **Import**.

4.  La traccia grafica viene generata automaticamente. Sarà disponibile non appena il puntatore in esecuzione in background sparisce.
    
    ![Applicazione di filtri nella visualizzazione Report.](images/JJ945604.1416468e-e3ab-478e-b569-e42ba9c27a17(OCS.15).jpg "Applicazione di filtri nella visualizzazione Report.")

## Applicazione di filtri alla visualizzazione rapporti

Di seguito sono illustrati i filtri che possono essere applicati alla visualizzazione rapporti:

![Applicazione di filtri nella visualizzazione Report.](images/JJ945604.1416468e-e3ab-478e-b569-e42ba9c27a17(OCS.15).jpg "Applicazione di filtri nella visualizzazione Report.")

1.  **Name** Filtra in base ai collegamenti WAN (il filtro si trova nella parte destra del grafico). Il prefisso indica i tipi di collegamenti seguenti. Vedere la casella verticale (blu):
    
      - **S Site** Collegamento WAN da un sito di rete a un'area di rete
    
      - **IS Inter-Site** Collegamento WAN tra due siti di rete
    
      - **R Inter-Region** Collegamento WAN tra due aree di rete

2.  **Exceeded limit** Filtra in base ai collegamenti WAN il cui utilizzo della larghezza di banda supera la capacità della larghezza di banda

3.  **Critical levels** Filtra in base ai collegamenti WAN il cui utilizzo della larghezza di banda ha raggiunto il 90% o più della capacità della larghezza di banda

4.  **Under-utilized** Filtra in base ai collegamenti WAN il cui utilizzo della larghezza di banda è inferiore al 25% della capacità della larghezza di banda

5.  **Link type** Filtra in base ai tipi di collegamenti WAN seguenti:
    
      - Tipo **Network site**
    
      - Tipo **Inter-site**
    
      - Tipo **Inter-Region link**

6.  **Region** Filtra in base all'area di rete

Nelle figure seguenti sono illustrati i filtri descritti in precedenza.

Filtro per **Name**. Selezionare l'elenco di collegamenti da visualizzare nel grafico.

![Filtro per nome in BandwidthUtilizationAnalyzer.](images/JJ945604.002b7c8e-f0da-48ce-9e1a-5c34d2cab063(OCS.15).jpg "Filtro per nome in BandwidthUtilizationAnalyzer.")

Filtro per **Exceeded limit**. Selezionare **True** per applicare il filtro.

![Filtro per Exceeded Limit.](images/JJ945604.5946c95e-76ce-46ca-8f3e-a79be1e5c527(OCS.15).jpg "Filtro per Exceeded Limit.")

Filtro per **Critical levels**. Selezionare **True** per applicare il filtro.

![Filtro per Critical Levels.](images/JJ945604.60771a52-d8ba-4cb9-a02d-d6c888cb5505(OCS.15).jpg "Filtro per Critical Levels.")

Filtro per **Under utilized**. Selezionare **True** per applicare il filtro.

![Filtro per Under Utilized.](images/JJ945604.95a2bf01-5aba-4927-af47-1ad3c459d791(OCS.15).jpg "Filtro per Under Utilized.")

Filtro per **Link Type**. Selezionare il tipo o i tipi di collegamenti da visualizzare.

![Filtro per Link Type.](images/JJ945604.08757949-06bd-4cf3-809f-d81fd23a6639(OCS.15).jpg "Filtro per Link Type.")

Filtro per **Region**. Selezionare i tipi di collegamento da visualizzare da un elenco di aree.

![Filtro per Region.](images/JJ945604.5de4cec4-6c09-48bb-98c7-b56f7bdb3d5a(OCS.15).jpg "Filtro per Region.")

## Requisiti

  - .NET Framework 3.5

  - Microsoft Excel 2010 o Excel 2007

## Riepilogo

Bandwidth Utilization Analyzer è utilizzato per tracciare l'uso della larghezza di banda audio per il traffico UC sulla rete. Questo strumento può inoltre essere usato per creare rapporti relativi all'utilizzo della larghezza di banda video.

## Call Parkometer

Call Parkometer è un'applicazione da riga di comando che offre accesso semplificato al database del codice orbit del parcheggio di chiamata.

## Descrizione

Call Parkometer è uno strumento che consente di tenere traccia delle chiamate attualmente parcheggiate. Raccoglie inoltre le statistiche relative all'utilizzo dei codici orbit e del server parcheggio di chiamata. Questo strumento da riga di comando fornisce accesso in lettura e scrittura al database SQL Server del codice orbit del server di parcheggio di chiamata da un computer locale o connesso in modalità remota.

Tutte le opzioni si escludono a vicenda. Di seguito viene illustrata la sintassi della riga di comando:

  - Parametro**–o:** elenca tutti gli intervalli del codice orbit configurati per questo pool.

  - Parametro **–n:** elenca tutti i codici orbit attualmente utilizzati in questo pool. Le informazioni visualizzate sono le seguenti:
    
      - URI SIP del parcheggiato e del parcheggiante.
    
      - Nome host del server di parcheggio di chiamata in cui è parcheggiata la chiamata.
    
      - Timestamp del parcheggio della chiamata.

  - Parametro **–f:** elenca tutti il numero di codici orbit attualmente liberi nel pool.

  - Parametro **–r \<n\>:** elenca le ultime \<n\> chiamate parcheggiate. Le informazioni visualizzate sono le seguenti:
    
      - URI SIP del parcheggiato.
    
      - URI SIP del parcheggiante.
    
      - Nome host del server di parcheggio di chiamata in cui è stata parcheggiata la chiamata.
    
      - Timestamp del recupero o dell'interruzione della chiamata.

  - Parametro **-t\<n\>:** verifica la prenotazione del codice orbit nel database per mostrare la casualità dei numeri di codice orbit assegnati.

## Output

A seconda dei parametri di input specificati a un prompt dei comandi, lo strumento Call Parkometer visualizza l'output seguente:

  - Tutti gli intervalli del codice orbit configurati per questo pool.

  - Chiamate attualmente parcheggiate

  - Numero di codici orbit liberi (disponibili)

  - Chiamate parcheggiate di recente

  - Codici orbit riservati per la verifica dei valori dei codici orbit uniformi e casuali

## Scopo

Lo strumento CPS offre l'accesso da riga di comando al database del server di parcheggio di chiamata. L'amministratore può visualizzare l'utilizzo del server di parcheggio di chiamata e determinare il numero di codici orbit assegnati a un pool.

## Requisiti

Non sono previsti requisiti se lo strumento viene eseguito nello stesso computer in cui è in esecuzione il server parcheggio di chiamata. Se lo strumento viene eseguito in un computer remoto, il database SQL Server utilizzato da Lync Server 2013 deve essere configurato per consentire l'accesso remoto. È necessario configurare Call Parkometer con una stringa di connessione del database SQL Server affinché esegua la connessione al database SQL Server del pool. Questa stringa di connessione del database SQL Server è definita nel file di configurazione, **parkometer.exe.config**. Il file deve essere posizionato nella stessa directory in cui si trova il file parkometer.exe. Il file XML seguente riporta un esempio di parkometer.exe.config. I parametri che devono essere configurati sono nome utente (ad esempio mydomain\\Administrator), password (ad esempio mypassword) e nome host (ad esempio myserver).
```XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
       <add key="SQL" value="server=myserver\RTC;
    database=cpsdyn;
    User Id=mydomain\Administrator;
    Password=mypassword.;
    Integrated Security=false;"/>
      </appSettings>
    </configuration>
```
## Esempi

Intervalli codici orbit distribuiti: il parametro \\endash o elenca tutti gli intervalli di codici orbit configurati per questo pool, come visualizzato

![Intervalli dei codici orbit in Call Parkometer.](images/JJ945604.9ede64cb-29d9-4782-a34b-b76c42fbdcad(OCS.15).jpg "Intervalli dei codici orbit in Call Parkometer.")

Chiamate attualmente parcheggiate: il parametro \\endash n elenca tutti i codici orbit attualmente utilizzati in questo pool, come visualizzato

![Chiamate attualmente parcheggiate in Call Parkometer.](images/JJ945604.07a7eec4-7999-4c92-93f0-95525b244b4c(OCS.15).jpg "Chiamate attualmente parcheggiate in Call Parkometer.")

Numero di codici orbit liberi: il parametro \\endash f elenca tutti il numero di codici orbit attualmente liberi nel pool, come visualizzato

![Codici orbit liberi in Call Parkometer.](images/JJ945604.ecc1d621-0ca0-4ecf-a579-08b41c6f08ed(OCS.15).jpg "Codici orbit liberi in Call Parkometer.")

Chiamate parcheggiate di recente: il parametro \\endash r \<n\> elenca le ultime \<n\> chiamate parcheggiate, come visualizzato

![Chiamate parcheggiate di recente in Call Parkometer.](images/JJ945604.1c5eb27d-faa1-491b-b4aa-b484255c3353(OCS.15).jpg "Chiamate parcheggiate di recente in Call Parkometer.")

Prenotazione codici orbit di test: il parametro \\endash t \<n\> verifica la prenotazione di un codice orbit nel database, come visualizzato

![Prenotazione codici orbit di test in Call Parkometer.](images/JJ945604.84c9b69e-7af0-4224-8711-a43a28f08691(OCS.15).jpg "Prenotazione codici orbit di test in Call Parkometer.")

## Riepilogo

Call Parkometer è uno strumento da riga di comando che offre informazioni dettagliate sul server di parcheggio di chiamata.

## CleanupStorageServiceData

Lo strumento del Resource Kit CleanupStorageServiceData consente l'eliminazione dei dati organi dal servizio di archiviazione di Lync Server. Una funzione del servizio di archiviazione prevedere il buffering delle comunicazioni tra Lync Server e vari endpoint di archiviazione dati back-end, ad esempio SQL Server e Exchange.

## Descrizione

Per supportare la disponibilità elevata, il servizio di archiviazione LYSS accetta e salva copie dei dati su più server front-end temporaneamente nel pool e rimuove tali dati non appena sono stati recapitati al relativo percorso di storage a lungo termine definitivo. Esistono situazioni insolite che possono verificarsi durante il funzionamento altrimenti normale, ad esempio quando un server si arresta in modo anomalo o si verifica un errore di elaborazione e alcuni dati non vengono puliti correttamente. Tali dati sono innocui ma utilizzano un numero limitato di risorse di elaborazione. La maggior parte delle normali operazioni di manutenzione dei dati necessarie sono automatizzate, ma questo strumento consente l'identificazione e la rimozione sicure di tali dati orfani quando non è possibile eseguire la rimozione automatica. L'utilizzo di questo strumento è indicato quando viene generato un avviso di monitoraggio di System Center Operations Manager (SCOM) che richiede all'amministratore di rimuovere i dati non necessari dai database LYSS locali nel pool. Nel registro eventi nel server Front End che ha generato l'avviso sarà presente un evento corrispondente. I dettagli dell'evento conterranno informazioni relative alla quantità di dati orfani contenuti nel server Front End e l'evento verrà generato quando tali dati superano determinate soglie predefinite.

## Requisiti

Installare Lync Server 2013, Strumenti del Resource Kit Lo strumento viene eseguito nei computer aggiunti al dominio in cui sono installati Lync Server e Lync Server 2013 Management Shell. Lo strumento utilizza un cmdlet dalla shell di gestione per identificare tutti i server front-end nel pool. In secondo luogo, lo strumento deve essere eseguito da un computer nel pool in cui è installato il database **RtcLocal**. Questo database è utilizzato dallo strumento CleanupStorageServiceData per ottenere i dettagli della connessione necessaria per comunicare con il servizio di routing di Lync Server. Infine, l'account o la credenziale che richiama lo strumento deve disporre dell'autorizzazione di lettura e scrittura nella condivisione file in cui desidera scrivere il log di output. Per l'esecuzione di questo strumento è inoltre necessario che il pool si trovi in uno stato stabile, ovvero, ogni server front-end deve essere operativo, deve essere possibile connettersi all'istanza LYNCLOCAL di SQL Server e al database LYSS e ogni gruppo di routing deve disporre di un set completo di 1) server front-end primari e 2) server front-end secondari.

## Esempi

C:\\Programmi\\Microsoft Lync Server 2013\\ResKit\\StorageService\> ImportStorageServiceData.exe
```C++
    Description:
    This tool will remove orphaned data from the Storage Service database
    for a pool. You are required to run this tool on a machine inside the
    pool which has the Lync Server Management Shell installed and has RtcLocal database installed.
    Usage: Default behavior is to clean up orphaned data from the all the 
           Storage Service databases in the current pool.
    Additional Options:
    -Verbose    : Turn verbose output on.
    -LogPath    : The UNC path to which to write the log.
    ------------------------------------------------------------------------------
    Please wait while we initialize...
    Found 4 front end servers
    Replica Instances for LYSS Service
    Address: server2.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server1.vdomain.com - Primaries: 7 Secondaries: 14
    Address: server3.vdomain.com - Primaries: 7 Secondaries: 14
    Primary Total Count = 28, Secondary Total Count = 56
    Finding and removing orphaned data for 28 routing groups
    Removing 1 stale groups from FE server.vdomain.com
    No stale routing groups detected on FE server2.vdomain.com
    No stale routing groups detected on FE server1.vdomain.com
    No stale routing groups detected on FE server3.vdomain.com
    Searching for stale queue items
    Removed 20 stale queue items for routing group 17D5435AE40259F7BBDF1866776386E4
    No stale queue items found for routing group 1975349662315F90B119DACB4F2AE3AD
    No stale queue items found for routing group 1A23E3D58BDB5A458A0B73F34AB7ACBE
    No stale queue items found for routing group 1AC91E3A1029535A80123121989CEADC
    No stale queue items found for routing group 3313935458E35B9B9759E08A15D251E6
    No stale queue items found for routing group 39BB0035B06B5427873FC6099720462A
    No stale queue items found for routing group 40721948E7B55CE893A53E911F76D185
    No stale queue items found for routing group 4501E04EAE4856059346949FF817C220
    No stale queue items found for routing group 4D833C98801F546F8E45E417EE028E2E
    No stale queue items found for routing group 5AD77443AD955A22A876749BE66D5317
    No stale queue items found for routing group 69844A271E6C5633A1F2B46A42287DD6
    No stale queue items found for routing group 69DA3BE407A95C7284EB4B1337718C93
    No stale queue items found for routing group 8437358AB34A5CC8967D5EF39494AB8D
    No stale queue items found for routing group 8ED455B1789655359816E1C5BF4C430F
    No stale queue items found for routing group 904F6C9B8AC951AE8B3C86684D3832E4
    No stale queue items found for routing group 90AAB3AE9A1950E0ADE7809A27021D63
    No stale queue items found for routing group 944F5724C65C5F93900DC1C8C898B102
    No stale queue items found for routing group 9E8A2630250C51769E39F63F0FB552BA
    No stale queue items found for routing group A11E27AE439A582288D4657EDA86B565
    No stale queue items found for routing group A9B10C76E764556FAEA3E47301EDF518
    No stale queue items found for routing group AEA2699E74ED59848ACEA7896699430D
    No stale queue items found for routing group B269961603E75065AFDA4F4F006DA5E4
    No stale queue items found for routing group BB873D9A3DA959DAB2FD743E5AA619F7
    No stale queue items found for routing group BCC6A48FBA2454B79B9EDB276657A404
    No stale queue items found for routing group C8EF4805722B5F6C876EBC0440B420FD
    No stale queue items found for routing group CA38EBDAC4845489ACE208C2240E4056
    No stale queue items found for routing group F5921887DB025C5F908CE42DB7F1AEE8
    No stale queue items found for routing group F9E606A825395422B3BF7A01ECBB7B1F
    Writing log: M:\Dev\Server\ResKit\StorageService\CleanupStorageServiceData.Log_20121009_151040
    Tool has finished execution.  Errors encountered: 0
    C:\Program Files\Microsoft Lync Server 2013\ResKit\StorageService>
```
## DBAnalyze

## Descrizione

DBAnalyze è uno strumento da riga di comando che consente agli amministratori di raccogliere rapporti di analisi sui database di Lync Server 2013. DBAnalyze include le modalità seguenti: diagnostica, dati utente, conferenza, MCU e frammentazione dischi:

  - **Modalità diagnostica**   Crea un rapporto contenente informazioni relative a tabelle (numero di record, frammentazione, dimensioni dei dati e dimensioni dell'indice), dimensioni dei file di log e dati, ora dell'ultimo backup, distribuzione dei contatti tra i server che eseguono Microsoft Office Communications Server, numero medio di autorizzazioni, contatti, contenitori, sottoscrizioni, pubblicazioni, endpoint per utente, eventuali utenti ospitati in modo non corretto, utenti che non è possibile instradare, numero medio di conferenze organizzate per utente, conferenze pianificate, conferenze attive e versione del database.
    

    > [!NOTE]
    > L'esecuzione in modalità diagnostica può incidere sulle prestazioni del server.



  - **Modalità dati utente**  Crea rapporti sui dati relativi a contatto, contenitore, sottoscrizione, pubblicazione, autorizzazione e gruppi di contatti per un determinato utente e per gli utenti nei cui elenchi di contatti e autorizzazioni è presente tale utente. In questa modalità vengono anche creati rapporti sui dati di riepilogo per le conferenze organizzate da un utente o a cui l'utente è stato invitato.

  - **Modalità conferenza**   Crea un rapporto con dati dettagliati su una specifica conferenza, inclusi tutti i dettagli sull'orario di pianificazione per la conferenza, l'elenco degli inviati, l'elenco dei tipi di contenuto multimediale consentiti per la conferenza, le unità MCU (Multipoint Control Unit) attive, l'elenco di partecipanti attivi e lo stato di segnalazione dei singoli partecipanti.

  - **Decodifica ID riunione**  Decodifica un ID riunione PSTN (Public Switched Telephone Network) specificato dall'opzione **/pstnid** ma non esegue la connessione al back-end per informazioni dettagliate.

  - **Risoluzione conferenza**   Decodifica un ID riunione PSTN specificato dall'opzione **/pstnid** e visualizza informazioni sulla conferenza identificata dall'ID.

  - **Modalità MCU**  Segnala ID, tipo di contenuto multimediale, URL, stato heartbeat, carico di conferenza e carico di partecipanti per ogni unità MCU nel pool.

  - **Modalità frammentazione dischi**  Visualizza lo stato di frammentazione di tutti i dischi.

Questo strumento può essere utilizzato per la diagnostica di diversi problemi o per assistere gli amministratori nelle attività di pianificazione della capacità. Ad esempio, se la maggior parte degli utenti ospitati sul server A sceglie utenti ospitati sul server B come contatti, l'amministratore può spostare sul server B gli utenti presenti sul server A per ridurre il traffico tra i server.

## Output

Questo strumento restituisce rapporti predefiniti sul database di Lync Server 2013. **Percorso:** %ProgramFiles%\\Microsoft Lync Server 2013\\Reskit

## Scopo

Per installare Dbanalyze.exe, copiarlo in una cartella locale ed eseguire lo strumento. Per utilizzare lo strumento, eseguire il comando seguente dalla riga di comando.`dbanalyze.exe [/v] [/report:value] [/sqlserver:value] [/user:user@domain.com] [/conf:value][/pstnid:Value] [/maxcontacts:value]` Di seguito sono riportate le descrizioni relative alle opzioni della riga di comando.

![Opzioni della riga di comando per Dbanalyze.exe.](images/JJ945604.22bf3432-af6d-495b-8f48-d94c5d259523(OCS.15).jpg "Opzioni della riga di comando per Dbanalyze.exe.")

## Requisiti

**Computer** DBAnalyze può essere eseguito solo da un computer aggiunto a un dominio in cui è installato Lync Server 2013.

**Rete** Il computer deve essere in grado di connettersi al database back-end.

**Software** Prima di eseguire DBAnalyze è necessario installare i componenti software di Lync Server 2013.

**Utenti**Nella tabella seguente sono indicati gli amministratori che dispongono delle autorizzazioni necessarie per accedere ai database di Lync Server 2013.

![Tabella di autorizzazioni per Dbanalyze.exe.](images/JJ945604.b8931e9e-834e-4dec-8a84-2fc47d1613e9(OCS.15).jpg "Tabella di autorizzazioni per Dbanalyze.exe.")


> [!NOTE]
> È necessario un account di amministratore locale per la modalità <STRONG>/report:disk</STRONG>.



## Esempi

Di seguito sono riportati alcuni esempi di comandi di Dbanalyze.exe validi:
```C++
    dbanalyze.exe /report:diag
    dbanalyze.exe /report:user /user:usera@domainb.com
    dbanalyze.exe /report:conf /user:bob@example.com /conf:1W9J71SKSX2X
    dbanalyze.exe /report:resolve /pstnid:12345
    dbanalyze.exe /report:mcus
    dbanalyze.exe /report:disk
```
## Riepilogo

DBAnalyzer offre agli amministratori un modo rapido e semplice per analizzare i database di Lync Server 2013.

## ImportStorageServiceData

Lo strumento ImportStorageServiceData del Resource Kit consente di reimportare nel servizio di archiviazione i dati relativi a coda ed endpoint che sono stati scaricati dal servizio di archiviazione (LYSS).

## Descrizione

Lo scaricamento dei dati dal servizio di archiviazione può essere avvenuto in modo automatico (periodico) in base allo stato dell'elemento della coda o alla dimensione del database. Può essersi verificato a seguito del richiamo manuale del cmdlet di failover del pool o del cmdlet StorageServiceFullFlush (richiamato dal cmdlet di failover del pool). Tenere presente che in teoria i dati non dovrebbero essere reimportati se la dimensione di un database del servizio di archiviazione (LYSS) sui server front-end è superiore al livello normale, poiché questo causerebbe probabilmente un aumento dei dati da riesportare. Inoltre, è necessario innanzi tutto risolvere i problemi che possono aver contribuito a causare gli errori che hanno determinato la crescita della coda del servizio di archiviazione, ad esempio errori degli endpoint di Exchange, errori di rete o problemi di altro tipo.

**Scenario 1:** durante il failover del pool, è possibile che vengano scaricati file dal servizio di archiviazione per ogni server front-end. Al termine del failover, è necessario eseguire lo strumento per reimportare i dati.

**Scenario 2:** i dati vengono scaricati automaticamente ogni giorno o in seguito al superamento di determinate soglie di dimensione del database del servizio di archiviazione, ad esempio 60%, 80%, 90% o completo. Questi dati scaricati automaticamente devono essere reimportati periodicamente dall'amministratore. Nella situazione descritta sopra, se non viene distribuito il pacchetto SCOM di monitoraggio, sono presenti eventi per il servizio di archiviazione di Lync Server correlati ai dati scaricati dal servizio di archiviazione, con ID evento 32075 (operazione di scaricamento completo avviata), 32076 (scaricamento completato), 32082 (scaricamento a livello di manutenzione avviato), 32083 (scaricamento a livello di manutenzione completato) e 32089 (scaricamento a causa di esaurimento dello spazio nel database). Si noti che questi ID evento corrispondono alla versione RTM. Quando un amministratore visualizza questi eventi, significa che alcuni file sono stati scaricati. Questi dati devono essere reimportati periodicamente mediante questo strumento, ad esempio una volta alla settimana.

Per la service release Online, se viene distribuito il pacchetto SCOM di monitoraggio dello stato per Lync Server, è possibile che vengano generati nuovi avvisi che richiedono all'amministratore di reimportare i dati scaricati nel servizio di archiviazione. Nel registro eventi nel server front-end che ha generato l'avviso sarà presente un evento corrispondente. Nell'evento verrà fornita una descrizione del percorso padre in cui sono situati i dati scaricati e sarà indicato il numero di file che soddisfano i criteri dell'avviso. I criteri dell'avviso prevedono che siano presenti X o più file nel percorso padre specifico che hanno almeno Y giorni (dove X e Y sono valori preimpostati all'interno del servizio di archiviazione ma possono essere sostituiti modificando il file APPCONFIG). Di seguito sono riportati due esempi di eventi che possono generare l'avviso di stato, in cui la differenza è rappresentata dal relativo percorso padre. Una possibilità è rappresentata dalla condivisione file del servizio Web, mentre l'altra è la directory Application Data locale per ogni server front-end, ad esempio c:\\Programmi\\Microsoft\\Lync Server\\StorageService. L'amministratore eseguirà quindi questo strumento del Resource Kit.

Questo strumento incrementa il carico della CPU e di IO sul server front-end su cui è in esecuzione, nonché sugli altri, laddove i dati non sono di proprietà del front-end su cui viene eseguito lo strumento. È consigliabile eseguire questo strumento quando il carico della CPU e di IO dei server front-end non è elevato, ad esempio fuori dalle ore di punta. In secondo luogo, l'importazione di un file di dati può richiedere 2-3 minuti. Tenerne conto quando si stima la durata di esecuzione dello strumento. Il file di log dettagliato generato dallo strumento sarà presente per impostazione predefinita nell'archivio file. Eliminarlo se non sono segnalati errori perché le dimensioni del file di log possono giungere a decine di MB o più.

![Esempio di eventi nel registro eventi del server di archiviazione.](images/JJ945604.3a903ef7-ea8a-4606-8229-a3e32f13af3a(OCS.15).jpg "Esempio di eventi nel registro eventi del server di archiviazione.")

## Requisiti

Installare Lync Server 2013, Strumenti del Resource Kit Lo strumento viene eseguito nei computer aggiunti al dominio in cui sono installati Lync Server e Lync Server Management Shell. Lo strumento utilizza un cmdlet dalla shell di gestione per identificare tutti i server front-end nel pool. In secondo luogo, lo strumento deve essere eseguito da un computer nel pool in cui è installato il database **RtcLocal**. Questo database viene utilizzato dallo strumento per recuperare la posizione della condivisione file WEBSERVICE per il pool. Inoltre, prima di utilizzare lo strumento, è necessario che ogni server front-end abiliti la comunicazione remota di Windows PowerShell mediante **Enable-PSRemoting** su ogni server front-end, nonché sul computer da cui viene eseguito lo strumento. In caso contrario, i comandi di Windows PowerShell da remoto da questo strumento avranno esito negativo. Al termine, la comunicazione remota di Windows PowerShell può essere disattivata su tutti i server front-end nel pool. Infine, l'account o la credenziale che richiama lo strumento deve disporre dell'autorizzazione di lettura/scrittura sulla condivisione file webservice per il pool su cui viene eseguito lo strumento. In caso contrario, lo strumento avrà esito negativo con errori di autorizzazione IO.


> [!NOTE]
> In Windows Server 2012 la comunicazione remota di Windows PowerShell è abilitata per impostazione predefinita, ma non sul sistema operativo Windows Server 2008.



## Esempi
```C++
    >  C:\StorageService>ImportStorageServiceData.exe
    Description:
    This tool will re-import Storage Service (LYSS) flushed queue data back in.  For a pool: you are required to run this tool on a machine inside the pool which has the Lync Server Management Shell installed.  Additionally, all front end machines need to have Windows Powershell Remoting enabled before executing this tool by executing Enable-PSRemoting.  Also, please ensure that all Storage Service instance DB Size are at the 'Normal' level (verify this by viewing Eventlog events). Otherwise re-importing may cause data to be flushed out again if any Storage Service instance DB size level goes above 'Normal'.
    Usage: Default behavior is to Import data from web service file share as well as any files on all Front End machines in pool.
    Additional Options:
    -Verbose                    : Turn verbose output on.
    
    -StorageServiceHostName     : Host Name of Storage Service WCF endpoint.  ( Default=localhost netnamedpipe binding. )
                                        
    -FileSharePath              : Import only all data from just under the UNC path specified.
    
    ActivityID: cc3b62ff-bb66-4e61-a6e2-96cb3626315c. <-- Use this to correlate with StorageService trace logs if troubleshooting.
    Type Server name (TCP binding) or press <enter> for localhost (NamePipe binding):
    Using NetNamedPipeBinding...
    OnTopologyChanged Event received
    Web Service File Share: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService
    
    Front Ends:
    server.vdomain.com
    server2.vdomain.com
    server1.vdomain.com
    server3.vdomain.com
    Looking under directory: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService for exported data.
    # Files found: 8
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    Items deserialized: 20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER.vdomain.com\944f5724c65c5f93900dc1c8c898b102__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server1.vdomain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER1.vdomain.com\17d5435ae40259f7bbdf1866776386e4__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d3832e4__0.xml
    
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server1.vdomain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d
    3832e4__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER1.vdomain.com\904f6c9b8ac951ae8b3c
    86684d3832e4__0.xml
    
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER1.vdomain.com\904f6c9b8ac951ae8b3c86684d3832e4__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42287dd6__0.xml
    
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server2.vdom
    ain.com, queueItems=20
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42
    287dd6__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER2.vdomain.com\69844a271e6c5633a1f2
    b46a42287dd6__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER2.vdomain.com\69844a271e6c5633a1f2b46a42287dd6__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\3313935458e35b9b9759e08a15d251e6__0.xml
    
    Items deserialized: 20
    
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=1
    
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\3313935458e35b9b9759e08a15
    d251e6__0.xml
    
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\3313935458e35b9b9759
    e08a15d251e6__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\3313935458e35b9b9759e08a15d251e6__0.xml: succeeded: 20, failed: 0
    
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\4501e04eae4856059346949ff817c220__0.xml
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=1
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\4501e04eae4856059346949ff8
    17c220__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\4501e04eae4856059346
    949ff817c220__0.xml
    
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\4501e04eae4856059346949ff817c220__0.xml: succeeded: 20, failed: 0
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\5ad77443ad955a22a876749be66d5317__0.xml
    
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=20
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\5ad77443ad955a22a876749be6
    6d5317__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\5ad77443ad955a22a876
    749be66d5317__0.xml
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\5ad77443ad955a22a876749be66d5317__0.xml: succeeded: 20, failed: 0
    Starting Import for file:\\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\2
    0120910\SERVER3.vdomain.com\a11e27ae439a582288d4657eda86b565__0.xml
    Items deserialized: 20
    [cc3b62ff-bb66-4e61-a6e2-96cb3626315c] Send EnqueueMessages to redirected, targetServer=server3.vdom
    ain.com, queueItems=20
    All items in file were enqueued successfully, will try to delete file: \\dc.vdomain.com\OcsFileStore
    \co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\a11e27ae439a582288d4657eda
    86b565__0.xml
    All items in file failed to enqueue so file will not be deleted.  File path: \\dc.vdomain.com\OcsFil
    eStore\co1-WebServices-1\StorageService\DataExport\20120910\SERVER3.vdomain.com\a11e27ae439a582288d4
    657eda86b565__0.xml
    Summary for file \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\DataExport\20120910\
    SERVER3.vdomain.com\a11e27ae439a582288d4657eda86b565__0.xml: succeeded: 20, failed: 0
    All files have been imported into Storage Service for path: \\dc.vdomain.com\OcsFileStore\co1-WebSer
    vices-1\StorageService
    Importing files for: server.vdomain.com
    No files founds.
    Importing files for: server2.vdomain.com
    No files founds.
    Importing files for: server1.vdomain.com
    No files founds.
    Importing files for: server3.vdomain.com
    No files founds.
    Writing log: \\dc.vdomain.com\OcsFileStore\co1-WebServices-1\StorageService\ImportStorageServiceData
    Log20120910_1609SS
    Tool has finished execution.
    >  C:\StorageService>
```
## LCSSync

Lo strumento LCSSync consente di distribuire il software di comunicazione Lync Server 2013 in un ambiente a più foreste. Questo strumento viene utilizzato per sincronizzare utenti e gruppi di diverse foreste di utenti come un oggetto contatto di Servizi di dominio Active Directory in una foresta centrale in cui è installato Lync Server 2013.

## Descrizione

LCSSync utilizza l'oggetto contatto di Servizi di dominio Active Directory sincronizzato nella foresta centrale per abilitare gli utenti per Lync Server. Per fornire l'accesso unico, è necessario che l'account utente primario sia mappato all'oggetto contatto di Servizi di dominio Active Directory nella foresta centrale per Lync Server 2013. Questo strumento consente di eseguire tale mapping. Lo strumento fornisce modelli per la creazione di agenti di gestione in Microsoft Identity Integration Server.

## Riepilogo

Lo strumento LCSSync consente di distribuire Lync Server in un ambiente a più foreste.

## LookupUserConsole

Lo strumento LookupUserConsole visualizza informazioni di routing interne di Lync Server su specifici utenti. Queste informazioni possono essere utili per il personale di supporto Microsoft per la diagnostica dei problemi di distribuzione e routing.

## Descrizione

Quando si esegue LookupUserConsole.exe viene aperto un prompt dei comandi che accetta indirizzi SIP e tenta di visualizzare informazioni di routing interne di Lync Server ad essi correlate. Digitare **exit** per chiudere lo strumento LookupUserConsole.

## Requisiti

Installare Lync Server 2013, Strumenti del Resource Kit Lo strumento viene eseguito nei computer aggiunti al dominio in cui è installato Lync Server.

## Esempi

C:\\Programmi\\Microsoft Lync Server 2013\\ResKit\>LookupUserConsole.exe
```C++
    > sip:john.doe@vdomain.com
    
      Execution time (ms):                            171.094
      Exeuction result:                               Success
      SIP URI:                                        sip:john.doe@vdomain.com
      User info:
        SID:                                          S-1-5-21-2831376166-29632525...    Display name:                                     John Doe
        Grouping ID:                                  00000000-0000-0000-0000-...
        Line URI:                                     <null>
        Policy assignment:                            TenantId={00000000--0000-000....
        SIP enabled:                                  True
        UC enabled:                                   False
        Tenant ID:                                    00000000-0000-0000-0000-...  Cluster info:
        Active cluster:                               pool0.vdomain.com
        Backup registrar cluster:                     <null>
        Deployment location:                          <null>
        Home Front-End FQDN:                          SERVER.vdomain.com
        Primary Registrar cluster:                    pool0.vdomain.com
        Remote Director external SIP FQDN:            <null>
        Remote Director internal SIP FQDN:            <null>
        Remote Director Web FQDN:                     <null>
        Routing group ID:                             4501e04e-ae48-5605-9346...
        Service tag ID:                               1266953005
        User Front-End resolved:                      True
        User in local forest:                         True
        User in remote forest:                        False
        User in split domain:                         False
        User-Services cluster:                        pool0.vdomain.com
    
    > sip:nouser@vdomain.com
    
      Execution time (ms):                            948.7574
      Exeuction result:                               UserDoesNotExist
    
    > exit
```
## MsTurnPing

Lo strumento MSTurnPing consente a un amministratore del software per le comunicazioni Microsoft Lync Server 2013 di controllare lo stato dei server che eseguono i servizi Audio/Video Edge e Audio/Video Authentication, nonché dei server che eseguono i servizi Bandwidth Policy Services nella topologia.

## Descrizione

Lo strumento MSTurnPing consente a un amministratore del software per le comunicazioni Lync Server 2013 di controllare lo stato dei server che eseguono i servizi Audio/Video Edge e Audio/Video Authentication, nonché dei server che eseguono i servizi Bandwidth Policy Services nella topologia.

Lo strumento consente all'amministratore di eseguire i test seguenti:

1.  Test dei server A/V Edge Server. Lo strumento esegue test su tutti i server A/V Edge Server nella topologia nel modo seguente:
    
      - Verifica che il servizio Audio/Video Authentication di Lync Server sia avviato e in grado di rilasciare credenziali appropriate.
    
      - Verifica che il servizio Audio/Video Edge di Lync Server sia avviato e in grado di allocare correttamente le risorse sul perimetro esterno.

2.  Test del servizio criteri larghezza di banda. Lo strumento esegue test su tutti i server che eseguono i servizi criteri larghezza di banda nella topologia nel modo seguente:
    
      - Verifica che il servizio criteri larghezza di banda (Autenticazione) di Lync Server sia avviato e in grado di rilasciare credenziali appropriate.
    
      - Verifica che il servizio criteri larghezza di banda (Core) di Lync Server sia avviato e in grado di eseguire correttamente il controllo della larghezza di banda.

Questo strumento deve essere eseguito da un computer incluso nella topologia e in cui sia installato l'archivio locale.

## Output

Lo strumento restituisce i risultati di ognuna delle operazioni.

  - Se viene eseguito il test **AudioVideoEdgeServer**, l'output dello strumento è il seguente:
    
      - Risultati del test dei computer che forniscono il servizio Autenticazione audio/video Lync Server nella topologia
    
      - Risultati del test dei computer che forniscono il servizio Lync Server Audio/Video Edge nella topologia

  - Se viene eseguito il test **BandwidthPolicyServer**, l'output dello strumento è il seguente:
    
      - Risultati del test dei computer che forniscono il servizio criteri larghezza di banda (Autenticazione) di Lync Server nella topologia
    
      - Risultati del test dei computer che forniscono il servizio criteri larghezza di banda (Core) di Lync Server nella topologia

## Requisiti

  - Questo strumento deve essere eseguito da un computer incluso nella topologia e che contenga l'archivio locale.

  - Deve essere eseguito come amministratore con autorizzazione di accesso all'archivio locale.

## Esempi

Di seguito è riportato un esempio di input dello strumento.
```C++
    MsTurnPing -ServerRole AudioVideoEdgeServer
    
    MsTurnPing -ServerRole BandwidthPolicyServer
```
## Riepilogo

Questo strumento può essere una risorsa preziosa per gli amministratori di Lync Server 2013 che intendono controllare lo stato dei server in cui sono in esecuzione i servizi audio/video e criteri di larghezza di banda.

## Network Configuration Viewer

Network Configuration Viewer può essere utilizzato dagli amministratori del software di comunicazione Lync Server 2013 per visualizzare la topologia di rete Controllo di ammissione di chiamata per un'azienda il cui provisioning consente le sessioni di comunicazione in tempo reale, quali ad esempio chiamate vocali o videochiamate, in base alla capacità di larghezza di banda specificata. Gli amministratori di Lync Server 2013 definiscono i criteri di controllo di ammissione di chiamata, che vengono applicati dai servizi criteri larghezza di banda installati con Microsoft Lync Server 2013.

## Descrizione

Network Configuration Viewer (NetworkConfigurationViewer.exe) consente agli amministratori di eseguire le attività seguenti:

  - Caricare e visualizzare in formato grafico la topologia di rete Controllo di ammissione di chiamata da una distribuzione di Lync Server 2013.

  - Caricare e visualizzare in formato grafico la topologia di rete Controllo di ammissione di chiamata da un file di log del server criteri larghezza di banda.

  - Salvare e archiviare la topologia di rete Controllo di ammissione di chiamata in formato XML sul disco.

  - Salvare e archiviare il diagramma della topologia di rete Controllo di ammissione di chiamata in formato JPG o BMP.

  - Visualizzare i dati di configurazione della topologia di rete Controllo di ammissione di chiamata.

  - Visualizzare la topologia di rete Controllo di ammissione di chiamata in uno stile di visualizzazione ad albero.

  - Definire connettori personalizzati per i collegamenti della topologia di rete Controllo di ammissione di chiamata, ad esempio i collegamenti sito-area, area-area e sito-sito.

  - Visualizzare informazioni sui siti, informazioni sulle aree, criteri di larghezza di banda di cui è stato eseguito il provisioning e collegamenti di rete per la topologia di rete Controllo di ammissione di chiamata.

## Scopo

Visualizzare i collegamenti della topologia di rete Controllo di ammissione di chiamata aziendale in un'interfaccia grafica.

## Esempi

**Caricare e visualizzare in formato grafico la topologia di rete Controllo di ammissione di chiamata da una distribuzione di Lync Server 2013:** gli amministratori di Lync Server 2013 possono caricare e visualizzare la configurazione della topologia di rete Controllo di ammissione di chiamata su qualsiasi computer Lync Server 2013 utilizzando l'opzione **Download Network Configuration** mostrata nella figura seguente. Lo strumento non è in grado di scaricare o visualizzare tale configurazione quando è distribuito su un computer privo di connettività all'archivio di configurazione di Lync.

![Download della configurazione di rete.](images/JJ945604.8d126d3f-2545-4f13-a244-974f09614982(OCS.15).jpg "Download della configurazione di rete.")

**Caricare e visualizzare in formato grafico la topologia di rete Controllo di ammissione di chiamata da un file di log del server criteri larghezza di banda:** i server criteri larghezza di banda di Lync Server 2013 salvano la topologia di rete Controllo di ammissione di chiamata come parte del meccanismo di registrazione nel percorso della condivisione file di Lync Server 2013. Gli amministratori di Lync Server possono visualizzare tale file in formato grafico utilizzando l'opzione **Open Network Configuration** mostrata sotto.

![Apertura di un file di log del server criteri larghezza di banda.](images/JJ945604.3e503e92-aacb-4921-a8d2-23f860fe2df6(OCS.15).jpg "Apertura di un file di log del server criteri larghezza di banda.")

Salvare e archiviare la topologia di rete Controllo di ammissione di chiamata in formato XML sul disco: gli amministratori di Lync Server 2013 possono salvare il file di configurazione della topologia di rete Controllo di ammissione di chiamata in formato XML utilizzando l'opzione **Save a copy of Network Configuration** mostrata sotto. Il file di configurazione salvato può quindi essere utilizzato offline per la visualizzazione in formato grafico.

![Salvataggio della configurazione di rete come file XML.](images/JJ945604.6eeef3b0-78b5-4ee6-8d94-1a4ddf3d8676(OCS.15).jpg "Salvataggio della configurazione di rete come file XML.")

Salvare e archiviare il diagramma della topologia di rete Controllo di ammissione di chiamata in formato JPG o BMP: gli amministratori di Lync Server 2013 possono salvare la configurazione della topologia di rete Controllo di ammissione di chiamata in formato grafico (formati di file JPG e BMP) utilizzando l'opzione **Save Network Configuration diagram as picture** mostrata sotto.

![Salvataggio della configurazione di rete come immagine.](images/JJ945604.145a6fb9-58b1-46b1-bbd5-a661ceba07b4(OCS.15).jpg "Salvataggio della configurazione di rete come immagine.")

**Visualizzare i dati di configurazione della topologia di rete Controllo di ammissione di chiamata:gli amministratori di**Lync Server 2013 possono visualizzare dati della configurazione di rete correlati, ad esempio aree di rete, siti di rete, profili di larghezza di banda e indirizzi IP della subnet del sito in formato testo utilizzando l'opzione View Network Configuration data mostrata sotto.

![Visualizzazione dei dati sulla configurazione di rete.](images/JJ945604.b72a4c21-a042-4d91-bf96-fcb396af0679(OCS.15).jpg "Visualizzazione dei dati sulla configurazione di rete.")

**Visualizzare la topologia di rete Controllo di ammissione di chiamata in uno stile di visualizzazione ad albero:** gli amministratori di Lync Server 2013 possono visualizzare dati della configurazione di rete correlati in una visualizzazione grafica ad albero utilizzando il pannello di controllo sulla sinistra della finestra dello strumento, come mostrato sotto.

![Visualizzazione dei dati sulla configurazione di rete in una visualizzazione ad albero.](images/JJ945604.4d924ac9-fd96-430f-b211-ee35b7ef9a23(OCS.15).jpg "Visualizzazione dei dati sulla configurazione di rete in una visualizzazione ad albero.")

**Definire connettori personalizzati per i collegamenti della topologia di rete Controllo di ammissione di chiamata, ad esempio i collegamenti sito-area, area-area e sito-sito:** gli amministratori di Lync Server 2013 possono definire connettori grafici personalizzati per i collegamenti WAN della configurazione di rete Controllo di ammissione di chiamata utilizzando l'opzione Settings mostrata sotto. Questo consente di distinguere i vari tipi di collegamenti di rete di cui è stato eseguito il provisioning nella configurazione di rete.

![Definire i connettori personalizzati per la topologia di rete Controllo di ammissione di chiamata](images/JJ945604.b20bea67-c8e1-453e-b1dd-e2aa17b62566(OCS.15).jpg "Definire i connettori personalizzati per la topologia di rete Controllo di ammissione di chiamata")

**Visualizzare informazioni sui siti, informazioni sulle aree e i criteri di larghezza di banda di cui è stato eseguito il provisioning per la topologia di rete Controllo di ammissione di chiamata:** gli amministratori di Lync Server 2013 possono visualizzare informazioni correlate sulle aree della rete Controllo di ammissione di chiamata, sui siti e sul provisioning di larghezza di banda per Controllo di ammissione di chiamata utilizzando le opzioni mostrate sotto. Ad esempio, è possibile fare clic su **Info** in un oggetto area di rete o sito di rete.

![Definizione di connettori personalizzati per la rete.](images/JJ945604.26262c75-4342-41c3-bc98-1793aa6a7713(OCS.15).jpg "Definizione di connettori personalizzati per la rete.")

## Riepilogo

Questo strumento può essere una risorsa preziosa per gli amministratori di Lync Server 2013 che desiderano visualizzare in formato grafico la topologia di rete Controllo di ammissione di chiamata per la propria distribuzione.

## Response Group Agent Live

L'applicazione Response Group consente agli agenti di accedere a utili informazioni in tempo reale utilizzando il relativo servizio Web incorporato. Purtroppo non è disponibile una visualizzazione grafica di questi dati all'esterno dell'applicazione. Lo strumento del Resource Kit Response Group Agent Live risolve questo problema fornendo una semplice soluzione grafica per accedere a queste informazioni, migliorata con informazioni del software di comunicazione Microsoft Lync 2013 in tempo reale, quali la presenza degli altri agenti.

## Descrizione

Response Group Agent Live è un'applicazione Windows che fornisce funzionalità di accesso e disconnessione e alcune informazioni in tempo reale, ad esempio l'appartenenza ai gruppi e il numero corrente di chiamate, agli agenti di Response Group. Si tratta di una versione avanzata della pagina Agent Groups, a cui è possibile accedere da Lync 2013.

## Scopo

L'applicazione Response Group accoda le chiamate in arrivo, quindi le instrada ai gruppi di agenti. Per ottimizzare il processo decisionale sulle chiamate da gestire, gli agenti possono accedere a informazioni in tempo reale sui propri gruppi di agenti, ad esempio quali agenti sono disponibili e quante chiamate sono in attesa in ogni coda Queste informazioni, inizialmente accessibili solo mediante il servizio Response Group, sono rese disponibili in modo intuitivo da Response Group Agent Live.

## Funzionalità

Lo strumento Response Group Agent Live è basato sul servizio Response Group e sull'SDK di Microsoft Lync 2013. Fornisce agli agenti di Response Group le informazioni e le funzionalità rese disponibili dal servizio Response Group, quali l'appartenenza a gruppi, la presenza degli altri agenti e il numero di chiamate in attesa.

Nella figura seguente è illustrata l'interfaccia principale di Response Group Agent Live.

![Strumento Response Group Agent Live.](images/JJ945604.63cb0374-a6ef-4a59-b60e-bec86a880d09(OCS.15).jpg "Strumento Response Group Agent Live.")

Sono disponibili le seguenti tre funzionalità principali per agenti in Response Group Agent Live:

  - **Accesso/disconnessione:** diversamente dalla pagina Agent Groups (accessibile da Lync 2013), Response Group Agent Live consente agli agenti di eseguire solo l'accesso o la disconnessione da tutti i gruppi di agenti contemporaneamente. Per eseguire rapidamente l'accesso o la disconnessione, gli agenti possono procedere in tre modi:
    
      - Fare clic sui pulsanti di accesso/disconnessione (verde e rosso) all'interno dell'applicazione.
    
      - Fare clic con il pulsante destro del mouse sull'icona sulla barra delle applicazioni e scegliere l'opzione per l'accesso o la disconnessione.
    
      - Utilizzare tasti di scelta rapida configurabili.

  - **Appartenenza al gruppo:** quando si seleziona un gruppo di agenti, Response Group Agent Live visualizza l'elenco degli agenti di tale gruppo nel riquadro destro. Se Lync 2013 e l'applicazione sono in esecuzione nello stesso computer, in Response Group Agent Live vengono visualizzate informazioni sulla presenza e la scheda contatto. Da qui gli agenti possono inviare un messaggio istantaneo o chiamare direttamente altri agenti.

  - **Statistiche in tempo reale:** Response Group Agent Live fornisce statistiche in tempo reale per tutti i gruppi di agenti. La frequenza di aggiornamento corrisponde a un minuto. Quando un Response Group risponde a una chiamata, viene aggiunto un indicatore visivo accanto al nome del gruppo con il numero corrente delle chiamate in coda. Posizionando il puntatore su un gruppo viene anche visualizzato il tempo di attesa più lungo.

## Requisiti

Response Group Agent Live richiede .NET Framework 4.0. Inoltre, per avvalersi delle funzionalità di presenza e scheda contatto, è necessario che Lync 2013 sia installato in locale e che sia in esecuzione.

## Configurazione

Response Group Agent Live può essere personalizzato in base alle proprie preferenze utilizzando la finestra delle opzioni nell'applicazione. Inoltre, l'amministratore può definire l'indirizzo host predefinito modificando direttamente la proprietà defaultHostAddress del file RGAgentLive.exe.config.

Nella figura seguente è illustrata la finestra di dialogo Options che gli agenti possono utilizzare per configurare l'indirizzo host e le combinazioni di tasti. A questa finestra di dialogo è possibile accedere facendo clic sul pulsante Options nella parte superiore destra dell'interfaccia principale.

![Finestra di dialogo Options di Response Group Agent Live.](images/JJ945604.3cc15e29-8699-45ab-90c3-e1565fa6ebf6(OCS.15).jpg "Finestra di dialogo Options di Response Group Agent Live.")

È possibile personalizzare le seguenti tre impostazioni nella configurazione di Response Group Agent Live:

  - Host address: corrisponde generalmente al nome di dominio completo del pool Web appartenente al pool principale dell'agente. L'indirizzo esatto del servizio Response Group viene ricavato automaticamente in background da queste informazioni, aggiungendo il percorso corretto dopo l'host.

  - Shortcuts: tasti di scelta rapida per l'accesso e la disconnessione da personalizzare. L'unica limitazione è data dal fatto che entrambe le combinazioni devono essere includere il tasto "Logo Windows" e almeno un altro tasto.

  - Start with Windows: l'applicazione può essere configurata per l'avvio automatico con Windows.

## Esempi

Nella figura seguente è illustrato come chiamare o inviare un messaggio istantaneo a un altro agente facendo clic con il pulsante destro del mouse sul contatto nel riquadro destro.

![Esecuzione di una chiamata o invio di un messaggio istantaneo.](images/JJ945604.009cebe0-5a93-4745-89c3-8a16c7c13009(OCS.15).jpg "Esecuzione di una chiamata o invio di un messaggio istantaneo.")

Nella figura seguente è mostrato come Response Group Agent Live visualizza il numero corrente di chiamate nella coda e il tempo di attesa più lungo tra tutte queste chiamate in arrivo.

![Visualizzazione di informazioni sulla coda.](images/JJ945604.131d7f79-b7ed-41f5-a9da-ffc556e31037(OCS.15).jpg "Visualizzazione di informazioni sulla coda.")

## Riepilogo

Accesso e disconnessione rapida, appartenenza ai gruppi e statistiche in tempo reale sono interessanti funzionalità di Response Group per gli agenti, disponibili solo all'esterno dell'applicazione tramite il servizio Response Group. Con lo strumento Response Group Agent Live del Resource Kit, gli amministratori di Lync possono fornire ai propri agenti un'applicazione Windows che consente loro di eseguire le proprie attività in modo più rapido e con un'interfaccia grafica.

## SEFAUtil

SEFAUtil (Secondary Extension Feature Activation Utility) è uno strumento da riga di comando che consente agli amministratori del software di comunicazione Microsoft Lync Server 2013 e agli agenti del supporto tecnico di configurare le funzioni di chiamata ai delegati, inoltro di chiamata e squillo simultaneo, le impostazioni di chiamata del team e la risposta alle chiamate di gruppo per conto di un utente di Lync Server 2013. Consente inoltre agli amministratori di eseguire query sulle impostazioni di routing delle chiamate pubblicate per un determinato utente. Con lo strumento SEFAUtil, gli amministratori possono abilitare/disabilitare/modificare l'inoltro di chiamata o lo squillo simultaneo per conto dell'utente. L'amministratore può specificare la destinazione, sotto forma di URI SIP, o utilizzare una destinazione già pubblicata dall'utente. Questo strumento consente inoltre agli amministratori di aggiungere o rimuovere delegati o membri del gruppo autorizzato alla risposta per conto dell'utente. Questo strumento è basato su Microsoft Unified Communications Managed API (UCMA) 3.0 e richiede la creazione di un'applicazione attendibile nell'archivio di gestione centrale per SEFAUtil

SEFAUtil (Secondary Extension Feature Activation Utility) consente agli amministratori di Lync Server 2013 e agli agenti del supporto tecnico di configurare le funzioni di chiamata ai delegati, inoltro di chiamata e squillo simultaneo, le impostazioni di intercettazione team e la risposta alle chiamate di gruppo per conto di un utente di Lync Server 2013. Consente inoltre agli amministratori di eseguire query sulle impostazioni di routing delle chiamate pubblicate per un determinato utente.

## Descrizione

La versione corrente di SEFAUtil è solo uno strumento da riga di comando. Non è disponibile un'interfaccia utente grafica di supporto. Lo strumento è basato su Microsoft Unified Communications Managed API (UCMA) 3.0. Le funzionalità incluse nello strumento consentono agli amministratori e agli agenti del supporto tecnico di eseguire le attività seguenti:

  - Visualizzare tutte le impostazioni di routing delle chiamate per un utente, inclusi l'inoltro di chiamata, la delega, lo squillo simultaneo, intercettazione team e risposta alle chiamate di gruppo.

  - Abilitare/disabilitare/modificare l'impostazione di inoltro di chiamata, inclusi la destinazione e il timer di mancata risposta

  - Abilitare/disabilitare/modificare le configurazioni immediate di inoltro di chiamata

  - Abilitare/disabilitare/modificare le impostazioni di delega

  - Abilitare/disabilitare/modificare le impostazioni del gruppo autorizzato alla risposta
    

    > [!NOTE]
    > Novità dello strumento SEFAUtil di Lync Server 2013



  - Abilitare/disabilitare/modificare le impostazioni dello squillo simultaneo, incluse le destinazioni
    

    > [!NOTE]
    > Novità dello strumento SEFAUtil di Lync Server 2013



  - Abilitare/disabilitare/modificare le impostazioni di risposta alle chiamate di gruppo
    

    > [!WARNING]
    > Novità dello strumento SEFAUtil di Lync Server 2013



Questo strumento presenta le limitazioni seguenti:

  - È supportato solo per gli utenti ospitati in un pool di Lync Server

  - Non è supportata la modifica in blocco delle impostazioni di routing delle chiamate per diversi utenti

## Output

L'output della versione corrente dello strumento è fornito solo nella finestra del prompt dei comandi. Per informazioni dettagliate, vedere la sezione Esempi più avanti in questo documento.

## Scopo

Di seguito sono illustrati alcuni scenari chiave in cui può essere utilizzato questo strumento:

  - Alberto è un dirigente ed è stato trasferito al sistema di telefonia Lync Server. Dispone della delega sul sistema PBX esistente. Nel contesto del passaggio a Lync, l'amministratore può configurare il routing di Alberto in modo da riflettere la sua configurazione di delega preesistente.

  - Alice è in trasferta e si rende conto di attendere una chiamata importante da un cliente. Si trova tuttavia in un hotel, senza la possibilità di accedere a un computer. Chiama il supporto tecnico e chiede che tutte le chiamate in arrivo al suo telefono dell'ufficio vengano inoltrate al suo cellulare. Il personale del supporto tecnico può effettuare la configurazione per suo conto.

  - Le chiamate in arrivo sul telefono dell'ufficio di Franco vengono trasferite alla segreteria del suo cellulare quando è al lavoro; tutto sembra invece funzionare correttamente nella maggior parte degli altri luoghi. L'addetto del supporto tecnico riesce a visualizzare la configurazione di routing di Franco e scopre che per il suo telefono cellulare è configurato lo squillo simultaneo. L'addetto chiede a Franco informazioni sulla copertura cellulare in ufficio e scopre che è la regola dello squillo simultaneo a causare il trasferimento delle chiamate alla segreteria del cellulare di Franco quando la copertura di rete è scarsa.

  - Diego è un nuovo dipendente di Contoso ed è stato inserito in un nuovo team in cui tutti i membri sono configurati per l'intercettazione team. Quando viene abilitato per Microsoft Lync, l'amministratore è in grado di configurare le sue impostazioni del gruppo autorizzato alla risposta in modo da includere tutti i membri del suo nuovo team. Inoltre, l'amministratore aggiunge Diego come membro del gruppo autorizzato alla risposta per tutti i membri del suo team.

  - Una prassi del servizio clienti presso il reparto risorse umane di Contoso prevede l'assistenza personale per tutti i chiamanti fin dalla prima chiamata. Dato che tutti i membri del reparto si trovano fisicamente vicini tra loro, se tutti i telefoni suonassero contemporaneamente con l'intercettazione team, questo rappresenterebbe un disturbo per il team. Per assicurare un servizio ottimale senza disturbare i membri del team, l'amministratore di Lync si avvale della funzionalità di risposta alle chiamate di gruppo. L'amministratore aggiunge tutti i membri del reparto a un gruppo di risposta e comunica al reparto il numero del gruppo di risposta. Quando Raffaella non si trova alla sua scrivania, Franco nota che il suo telefono squilla e risponde alla chiamata dalla propria postazione.

## Requisiti

Lo strumento SEFAUtil può essere eseguito solo su un computer appartenente a un pool di applicazioni attendibili. Su tale computer deve essere installato UCMA 3.0. Per eseguire lo strumento, è necessario che su tale pool venga creata una nuova applicazione attendibile con l'ID applicazione di SEFAUtil.

**Creazione di una nuova applicazione attendibile per lo strumento SEFAUtil**

1.  Lo strumento SEFAUtil può essere eseguito solo su un computer appartenente a un pool di applicazioni attendibili. Se necessario, è possibile aggiungere un pool come nuovo pool di applicazioni attendibili utilizzando Lync Server Management Shell con il cmdlet seguente:
    ```C++
        New-CsTrustedApplicationPool -id <Pool FQDN> -Registrar <Pool Registrar FQDN> -site Site:<Pool Site>
    ```

    > [!NOTE]
    > UCMA 3.0 deve essere installato su tutti i computer che verranno utilizzati per eseguire lo strumento SEFAUtil.



2.  È necessario definire un'applicazione attendibile nella topologia per lo strumento SEFAUtil. Per definire SEFAUtil come nuova applicazione attendibile, utilizzare Lync Server Management Shell ed eseguire il cmdlet seguente:
    ```C++
        New-CsTrustedApplication -ApplicationId sefautil -TrustedApplicationPoolFqdn <Pool FQDN>  -Port 7489
    ```

    > [!NOTE]
    > Se necessario, è possibile utilizzare una porta diversa.



3.  È necessario che siano abilitate le modifiche alla topologia. Per abilitare le modifiche alla topologia, è possibile utilizzare Lync Server Management Shell eseguendo il cmdlet seguente:
    ```C++
        Enable-CsToplogy
    ```
4.  Se necessario, installare gli strumenti del Resource Kit di Lync Server 2013 nel server che verrà utilizzato per eseguire lo strumento SEFAUtil (il server deve far parte di un pool di applicazioni attendibili).

5.  Verificare che SEFAUtil venga eseguito correttamente. A questo scopo, eseguire lo strumento dal prompt dei comandi di Windows con privilegi di amministratore per visualizzare le impostazioni relative all'inoltro di chiamata di un utente nella distribuzione. Per impostazione predefinita, lo strumento si trova nel seguente percorso: “…\\Programmi\\Microsoft Lync Server 2013\\Reskit”. Per visualizzare le impostazioni relative all'inoltro di chiamata, utilizzare il comando seguente:
    ```C++
        SEFAUtil.exe <user SIP address> /server:<Lync Server/Pool FQDN>
    ```
    Verranno visualizzate le impostazioni di inoltro di chiamata dell'utente.

## Risposta alle chiamate di gruppo

Affinché la funzionalità di risposta alle chiamate di gruppo sia pienamente abilitata, sono necessarie alcune operazioni di configurazione supplementari in Lync Server. Prima di assegnare gruppi di risposta agli utenti, fare riferimento alla documentazione del prodotto per informazioni sulla pianificazione e sulle procedure di distribuzione di questa funzionalità.

## Esempi

## Visualizzare le impostazioni correnti di gestione delle chiamate

Il comando che segue consente di visualizzare la gestione delle chiamate per l'utente. `SEFAUtil.exe /server:lyncserver.contoso.com katarina@contoso.com`


> [!NOTE]
> In questo esempio viene utilizzata l'opzione <STRONG>/server</STRONG> per specificare il Lync Server a cui connettersi.



**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:20
    Call Forward No Answer to: voicemail
```
## Impostare la destinazione per inoltro di chiamata/mancata risposta

In questo esempio vengono impostati la destinazione per inoltro di chiamata/mancata risposta e il ritardo squilli. In questo caso non viene specificata l'opzione /server e SEFAUtil tenta di individuare automaticamente il Lync Server.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /enablefwdnoanswer /callanswerwaittime:30 /setfwddestination:+1425555 0126@contoso.com;user=phone
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: sip:+14255550126@contoso.com;user=phone
```
## Abilitare immediatamente l'inoltro di chiamata

In questo esempio viene abilitato immediatamente l'inoltro di chiamata a un altro utente.
```C++
    SEFAUtil.exe sip:katarina@contoso.com /enablefwdimmediate /setfwddestination:anders@contoso.com
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    Forward immediate to: sip:anders@contoso.com
```
## Disabilitare immediatamente l'inoltro di chiamata

In questo esempio viene disabilitato immediatamente l'inoltro di chiamata.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com katarina@contoso.com  /disablefwdimmediate
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail
```
## Aggiungere un utente come delegato e configurare lo squillo simultaneo dei delegati

In questo esempio viene aggiunto un utente come delegato e viene configurato lo squillo simultaneo dei delegati.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /adddelegate:joe@contoso.com /simulringdelegates
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simultaneously Ringing Delegates: sip:joe@contoso.com
```
## Modificare la regola di squillo simultaneo dei delegati

In questo esempio la regola di squillo simultaneo impostata nell'esempio precedente viene sostituita dalla regola di squillo ritardato.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /delayringdelegates:10
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    Delay Ringing Delegates (delay:10 seconds): sip:joe@contoso.com
```
## Rimuovere il delegato

In questo esempio viene rimosso il delegato.


> [!NOTE]
> Quando viene rimosso l'ultimo delegato, la chiamata ai delegati viene disabilitata automaticamente.


```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /removedelegate:joe@contoso.com
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail
```
## Aggiungere un delegato e configurare la regola di inoltro di chiamata ai delegati

In questo esempio viene aggiunto un delegato e viene impostata la regola di inoltro di chiamata ai delegati.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /adddelegate:anders@contoso.com /fwdtodelegates
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Forwarding calls to Delegates: sip:anders@contoso.com
```
## Abilitare lo squillo simultaneo e impostare un numero di destinazione

In questo esempio viene abilitato lo squillo simultaneo e viene impostato un numero di destinazione per lo squillo simultaneo.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /setsimulringdestination:+14255550126 /enablesimulring
```

> [!NOTE]
> Per cambiare il numero di destinazione dello squillo simultaneo di un utente per cui questa funzionalità è già abilitata, mantenere il comando con l'opzione /enablesimulring; in caso contrario, il numero di destinazione non verrà cambiato.



**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: True
    Simul_Ringing to: sip:+14255550126@contoso.com;user=phone
```
## Disabilitare lo squillo simultaneo

In questo esempio viene disabilitato lo squillo simultaneo.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disablesimulring
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Simulring enabled: False
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail
```
## Aggiungere un membro del team e configurare lo squillo simultaneo al gruppo autorizzato alla risposta

In questo esempio viene aggiunto un membro del team al gruppo autorizzato alla risposta di un utente e viene abilitato lo squillo simultaneo al gruppo autorizzato alla risposta.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /addteammember:anders@contoso.com /simulringteam
```

> [!NOTE]
> Quando si aggiunge un membro al gruppo autorizzato alla risposta di un utente, viene attivata automaticamente l'impostazione dello squillo simultaneo al gruppo autorizzato alla risposta dell'utente.



**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Team ringing enabled. Team: sip:anders@contoso.com
```
## Rimuovere un membro dal gruppo autorizzato alla risposta

In questo esempio viene rimosso un membro del gruppo autorizzato alla risposta di un utente.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /removeteammember:anders@contoso.com
```

> [!NOTE]
> Se il membro rimosso è l'unico componente del gruppo autorizzato alla risposta, viene disabilitato automaticamente lo squillo simultaneo al gruppo autorizzato alla risposta.



**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail
```
## Impostare lo squillo ritardato al gruppo autorizzato alla risposta

In questo esempio viene modificata l'impostazione del ritardo dello squillo al gruppo autorizzato alla risposta.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /delayringteam:5
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Delay Ringing Team (delay:5 seconds). Team: sip:anders@contoso.com
```
## Abilitare l'intercettazione team

In questo esempio viene abilitata l'intercettazione team per un determinato utente.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /simulringteam
```

> [!NOTE]
> Se il gruppo autorizzato alla risposta dell'utente non include alcun membro, l'intercettazione team non verrà abilitata.



**Output**

## Disabilitare l'intercettazione team

In questo esempio viene disabilitata l'intercettazione team per un determinato utente.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disableteamcall
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    User Ring time: 00:00:30
    Call Forward No Answer to: voicemail
```
## Abilitare la risposta alle chiamate di gruppo e assegnare un gruppo di risposta a un utente

In questo esempio viene assegnato un gruppo di risposta a un utente e viene abilitata la risposta alle chiamate di gruppo.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /enablegrouppickup:199
```
**Output**
```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
    Group Pickup Orbit: sip:199;phone-context=user-default@ contoso.com;user=phone
```
## Disabilitare la risposta alle chiamate di gruppo

In questo esempio viene disabilitata la risposta alle chiamate di gruppo per un determinato utente.
```C++
    SEFAUtil.exe /server:lyncserver.contoso.com sip:katarina@contoso.com /disablegrouppickup
```

> [!NOTE]
> Quando si disabilita la risposta alle chiamate di gruppo per un utente, il numero del gruppo assegnato all'utente non viene conservato. Se in seguito si desidera riabilitare la risposta alle chiamate di gruppo per tale utente, è necessario assegnare nuovamente il numero del gruppo con l'opzione /enablegrouppickup.


```C++
    User Aor: sip:katarina@contoso.com
    Display Name: Katarina Larsson
    UM Enabled: True
```
## SYSPrep.ps1

## Descrizione

SYSPrep.ps1 è uno script di Windows PowerShell che installa i seguenti prerequisiti di Lync Server 2013 in un computer con sistema operativo Windows Server 2008.

  - Microsoft .Net Framework 4.5

  - Microsoft SQL Server Express

  - Windows PowerShell versione 3.0

  - Visual C++ 2010 Redistributable

  - Aggiornamenti di Internet Information Server

  - Windows Identity Foundation

  - File principali di Lync Server 2013

Sebbene il nome dello script sia simile a quello dell'Utilità preparazione sistema dei sistemi operativi Microsoft Windows, svolgono funzioni differenti. Questo script installa solo i prerequisiti necessari per Lync Server 2013. Terminata l'installazione di tali prerequisiti, lo strumento Windows SYSPrep può essere utilizzato per creare un'immagine del server.

## Requisiti

Prima di eseguire lo script SYSPrep.ps1, è necessario copiare i file prerequisiti in una cartella locale nel computer con sistema operativo Windows Server 2008, ad esempio **D:\\Setup**. Questa cartella deve includere anche una copia dei file di Lync Server 2013, in particolare **Setup.exe.** Di seguito sono indicate le posizioni da cui è possibile scaricare i file prerequisiti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prerequisito</th>
<th>Posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft .Net Framework 4.5</p></td>
<td><p>http://go.microsoft.com/?linkid=9816306</p></td>
</tr>
<tr class="even">
<td><p>Microsoft SQL Server Express 2008 R2</p></td>
<td><p>http://www.microsoft.com/it-it/download/details.aspx?id=23650</p></td>
</tr>
<tr class="odd">
<td><p>Windows PowerShell versione 3.0</p></td>
<td><p>http://www.microsoft.com/en-us/download/details.aspx?id=34595</p></td>
</tr>
<tr class="even">
<td><p>Visual C++ 2010 Redistributable</p></td>
<td><p>http://www.microsoft.com/it-it/download/details.aspx?id=5555</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamenti di Internet Information Server</p></td>
<td><p>http://www.microsoft.com/it-it/download/details.aspx?id=34869</p></td>
</tr>
<tr class="even">
<td><p>Windows Identity Foundation</p></td>
<td><p>http://www.microsoft.com/it-it/download/details.aspx?id=17331</p></td>
</tr>
<tr class="odd">
<td><p>Setup.exe di Lync Server 2013</p></td>
<td><p>Copia dal supporto di Lync Server 2013</p></td>
</tr>
</tbody>
</table>


## Parametro

Il parametro **\\endash SetupFolder** accetta come argomento il percorso di directory dei file prerequisiti

## Esempi

Per eseguire lo script SYSPrep.ps1 e installare i prerequisiti di Lync Server 2013, eseguire il comando seguente dal prompt dei comandi con privilegi elevati:
```C++
    ./SysPrep.PS1 -SetupFolder D:\Setup
```
## Unassigned Number Announcements Migration

Lo strumento Unassigned Number Announcements Migration consente a un amministratore di Lync di spostare la configurazione dei numeri non assegnati gestiti dall'applicazione di annuncio da un server o pool di Lync di origine a un server o pool di Lync di destinazione.

## Descrizione

Lo strumento Unassigned Number Announcements Migration è uno script di Windows PowerShell che sposta la configurazione dei numeri non assegnati gestiti dall'applicazione di annuncio da un server o pool di Lync di origine a un server o pool di Lync di destinazione.

Quando viene eseguito lo script Unassigned Number Announcements Migration, vengono effettuate le operazioni seguenti:

1.  Tutti i file audio utilizzati dagli annunci di numeri non assegnati dell'applicazione di annuncio ospitata dal server o pool di origine vengono spostati nell'archivio file del server o pool di destinazione
    

    > [!NOTE]
    > dopo essere stati copiati nel pool di destinazione, i file audio vengono rimossi dal pool di origine.



2.  Tutti gli annunci di numeri non assegnati configurati per l'applicazione di annuncio ospitata nel server o pool di origine vengono spostati nel server o pool di destinazione.

3.  Tutti gli intervalli di numeri non assegnati gestiti dall'applicazione di annuncio ospitata nel server o pool di origine vengono riassegnati al server o pool di destinazione.

Dopo l'esecuzione dello script, tutti gli intervalli di numeri non assegnati che in precedenza erano gestiti dall'applicazione di annuncio ospitata nel server o pool di origine verranno gestiti con la stessa configurazione dal server o pool di destinazione.

## Output

Lo script **Move-CsAnnouncementConfiguration** indica l'esito positivo o negativo dell'operazione di migrazione nella finestra Lync Server Management Shell da cui viene eseguito.

Se l'operazione viene interrotta da un errore qualsiasi, gli intervalli di numeri non assegnati già spostati correttamente nella destinazione rimarranno nella destinazione in forma operativa e i restanti intervalli di numeri non assegnati di cui eseguire la migrazione rimarranno nell'origine, anch'essi in forma operativa. Per completare la migrazione del resto della configurazione, eseguire nuovamente lo script dopo avere risolto l'errore.

## Scopo

Lo script Unassigned Number Announcements Migration può essere utilizzato nei seguenti tre scenari:

  - **Migrazione delle impostazioni di configurazione a una nuova versione di Lync Server:** Contoso sta effettuando la migrazione a Lync Server 2013 e, nell'ambito del processo di migrazione, l'amministratore di Lync Server intende spostare la configurazione dei numeri non assegnati gestiti dall'applicazione di annuncio dalla distribuzione di Lync Server 2010 alla nuova distribuzione di Lync Server 2013. Per spostare le impostazioni di configurazione, l'amministratore di Lync Server utilizza lo strumento Unassigned Number Announcements Migration.

  - **Rollback di una distribuzione da Lync Server 2013 a Lync Server 2010:** Per motivi imprevisti, Contoso deve eseguire il rollback della migrazione alla nuova implementazione di Lync Server 2013. Per ridurre al minimo le interruzioni del servizio, l'amministratore di Lync Server utilizza lo strumento Unassigned Number Announcements Migration per eseguire il rollback della configurazione dalla distribuzione di Lync Server 2013 alla distribuzione di Lync Server 2010.

  - **Spostamento di dati tra distribuzioni di Lync:** Contoso ha avviato la sostituzione di tutti i server di un pool con nuovi server. La strategia consiste nel distribuire un nuovo pool di Lync Server 2013, spostare tutti i dati dal pool precedente a quello nuovo, per poi deprecare il pool precedente. Al termine della distribuzione del nuovo pool, viene utilizzato lo strumento Unassigned Number Announcements Migration per spostare la configurazione dal pool precedente a quello nuovo.

## Requisiti

Di seguito sono indicati i requisiti principali necessari per eseguire correttamente lo strumento:

1.  Lo script deve essere eseguito da un computer in cui è installato Lync Server 2013 Management Shell.

2.  L'applicazione di annuncio deve essere distribuita correttamente nei server o pool di Lync di origine e di destinazione.

## Script Move-CsAnnouncementConfiguration

Lo script Move-CsAnnouncementConfiguration richiede i due parametri descritti nella tabella riportata di seguito.

![Parametri di Move-CsAnnouncementConfiguration.](images/JJ945604.7ab66ad3-d0db-4d77-8b93-ebccf0cb0663(OCS.15).jpg "Parametri di Move-CsAnnouncementConfiguration.")

## Esempi

## Spostamento della configurazione degli annunci di numeri non assegnati da un pool di Lync Server 2010 a un pool di Lync Server 2013

In questo esempio vengono spostati gli annunci di numeri non assegnati dal pool di origine (Lync Server 2010) al pool di destinazione (Lync Server 2013).
```C++
    Move-CsAnnouncementConfiguration.ps1 -Source LS2010Pool.contoso.com -Destination LS2013Pool.contoso.com
```
## Spostamento della configurazione degli annunci di numeri non assegnati da un pool di Lync Server 2013 a un pool di Lync Server 2010

In questo esempio vengono spostati gli annunci di numeri non assegnati dal pool di origine (Lync Server 2013) al pool di destinazione (Lync Server 2010).
```C++
    Move-CsAnnouncementConfiguration.ps1 -Source LS2013Pool.contoso.com -Destination LS2010Pool.contoso.com
```
## Web Conf Data

Lo strumento Web Conf Data consente a un amministratore del software di comunicazione Lync Server 2013 di disporre di maggiore controllo sui dati associati alle conferenze Web di un organizzatore. Gli scenari includono la possibilità di eliminare i dati sulle riunioni di un determinato utente secondo un criterio basato sul timestamp.

## Descrizione

Questo strumento consente all'amministratore di eseguire le operazioni seguenti:

1.  Trovare tutti i dati delle conferenze Web associati a un utente.

2.  Eliminare tutti i dati delle conferenze Web associati a un utente.

3.  Spostare tutti i dati delle conferenze Web associati a un utente che sono precedenti rispetto a una certa data.

4.  Spostare tutti i dati delle conferenze Web associati a un utente quando tale utente viene spostato da un pool a un altro.


> [!NOTE]
> Gli Strumenti del Resource Kit per Lync Server 2010 supportano lo spostamento di tutti i dati delle conferenze Web associati a un utente quando tale utente viene spostato da un pool a un altro. Tale funzionalità è stata deprecata in questo strumento e sostituita dal parametro <STRONG>MoveConferenceData</STRONG>. Per informazioni dettagliate su questo parametro, vedere il cmdlet <A href="https://technet.microsoft.com/it-it/library/gg398528(v=ocs.15)">Move-CSUser</A>.



Lo strumento elimina i dati sulle riunioni solo per le riunioni inattive. Le riunioni attive, o riunioni nelle sessioni, non possono essere eliminate.

Questo strumento deve essere eseguito da un computer ubicato nello stesso pool dell'utente di destinazione. L'utente di cui lo strumento gestisce i dati del contenuto delle riunioni deve essere ospitato nello stesso pool di utenti.

## Output

Questo strumento restituisce i risultati delle singole operazioni:

  - Se viene eseguita una query, l'output dello strumento è costituito da un elenco di tutte le cartelle di dati sulle riunioni inattive di cui l'utente dispone come organizzatore.

  - Se viene eseguita un'eliminazione, l'output dello strumento è costituito da un elenco di tutte le cartelle di dati sulle riunioni di cui verranno eliminati i dati.

## Requisiti

Lo strumento deve essere eseguito nello stesso pool in cui è ospitato l'organizzatore.

Lo strumento deve essere eseguito con privilegi di amministratore con accesso all'archivio file di dati.

## Esempi

Nella tabella seguente sono descritti i parametri, alcuni dei quali sono utilizzati negli esempi.

![Parametri dello strumento Web Conf Data.](images/JJ945604.a733c1c6-5dfc-4874-a74f-bfdee81c1401(OCS.15).jpg "Parametri dello strumento Web Conf Data.")
```C++
    WebConfDataTool.exe /User:user0@contoso.com /Action:query ""/ExpirationDate:08/09/2010 12:00:00""
```
Nell'esempio riportato sopra è illustrato il funzionamento di un comando di query. L'output di tale comando è un elenco di tutte le cartelle di contenuto delle riunioni interessate dallo strumento.
```C++
    WebConfDataTool.exe /User:user0@contoso.com /Action:delete
```
Nell'esempio riportato sopra viene illustrato un comando di eliminazione. Tale comando rimuove tutte le cartelle delle riunioni inattive dall'utente specificato.

## Riepilogo

Questo strumento può essere una risorsa preziosa per gli amministratori che necessitano di un controllo più preciso sui dati relativi alle riunioni in conferenza.

