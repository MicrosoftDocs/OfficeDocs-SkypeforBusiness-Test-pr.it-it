---
title: 'Lync Server 2013: Note sulla versione'
TOCTitle: Note sulla versione
ms:assetid: 9f9e864c-3365-4800-803c-5289bd8fd363
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205120(v=OCS.15)
ms:contentKeyID: 49301489
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Note sulla versione per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-23_

Fare riferimento al presente file delle Note sulla versione di Lync Server 2013 per informazioni relative ai problemi noti di Lync Server 2013.

## Informazioni sul documento

In questo documento sono disponibili informazioni importanti che è consigliabile conoscere prima di distribuire e usare Lync Server 2013. Per informazioni dettagliate su Lync Server 2013, fare riferimento alla documentazione di [Microsoft Lync Server 2013](microsoft-lync-server-2013.md).

Sezioni del documento:

   Client Lync 2013

   Lync Server

   Installazione

   Mobilità
  
   Servizi di conferenza

   VoIP aziendale

   Presenza

   applicazione Response Group, applicazione Parcheggio di chiamata e risposta alle chiamate di gruppo

   Pannello di controllo di Lync Server, Generatore di topologie e Strumento di pianificazione

   Localizzazione

   Copyright

## Client Lync 2013

## Impossibile trasferire un file in un messaggio istantaneo se il file è aperto in un'altra applicazione (1920369)

**Problema:**

Se si tenta di trasferire un file, ad esempio un documento di Word, aggiungendolo a un messaggio istantaneo destinato a un altro utente Lync, il trasferimento potrebbe non andare a buon fine anche se l'operazione sembra completata correttamente. Nel client Lync compare l'icona del tipo di file, ma il destinatario designato non riesce ad aprirlo. Non viene visualizzato alcun messaggio di errore per informare che il trasferimento non è andato a buon fine.

**Soluzione:**

Per risolvere questo problema, chiudere il file o l'applicazione in cui è aperto prima di tentare il trasferimento in un messaggio instantaneo.

## Lync Server

## Se la replica dei dati del servizio di archiviazione di Lync Server ha esito negativo, gli amministratori devono controllare i contatori delle prestazioni per verificare se nella coda del servizio sono presenti elementi (3225121)

**Problema:**

Il servizio di archiviazione di Lync Server usa Windows Fabric per la replica. Se i dati vengono eliminati in un Front End Server primario, ma l'operazione di eliminazione non riesce su un Front End Server secondario, ad esempio in caso di arresto o errore imprevisto nel Front End Server, i dati possono essere mantenuti diventando "orfani". I dati orfani possono causare una riduzione delle prestazioni e occupano spazio su disco.

**Soluzione:**

Per risolvere questo problema, se nel registro eventi vengono generati gli eventi LYSS\_DB\_SPACE\_USED\_ERROR (Id=32058) e LYSS\_DB\_SPACE\_USED\_CRITICAL (Id=32059), gli amministratori devono controllare il contatore delle prestazioni nel Front End Server in **LS:LYSS - API del servizio di archiviazione** denominato **LYSS - Numero corrente di elementi obsoleti in coda del servizio di archiviazione**. Se il valore di questo contatore delle prestazioni è elevato, ad esempio maggiore di 50.000, l'amministratore deve eseguire lo strumento CleanuUpStorageServiceData.exe disponibile in Lync Server 2013 Resource Kit, il quale elimina tutti i dati orfani dal pool. Per informazioni dettagliate su questo strumento, vedere la documentazione di Lync Server 2013 Resource Kit.

## Ogni volta che si apportano modifiche alla configurazione degli indirizzi IP di un server o un pool, i servizi di Lync Server devono essere riavviati (3212447)

**Problema:**

Quando si modifica la configurazione degli indirizzi IP per una distribuzione di Lync Server 2013, ad esempio se si passa da IPv4 a dual stack o da quest'ultimo a IPv6, la nuova configurazione non viene applicata a tutti i componenti server se i servizi non vengono riavviati.

**Soluzione:**

Per risolvere questo problema, riavviare i servizi di Lync Server dopo aver apportato modifiche alla configurazione degli indirizzi IP della distribuzione. A tale scopo, eseguire i cmdlet seguenti nella Lync Server Management Shell:

```
Stop-CsWindowsService -graceful
```

```
Start-CsWindowsService
```

## Il cmdlet delle transazioni sintetiche delle conferenze telefoniche con accesso esterno non è più disponibile in Lync Server 2013 Management Pack (3212342)

**Problema:**

Il cmdlet delle transazioni sintetiche delle conferenze telefoniche con accesso esterno **Test-CsDialInConferencing** non è più disponibile in Lync Server 2013 Management Pack.

**Soluzione:**

L'uso del cmdlet delle transazioni sintetiche delle conferenze telefoniche con accesso esterno **Test-CsDialInConferencing** è supportato solo all'interno di un'organizzazione.

Gli amministratori possono continuare a usare il cmdlet nella Lync Server Management Shell a fini di risoluzione dei problemi. Se necessario, le organizzazioni possono anche sviluppare un Management Pack privato per l'esecuzione interna di cmdlet.

## Il servizio di registrazione centralizzato viene arrestato se il traffico di rete si interrompe durante la copia dei file di log in una condivisione di rete (3212464)

**Problema:**

Se il servizio di registrazione centralizzato è configurato per l'uso di un percorso di rete (il valore del parametro CacheFileNetworkFolder del cmdlet **Get-CsClsConfiguration** è un percorso UNC valido), i file di log memorizzati nella cache vengono copiati nella condivisione di rete. Se si verifica un'interruzione del traffico di rete durante la copia dei file, viene generata un'eccezione a causa della quale il servizio di registrazione centralizzato viene arrestato.

Il servizio è configurato per il riavvio automatico fino a tre volte, pertanto viene ripristinato in seguito alle prime tre eccezioni.

**Soluzione:**

Non esiste una soluzione a questo problema. Per individuarlo, monitorare l'evento con ID 7031 nel registro eventi da "Gestione controllo servizi". Questo evento viene registrato se "l'agente del servizio di registrazione centralizzato di Lync Server" viene terminato in modo imprevisto. Se ciò si verifica per più di tre volte, riavviare il servizio manualmente mediante il cmdlet **Start-CsWindowService**.

## È necessario importare manualmente gli elementi della coda del servizio di archiviazione (3211368)

**Problema:**

Lync Server 2013 archivia i dati sulle conferenze e i messaggi istantanei, ad esempio i messaggi archiviati e la registrazione dettagli chiamata (CDR) in un database in ogni Front End Server. I dati vengono archiviati nel database durante l'elaborazione e prima di essere recapitati alla destinazione prevista. Per migliorare le prestazioni, Lync Server 2013 esporta regolarmente gli elementi della coda del database locale non elaborati per periodi di tempo prolungati e li salva nell'archivio file. Se l'archivio file non è disponibile, gli elementi vengono archiviati in ogni Front End Server. La stessa operazione viene eseguita per evitare la perdita di dati durante il failover del pool.

Durante l'operazione di esportazione, il servizio di archiviazione di Lync Server ne registra ogni fase nel registro eventi con gli ID 32075 (operazione di scaricamento completo avviata), 32076 (scaricamento completato), 32082 (scaricamento a livello di manutenzione avviato), 32083 (scaricamento a livello di manutenzione completato), 32089 (scaricamento a causa di esaurimento dello spazio nel database). I dati non vengono automaticamente reimportati nel sistema a fini di elaborazione e recapito alla destinazione finale ( SQL Server o Exchange Server).

**Soluzione:**

Per importare i dati nel sistema, gli amministratori devono usare lo strumento ImportStorageServiceData in Lync Server Resource Kit, il quale riaggiunge i dati al sistema per l'elaborazione e il recapito alla destinazione finale.

## Le ricerche del servizio query Web Rubrica hanno esito negativo se il valore predefinito di UseNormalizationRules viene impostato su False (3175514)

**Problema:**

Se il valore predefinito di UseNormalizationRules viene impostato su False, le ricerche del servizio query Web Rubrica hanno esito negativo. Dopo che il valore predefinito viene cambiato, gli utenti del client Lync non saranno in grado di usare il servizio query Web Rubrica per cercare utenti.

**Soluzione:**

Se il valore predefinito di UseNormalizationRules viene impostato su False in modo che gli utenti possano usare i numeri di telefono definiti in Servizi di dominio Active Directory senza applicare regole di normalizzazione di Lync Server 2013, è possibile risolvere il problema nel modo seguente:

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire una delle operazioni seguenti:
    
      - Se la distribuzione include solo server Lync Server 2013, eseguire il cmdlet indicato di seguito a livello globale per cambiare i valori di UseNormalizationRules e IgnoreGenericRules impostandoli su True:
        
            Set-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true
    
      - Se la distribuzione include una combinazione di Lync Server 2013 e Lync Server 2010 o Office Communications Server 2007 R2, eseguire il cmdlet indicato di seguito e assegnarlo a ogni pool Lync Server 2013 nella topologia:
        
            new-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true

3.  Attendere che venga eseguita la replica dell'archivio di gestione centrale in tutti i pool.

4.  Modificare le regole di normalizzazione del telefono nella distribuzione per cancellare il contenuto. Il file si trova nella condivisione file di ogni pool Lync Server 2013. Se il file non è presente, crearne uno vuoto denominato "Company\_Phone\_Number\_Normalization\_Rules.txt."

5.  Attendere alcuni minuti affinché i nuovi file vengano letti da tutti i pool Front End.

6.  Eseguire il cmdlet seguente in ogni pool Lync Server 2013 della distribuzione.
    
        Update-csAddressBook

## L'evento di errore 21054 del server della rubrica viene generato una volta al giorno per ogni pool di Lync 2013 (3195918)

**Problema:**

Il server della rubrica di Lync Server 2013 genera un evento di errore 21054 una volta al giorno quando si esegue la manutenzione quotidiana. L'errore viene generato anche ogni volta che un amministratore esegue il cmdlet **Update-csAddressBook**, anche se l'aggiornamento viene completato correttamente. Questo evento di errore può tuttavia essere tranquillamente ignorato se l'aggiornamento ha esito positivo.

**Soluzione:**

Quando si verifica questo evento di errore, eseguire questo cmdlet:

    Debug-csAddressBookReplication -Poolfqdn <Pool FQDN for which the event was generated>

Se il cmdlet segnala che non sono presenti oggetti non indicizzati o abbandonati, l'evento di errore 21054 può essere tranquillamente ignorato.

Inoltre, è necessario disabilitare l'indicatore KHI (Key Health Indicator) "Address Book Users Correctly Indexed" in System Center Operations Manager.

## Le richieste possono avere esito negativo se in un pool di server perimetrali è configurato IPv6 (3205810)

**Problema:**

Se in un pool di server perimetrali è configurato IPv6, alcune richieste al pool potrebbero avere esito negativo.

**Soluzione:**

Per risolvere questo problema, non configurare i pool di server perimetrali con IPv6.

## L'esecuzione del cmdlet invoke-csPoolFailback potrebbe avere esito negativo durante il failback del pool (3206153)

**Problema:**

Quando si tenta di eseguire il failback di un pool, l'esecuzione del cmdlet **invoke-csPoolFailback** potrebbe non riuscire con l'errore "Processo di attivazione non riuscito dopo svariati tentativi".

**Soluzione:**

Per risolvere questo problema, eseguire di nuovo il cmdlet e attendere finché non viene eseguito correttamente. Tenere presente che il processo di failback può richiedere diversi minuti, fino a 60 per un pool con 20.000 utenti.

## Quando si aggiunge un Front End Server a un pool già esistente potrebbe verificarsi una perdita di dati (3015990) – Hybrid, Skype for Business online

**Problema:**

Questo problema può verificarsi negli ambienti in cui un pool ha più Front End Server e si riavvia uno dei Front End Server oppure si aggiunge un nuovo Front End Server che in precedenza non faceva parte del pool.

I dati degli utenti in fase di archiviazione potrebbero essere persi finché non si stabilisce una distribuzione stabile dell'archiviazione dati per il pool. Questo periodo di potenziale perdita di dati è limitato a 15 minuti per le conversazioni da persona a persona e a 30 minuti per le conferenze.

**Soluzione:**

Quando si esegue la manutenzione, invece di avviare i Front End Server nel pool uno alla volta, è consigliabile eseguire il failover del pool a un altro pool e quindi provvedere alle attività di manutenzione dei server. È anche possibile rendere il servizio non disponibile prima di eseguire le attività di manutenzione e quindi ripristinarlo una volta portate a termine.

## Gli amministratori non riescono a ottenere il conteggio dei licenziatari mediante il cmdlet Get-CsClientAccessLicense (3012255)

**Problema:**

Gli amministratori non riescono a ottenere dati esatti sull'uso delle licenze client mediante il cmdlet **Get-CsClientAccessLicense**.

**Soluzione:**

Per verificare il tipo di licenza del server, è possibile eseguire il cmdlet **Get-CsService** per recuperare i nomi di dominio completi (FDQN) di tutti i database. Se il nome di dominio completo del Front End Server corrisponde a quello del database back-end, la licenza è quella della Standard Edition. In caso contrario, si tratta di una licenza Enterprise Edition.

## Non viene riportato il conteggio esatto dei licenziatari client (3010175)

**Problema:**

Quando si determinano i conteggi delle licenze client, possono verificarsi le condizioni seguenti:

1.  **Conteggio licenze non esatto per gli utenti mobili**
    
    Il conteggio delle licenze si basa sul numero di indirizzi IP univoci per gli utenti basati su dispositivi. Il conteggio delle licenze è limitato nei modi seguenti:
    
      - Il conteggio delle licenze risulta errato per eccesso se l'indirizzo IP dell'utente cambia durante le sessioni di Lync. Questa condizione si verifica se un utente si connette a Lync Server da più postazioni con un client desktop.
    
      - Il conteggio delle licenze risulta errato per difetto se un utente si connette con un client mobile, perché non è possibile determinare l'indirizzo IP del dispositivo.

2.  **Le licenze vengono conteggiate due volte per le chiamate da rete PSTN (Public Switched Telephone Network) a client Lync, da client Lync a linee di rete PSTN e per chiamate Lync inoltrate a linee di rete PSTN**
    
    Negli scenari seguenti vengono conteggiate due licenze aggiuntive invece di una perché vengono considerati sia il numero di telefono sia l'utente Lync per determinare il numero di licenze in uso. Per ottenere dati esatti sulle licenze, rimuovere manualmente le licenze generate da numeri di telefono.
    
      - Chiamata da telefono PSTN a Lync
    
      - Chiamata Lync a una linea di rete PSTN
    
      - Chiamata da rete PSTN a Lync e quindi inoltro della chiamata a una linea di rete PSTN. Una delle linee di rete PSTN viene conteggiata.

3.  **Non vengono conteggiate licenze per telefoni Lync connessi**
    
    Quando un utente usa un telefono certificato per Lync il quale effettua l'accesso e rimane connesso, non verrà conteggiato l'uso di una licenza se la query sulle licenze viene eseguita dopo che l'accesso del telefono è stato effettuato.

4.  **Licenze conteggiate per telefoni PSTN partecipanti a conferenze**
    
    Quando un utente partecipa a una conferenza con un telefono PSTN, viene erroneamente conteggiata una licenza. Non è tuttavia necessaria alcuna licenza per partecipare a una conferenza con un telefono PSTN.

**Soluzione:**

1.  **Conteggio licenze non esatto per gli utenti mobili**
    
      - È possibile identificare manualmente gli indirizzi IP appartenenti allo stesso dispositivo e quindi rimuovere uno di essi dal conteggio delle licenze.
    
      - Non esiste una soluzione a questo problema per i dispositivi mobili che si connettono con client Lync.

2.  **Le licenze vengono conteggiate due volte per le chiamate da rete PSTN a client Lync, per chiamate da client Lync a linee di rete PSTN e per chiamate Lync inoltrate a linee di rete PSTN**
    
    È necessario identificare manualmente il numero di telefono PSTN e rimuoverlo dal conteggio delle licenze.

3.  **Le licenze per i telefoni Lync connessi non vengono conteggiate**
    
    È possibile configurare il telefono Lync affinché si disconnetta e quindi riacceda periodicamente, ad esempio ogni 3 mesi.

4.  **Licenze conteggiate per telefoni PSTN partecipanti a conferenze**
    
    È possibile identificare manualmente il numero di telefono PSTN usato per partecipare alla conferenza e rimuoverne la licenza dal conteggio generato.

## Il Pannello di controllo di Lync Server smette di funzionare negli ambienti VMware dopo l'aggiornamento a Silverlight 5 (3010077)

**Problema:**

Se si usa il Pannello di controllo di Lync Server in un ambiente VMware, il Pannello di controllo di Lync Server potrebbe smettere di funzionare dopo aver aggiornato Microsoft Silverlight alla versione 5.

**Soluzione:**

Per risolvere questo problema, effettuare una delle operazioni seguenti:

  - Disinstallare Silverlight 5 e installare Silverlight 4 da [http://go.microsoft.com/fwlink/p/?LinkID=149156](http://go.microsoft.com/fwlink/p/?linkid=149156).

  - Accedere al Pannello di controllo di Lync Server da un computer che non sia un computer virtuale VMware.
    
    A tale scopo, è possibile avviare il Pannello di controllo di Lync Server dal menu **Start** di Windows, se gli strumenti di amministrazione di Lync Server sono installati nel computer.
    
    È anche possibile accedere al Pannello di controllo di Lync Server mediante un Web browser. L'URL è analogo a https://\<fqdn\_pool\_frontend\>/cscp.

## Le informazioni sugli utenti nel servizio Rubrica non vengono aggiornate dopo che il nome distinto dell'utente viene modificato in Active Directory (3211549)

**Problema:**

Se il nome distinto di un utente (noto come DN) viene cambiato in Servizi di dominio Active Directory, eventuali ulteriori modifiche non verranno aggiornate nel servizio Rubrica. Ciò non influisce sull'accesso o la presenza dell'utente, ma impedisce le comunicazioni se viene modificato anche l'indirizzo SIP in quanto le ricerche restituiranno un indirizzo SIP obsoleto.

**Soluzione:**

Per risolvere questo problema, non modificare il nome distinto degli utenti. Se si ripristina il nome distinto originario dell'utente, gli aggiornamenti verranno applicati al servizio Rubrica.

## Installazione

## L'utilizzo di caratteri non ASCII potrebbe impedire l'avvio del server Lync

**Problema:**

L'installazione non riuscirà se il nome della cartella di destinazione include caratteri non ASCII (inclusi UNICODE, set di caratteri a doppio byte (DBCS), UTF-8 e UTF-16). Inoltre, l'installazione potrebbe riuscire ma il server non verrà avviato se gli elementi seguenti includono caratteri non ASCII:

  - Nome del computer

  - Nome del dominio

  - Nome utente

  - URI SIP dell'utente

  - Nome dell'account di servizio

**Soluzione:**

Utilizzare solo caratteri ASCII nel nome della cartella di destinazione, nel nome del computer, nel nome del dominio, nel nome dell'utente, nell'URI SIP dell'utente e nei nomi di account di servizio.

## Prima di installare Lync Server 2013, è necessario installare l'hotfix per risolvere il problema del danneggiamento degli heap che si verifica quando un modulo chiama il metodo InsertEntityBody in IIS 7.5.

**Problema:**

L'hotfix per risolvere il problema del danneggiamento degli heap che si verifica quando un modulo chiama il metodo InsertEntityBody in IIS 7.5 ( [http://go.microsoft.com/fwlink/p/?LinkId=268602](http://go.microsoft.com/fwlink/p/?linkid=268602)), descritto nell'articolo della Microsoft Knowledge Base 264886 ( [http://go.microsoft.com/fwlink/p/?LinkId=268603](http://go.microsoft.com/fwlink/p/?linkid=268603)), deve essere installato prima di installare Lync Server 2013.

**Soluzione:**

Scaricare e installare l'hotfix dall'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268602\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268602%26clcid=0x410).

## L'installazione di Lync Server 2013 non riesce sulla versione italiana di Windows Server 2012 OS RTM (3179467)

**Problema:**

L'installazione di Lync Server 2013 sulla versione italiana di Windows Server 2012 non riesce a causa dell'esito negativo dell'installazione di Windows Fabric.

L'installazione di Windows Fabric non riesce perché vengono create tracce di fabric con il formato di ora HH:MM:SS, mentre nella versione italiana di Windows Server il formato è HH.MM.SS.

**Soluzione:**

Per risolvere questo problema, aggiornare il Registro di sistema prima di installare Lync Server 2013. La chiave del Registro di sistema da aggiornare è: HKEY\_USERS\\.DEFAULT\\Control Panel\\International\\sTimeFormat. Modificare il valore di sTimeFormat impostandolo su HH:mm:ss mediante interfaccia della riga di comando Windows PowerShell nel modo seguente:

1.  Avviare Windows PowerShell ed eseguire i cmdlet seguenti:
    
    ```
    New-PSDrive -Name HKU -PSProvider Registry -Root HKEY_USERS
    ```
    ```
    $a="HKU:\.Default\Control Panel\International"
    ```

2.  Per visualizzare il valore corrente, eseguire il cmdlet seguente:
    
        Get-itemproperty $a -Name sTimeFormat
    
    Prendere nota del valore corrente di sTimeFormat in modo da poterlo ripristinare al termine dell'installazione.

3.  Per impostare un nuovo valore, eseguire il cmdlet:
    
        Set-ItemProperty $a -Name sTimeFormat -Value "HH:mm:ss"

4.  Dopo aver installato correttamente Lync Server 2013, ripristinare il valore originale di sTimeFormat eseguendo questo cmdlet:
    
        - Set-ItemProperty $a -Name sTimeFormat -Value "<Value noted down in Step 3. above>"

## Mobilità

## Problemi relativi ai client mobili durante il processo di failover del server (3345992)

**Problema:**

Quando si verifica un errore in Lync Server e inizia il processo di failover, gli utenti di client mobili possono essere interessati dai problemi seguenti:

  - Dopo l'inizio del failover non è possibile ricevere chiamate Lync in arrivo o segnale per un massimo di 10 minuti.

  - Non è possibile accettare le richieste di chat in arrivo

  - Non è possibile partecipare a riunioni se il server in errore è il server principale dell'utente

**Soluzione:**

Non è disponibile una soluzione per questo problema. La normale funzionalità verrà ripristinata al termine del processo di failover.

## Se l'utente di un dispositivo mobile rifiuta una chiamata in arrivo da un altro endpoint Lync, la chiamata viene visualizzata come conversazione non effettuata sui client Lync Mobile (3346251)

**Problema:**

Se l'utente di un dispositivo mobile rifiuta una chiamata in arrivo proveniente da un altro endpoint Lync, la chiamata viene visualizzata come conversazione non effettuata nel client Lync Mobile invece di essere inserita nell'elenco chiamate del dispositivo.

**Soluzione:**

Non è disponibile una soluzione per questo problema.

## Il nome in un contatto federato potrebbe non essere visualizzato sul client mobile quando si esegue la ricerca di contatti (3346256)

**Problema:**

È possibile che i nomi dei contatti federati non vangano visualizzati in alcuni scenari, ad esempio quando si esegue la ricerca di un contatto federato nell'elenco contatti. Questo problema può verificarsi quando non è disponibile una sottoscrizione attiva relativa alla presenza per il contatto sul client Lync Mobile.

**Soluzione:**

Non è disponibile una soluzione per questo problema.

## Nel client mobile le informazioni su invitati e timestamp non vengono riportate nel messaggio su una conversazione non effettuata che corrisponde a un invito a una conferenza (3346265)

**Problema:**

Nel client mobile, quando una conversazione non effettuata corrisponde a un invito a una conferenza, le informazioni su invitati e timestamp non vengono riportate nel messaggio di conversazione non effettuata.

**Soluzione:**

Non è disponibile una soluzione per questo problema.

## Gli utenti di client mobili che effettuano chiamate mediante VoIP non possono lasciare messaggi agli utenti la cui segreteria telefonica è configurata in Exchange 2010 o versioni precedenti (3346260)

**Problema:**

Se l'utente di un client mobile utilizza VoiP per effettuare chiamate, non potrà lasciare messaggi agli utenti la cui segreteria telefonica è configurata in Microsoft Exchange Server 2007 o Microsoft Exchange Server 2010.

**Soluzione:**

Per risolvere il problema, utilizzare Exchange 2010 con SP1 o una versione successiva di Microsoft Exchange Server.

## Quando si sceglie l'opzione Blocca con URL per Configurazione versione client nei client mobili, è possibile che venga visualizzato un messaggio di errore non corretto (3346258)

**Problema:**

Quando si sceglie l'opzione **Blocca con URL** per Configurazione versione client nei client mobili, è possibile che venga visualizzato un messaggio di errore non corretto quando la versione del client non è supportata.

**Soluzione:**

Per risolvere il problema, specificare **Blocca** anziché **Blocca con URL** per Configurazione versione client.

## Servizi di conferenza

## Il software antivirus in esecuzione sui Front End Server di Lync Server 2013 può causare il riciclo del dominio dell'applicazione, il che determina una temporanea interruzione del servizio per Lync Web App 2013, Lync Mobile 2010 e client Lync Mobile 2013 (3212531)

**Problema:**

Il software antivirus può attivare il riavvio del dominio dell'applicazione, in che può determinare la perdita dello stato delle applicazioni client del sevizio per dispositivi mobili di Lync 2013 e dell'API Web di comunicazioni unificate ( Lync Web App 2013, Lync Mobile 2010 e Lync Mobile 2013).

**Soluzione:**

Per risolvere questo problema, escludere le cartelle contenenti componenti Web e .NET Framework dall'analisi antivirus. Per informazioni dettagliate, vedere l'articolo della Microsoft Knowledge Base 312592, "PRB: Riavvio di un'applicazione casuale con il messaggio di errore "Riavvio dell'applicazione in corso" in ASP.NET" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x410).

È consigliabile escludere le cartelle seguenti:

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Mcx\\Ext

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Mcx\\Int

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Ucwa\\Int

  - %ProgramFiles%\\Microsoft Lync Server 2013\\Web Components\\Ucwa\\Ext

  - %Windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\Config

## Per partecipare alle conferenze è necessario che in Windows Internet Explorer sia abilitato il supporto per i controlli ActiveX o il supporto nativo di XMLHTTP (2798163)

**Problema:**

Se un utente ha disabilitato sia il supporto dei controlli ActiveX sia il supporto nativo di XMLHTTP nelle impostazioni Internet del browser Windows Internet Explorer, non è possibile partecipare a una riunione se Internet Explorer è selezionato come browser predefinito.

**Soluzione:**

Abilitare il supporto dei controlli ActiveX o il supportato nativo di XMLHTTP in Internet Explorer.

## Non è possibile ripristinare il servizio Web Conferencing di Lync Server dalla modalità critica (2788663)

**Problema:**

Se è attiva la modalità critica per l'archiviazione, in caso di errori di sistema essa viene avviata e le conferenze smetteranno di funzionare per i partecipanti. Dopo che l'amministratore ha corretto gli errori di sistema (ad esempio risolvendo un problema del database), il servizio di conferenza dati non viene ripristinato automaticamente, bensì deve essere riavviato manualmente dall'amministratore.

**Soluzione:**

Un amministratore deve riavviare manualmente il servizio di conferenza dopo che è stato corretto l'errore di sistema.

## Il servizio Web Conferencing ignora il proxy HTTP per i server Office Web Apps esterni (2602182)

**Problema:**

Se si distribuisce un Server Office Web Apps all'esterno del servizio Web Conferencing (ovvero il server non si trova all'interno della rete aziendale interna) in Internet, nella rete perimetrale e il servizio Web Conferencing richiede un proxy HTTP per connettervisi, l'individuazione del Server Office Web Apps ha esito negativo. Il servizio Web Conferencing ignora le impostazioni proxy HTTP come definite in Generatore di topologie per l'installazione di Server Office Web Apps. Di conseguenza, il client Lync non sarà in grado di eseguire la condivisione di Microsoft PowerPoint 2010 con altri partecipanti alla conferenza. Se si installa Lync Server in locale e si configura Server Office Web Apps ugualmente in locale nella rete interna, la configurazione proxy non è necessaria.

**Soluzione:**

L'unica soluzione è non configurare una distribuzione che necessita dell'uso del proxy HTTP per comunicare con un Server Office Web Apps esterno.

## L'aggiunta di video a una conferenza di un provider di servizi di audioconferenza non è supportata (2603861)

**Problema:**

L'aggiunta di un video non è supportata se l'utente partecipa a una conferenza di un provider di servizi di audioconferenza.

**Soluzione:**

Non è disponibile una soluzione per questo problema.

## Le topologie con IPv6 abilitato impongono l'aggiornamento automatico del plug-in Silverlight di Lync Web App per assicurare il funzionamento della caratteristiche di condivisione dello schermo da Lync Web App (2604634)

**Problema:**

Se una topologia è configurata con IPv6 abilitato, gli utenti non possono condividere lo schermo dal client Lync Web App se è già installata una versione precedente del plug-in di condivisione.

**Soluzione:**

Per imporre l'aggiornamento alla versione più recente del plug-in di condivisione dello schermo all'accesso a una riunione tramite Lync Web App, modificare il valore di **MinSupportedBuildVersion** da "4.0.7457.0" a "4.0.7577.380" in entrambi i file seguenti:

  - %ProgramFiles%\\Microsoft Lync Server 15\\Web Components\\Reach\\Int\\Client\\Plugins\\ReachAppShPluginProperties.xml

  - %ProgramFiles%\\Microsoft Lync Server 15\\Web Components\\Reach\\Ext\\Client\\Plugins\\ReachAppShPluginProperties.xml

## VoIP aziendale

## In alcuni casi, un client Lync in esecuzione in un computer configurato per l'utilizzo del dual stack IPv4 e IPv6 potrebbe non supportare funzionalità basate sulla subnet IP del computer, ad esempio E911, bypass multimediale, controllo di ammissione di chiamata e routing in base alla posizione (3335508)


> [!NOTE]
> Le informazioni in questa sezione sono relative agli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.



**Problema:**

Un client Lync in esecuzione in un computer abilitato per il dual stack IPv4 e IPv6 e basato sulla risoluzione DNS del server proxy può utilizzare l'indirizzo IPv6 del computer per l'accesso. In seguito, il client Lync supporterà solo le funzionalità supportate per a IPv6, che non includono E911, bypass multimediale, controllo di ammissione di chiamata e routing in base alla posizione.

**Soluzione:**

Per risolvere il problema, disabilitare il supporto per IPv6 sul computer client.

## Se per un utente non è configurato il VoIP aziendale, l'utente deve usare il formato E164 per effettuare una chiamata in uscita da una conferenza (3215342)

**Problema:**

Se per un utente non è configurato il VoIP aziendale, l'utente deve usare il formato E164 per effettuare una chiamata in uscita da una conferenza. Se il formato E164 non è usato, l'utente non sarà in grado di effettuare la chiamata in uscita.

**Soluzione:**

Per risolvere questo problema, gli utenti per cui non è abilitato il VoIP aziendale devono effettuare la chiamata in uscita da una conferenza mediante numeri in formato E164.

## Presenza

## Se un utente seleziona "Blocca tutti gli inviti e le comunicazioni" mentre è abilitato l'archivio contatti unificato, lo stato presenza non è rifiutato quando dovrebbe esserlo (3204526)

**Problema:**

Se un utente seleziona "Blocca tutti gli inviti e le comunicazioni" mentre è abilitato l'archivio contatti unificato, lo stato presenza non è rifiutato quando dovrebbe esserlo.

**Soluzione:**

Per risolvere questo problema, è possibile disabilitare l'archivio contatti unificato per l'utente. A tale scopo, eseguire i cmdlet seguenti:

    Set-CsUserServicesPolicy -Identity "<user display name>" -UcsAllowed $False

Ad esempio:

    Set-CsUserServicesPolicy -Identity "Ken Myer" -UcsAllowed $False

## Gli utenti di Office Communications Server 2007 R2 in locale non sono in grado di vedere lo stato presenza degli utenti di Skype for Business online in distribuzioni ibride (3014624) - Hybrid

**Problema:**

Il problema può verificarsi in una distribuzione ibrida quando si usa un server Director di Lync Server 2013.

Lo stato presenza degli utenti disponibili in Skype for Business online viene indicato come Stato presenza sconosciuto per gli utenti locali. Inoltre, gli utenti in Skype for Business online non sono in grado di visualizzare lo stato presenza degli utenti locali di Office Communications Server R2.

**Soluzione:**

Per risolvere parzialmente questo problema, modificare il server principale (msrtcsip-presencehomeserver) degli utenti di Skype for Business online affinché punti a un pool locale di Lync Server 2013 invece che al server Director di Lync Server 2013. È possibile modificare questa impostazione nel Front End Server locale.

Questa soluzione consente di visualizzare correttamente lo stato presenza degli utenti in Office Communications Server 2007 R2 agli utenti di Skype for Business online.

## applicazione Response Group, applicazione Parcheggio di chiamata e risposta alle chiamate di gruppo

## Il chiamante potrebbe ascoltare un secondo di musica di attesa mentre viene stabilita una chiamata con l'utente che la recupera (3334097)


> [!NOTE]
> Le informazioni in questa sezione sono relative agli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.



**Problema:**

Quando si recupera una chiamata mediante risposta alle chiamate di gruppo, il chiamante potrebbe ascoltare un secondo di musica di attesa mentre viene stabilita la chiamata.

**Soluzione:**

Non è disponibile una soluzione per questo problema.

## L'accesso e l'uscita di un agente Response Group tramite una console agente di Lync Server 2010 è possibile solo per gruppi di agenti formali di Lync Server 2010 (2773455)

**Problema:**

L'accesso e l'uscita di un agente Lync Server 2013Response Group tramite una console agente di Lync Server 2010 è possibile solo per gruppi di agenti formali di Lync Server 2010. Nella console agente di Lync Server 2010 gli utenti possono visualizzare solo il Response Group di Lync Server 2010 a cui essi appartengono. Non possono visualizzare i Response Group di Lync Server 2013 a cui appartengono.

**Soluzione:**

Se l'agente Response Group è un utente di Lync Server 2013 e fa parte di un gruppo di agenti formali di Lync Server 2013, deve accedere alla console agente di Lync Server 2013 direttamente tramite un collegamento Web in un browser per accedere a gruppi di agenti di Lync Server 2013 o per uscirne.

## Un agente Response Group di Lync Server 2010 non può effettuare chiamate per conto di un Response Group di Lync Server 2013 (2773471)

**Problema:**

Un utente di Lync Server 2010 che è un agente del Response Group di Lync Server 2013 non può effettuare chiamate per conto del Response Group. Il Response Group di Lync Server 2013 non sarà disponibile nel client Lync per effettuare chiamate.

**Soluzione:**

Per risolvere questo problema, è necessario spostare l'utente di Lync Server 2010 in Lync Server 2013.

## La rimozione di un Response Group da Lync Server 2010 dopo che ne è stata eseguita la migrazione a Lync Server 2013 impedisce al Response Group di accettare chiamate in arrivo (3016227)

**Problema:**

Se un Response Group di cui è stata eseguita la migrazione da Lync Server 2010 a Lync Server 2013 viene rimosso da Lync Server 2010 tramite il Pannello di controllo di Lync Server o la Lync Server Management Shell, il Response Group in Lync Server 2013 smetterà di ricevere chiamate in arrivo.

**Soluzione:**

Per risolvere questo problema, non rimuovere da Lync Server 2010 Response Group di cui è stata eseguita la migrazione da Lync Server 2010 a Lync Server 2013.

Se il Response Group è già stato rimosso, è necessario ridistribuirlo in Lync Server 2013.

## Quando un nuovo flusso di lavoro gestito viene impostato come inattivo alla creazione, la distribuzione del flusso di lavoro ha esito negativo (3207527)

**Problema:**

Quando un nuovo flusso di lavoro gestito viene impostato come inattivo alla creazione, la distribuzione del flusso di lavoro ha esito negativo. Questo problema si verifica se il flusso di lavoro viene impostato come inattivo alla creazione ma non influisce su flussi di lavoro modificati per essere impostati come inattivi dopo la distribuzione.

**Soluzione:**

Quando si crea e si distribuisce un flusso di lavoro, impostarlo come attivo e quindi distribuirlo. Dopo aver correttamente distribuito il flusso di lavoro, è possibile modificarlo per impostarlo come inattivo.

## La rimozione di un Response Group dal pool del proprietario impedisce al Response Group del pool di backup di accettare eventuali chiamate in arrivo durante il failover se il Response Group è stato importato nel pool di backup (3016214)

**Problema:**

Se un Response Group di proprietà del pool principale è stato importato in un pool di backup senza sovrascrivere il proprietario e il Response Group viene rimosso dal pool del proprietario, il Response Group nel pool di backup non accetterà eventuali chiamate in arrivo durante il failover.

**Soluzione:**

È necessario ridistribuire il Response Group nel pool principale. Sarà quindi necessario esportare la configurazione del Response Group dal pool principale e importarla di nuovo nel pool di backup.

È inoltre possibile ricreare il Response Group nel pool di backup. In questo caso, il pool di backup sarà il pool del proprietario del Response Group.

## Non è possibile recuperare una chiamata parcheggiata da applicazione Parcheggio di chiamata se la richiesta di recupero viene effettuata per conto di un Response Group (3211798)

**Problema:**

Quando si verificano le condizioni indicate di seguito, la richiesta di recupero di una chiamata parcheggiata ha esito negativo:

  - Un agente fa parte di un Response Group anonimo

  - L'agente tenta di recuperare una chiamata parcheggiata da applicazione Parcheggio di chiamata tramite il Response Group anonimo

  - L'agente tenta di recuperare la chiamata componendo il numero tramite l'opzione di chiamata per contro di un altro oppure tramite la stessa opzione nel client operatore Lync

**Soluzione:**

Non sono previste soluzioni alternative per questo problema. La chiamata parcheggiata deve essere recuperata senza effettuare l'operazione per conto di un Response Group.

## Pannello di controllo di Lync Server, Generatore di topologie e Strumento di pianificazione

## Limitazioni dello strumento di pianificazione (3331056 e 3331059)


> [!NOTE]
> Le informazioni in questa sezione sono relative agli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.



**Problema:**

Lo strumento di pianificazione presenta le limitazioni seguenti per la pianificazione della distribuzione:

  - Sono supportati al massimo 10 siti centrali

  - Ogni sito centrale può includere un massimo di 14 siti di succursale

  - Ogni sito centrale può includere un massimo di 240.000 utenti

Inoltre, lo strumento di pianificazione non include valori per gli elementi seguenti quando viene calcolata la topologia consigliata:

  - Il numero di utenti ospitati online

  - La percentuale di utenti abilitati per la federazione XMPP

  - La percentuale di utenti che utilizzano Lync Web App

**Soluzione:**

Non è disponibile una soluzione per questi problemi. Per ulteriori informazioni sullo strumento di pianificazione, vedere [Progettazione della topologia per Lync Server 2013 mediante lo strumento di pianificazione](lync-server-2013-designing-the-topology-by-using-the-planning-tool.md).

## Lo strumento di pianificazione potrebbe non utilizzare gli indirizzi IP definiti in precedenza per la rete perimetrale quando vengono aggiornate le opzioni

**Problema:**

Dopo aver completato la progettazione con lo strumento di pianificazione, se si apportano modifiche alle opzioni della rete perimetrale, è possibile che vengano aggiunti altri indirizzi IP anziché aggiornare quelli esistenti. Questo problema può verificarsi quando si visualizzano i dettagli del diagramma di rete perimetrale, si seleziona **Fare clic qui per aggiornare le opzioni** e quindi, nella finestra di dialogo Opzioni di configurazione, si seleziona **Per i servizi Edge nel server perimetrale voglio usare gli stessi FQDN e indirizzi IP, ma porte diverse** . Con l'applicazione delle modifiche, è possibile che allo schema vengano aggiunti nuovi indirizzi IP e server perimetrali.

**Soluzione:**

Al momento non è disponibile una soluzione per questo problema.

## In Pannello di controllo di Lync Server, l'opzione "Sposta tutti gli utenti nel pool" potrebbe non funzionare come previsto (3199270)

**Problema:**

Quando si usa il Pannello di controllo di Lync Server per spostare tutti gli utenti da un pool a un altro in un ambiente Active Directory complesso, ad esempio con più controller di dominio e domini padre/figlio, potrebbe essere restituito il messaggio di errore “L'utente specificato non è legacy. Utilizzare invece il cmdlet Move-CsUser”. Si tratta del risultato dei tempi di replica più lunghi in ambienti Active Directory complessi.

**Soluzione:**

Per risolvere questo problema, effettuare una delle operazioni seguenti:

  - Usare i filtri nel Pannello di controllo di Lync Server per cercare utenti legacy, selezionarli e quindi usare il comando **Sposta utenti selezionati nel pool** invece di **Sposta tutti gli utenti nel pool** .

  - Usare la Lync Server Management Shell per spostare gli utenti legacy in batch mediante cmdlet Lync Server.

## Il Pannello di controllo di Lync Server smette di funzionare in ambienti VMware dopo che plug-in per il browser Microsoft Silverlight viene aggiornato alla versione 5 (3199270)

**Problema:**

Se si usa il Pannello di controllo di Lync Server in un ambiente VMware, il Pannello di controllo di Lync Server potrebbe smettere di funzionare dopo aver aggiornato Silverlight alla versione 5.

**Soluzione:**

Per risolvere questo problema, effettuare una delle operazioni seguenti:

  - Disinstallare Silverlight 5 e installare Silverlight 4 da [http://go.microsoft.com/fwlink/?linkid=149156\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=149156%26clcid=0x410).

  - Aprire il Pannello di controllo di Lync Server da un computer che non sia un computer virtuale VMware.
    
    Per aprire il Pannello di controllo di Lync Server da un computer remoto, installare gli strumenti di amministrazione di Lync Server nel computer e quindi avviare il Pannello di controllo di Lync Server dal menu **Start** di Windows.
    
    È anche possibile aprire il Pannello di controllo di Lync Server immettendone l'URL in un Web browser. L'URL è analogo a https://\<fqdn\_pool\_frontend\>/cscp.

## Un amministratore non riesce a eseguire il cmdlet Uninstall-csMirrorDB dopo la rimozione del database di mirroring in Generatore di topologie (3199266)

**Problema:**

Quando un amministratore disabilita un database di mirroring in Generatore di topologie e quindi tale database viene eliminato in Generatore di topologie, viene visualizzato un messaggio nell'Elenco attività dell'amministratore per l'esecuzione del cmdlet **Uninstall-csMirrorDatabase** allo scopo di rimuovere il mirroring da SQL Server. Quando l'amministratore tenta di eseguire il cmdlet, questo ha esito negativo.

**Soluzione:**

Per rimuovere il mirroring SQL di un pool in Generatore di topologie, è innanzitutto necessario usare un cmdlet per rimuovere il mirroring in SQL Server. Sarà quindi possibile usare Generatore di topologie per rimuovere il mirroring dalla topologia. Per rimuovere il mirroring in SQL Server, usare il cmdlet seguente:

    Uninstall-CsMirrorDatabase -SqlServerFqdn <SQLServer FQDN> [-SqlInstanceName <SQLServer instance name>] -DatabaseType <Application | Archiving | CentralMgmt | Monitoring | User | BIStaging | PersistentChat | PersistentChatCompliance> [-DropExistingDatabasesOnMirror] [-Verbose]

Ad esempio, per rimuovere il mirroring ed eliminare i database degli utenti, digitare quanto segue:

    Uninstall-CsMirrorDatabase -SqlServerFqdn primaryBE.contoso.com -SqlInstanceName rtc -Verbose -DatabaseType User -DropExistingDatabasesOnMirror

Il parametro *DropExistingDatabasesOnMirror* determina l'eliminazione dei database interessati dal mirroring. Per rimuovere quindi il mirroring dalla topologia, procedere come segue:

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul pool e scegliere **Modifica proprietà** .

2.  Deselezionare **Abilita mirroring dell'archivio SQL** e fare clic su **OK** .

3.  Pubblicare la topologia.

> [!IMPORTANT]  
> Ogni volta che si apporta una modifica a una relazione di mirroring dei database back-end, è necessario riavviare tutti i Front End Server nel pool.

## Vengono restituiti errori di convalida in Generatore di topologie quando un amministratore tenta di rimuovere una distribuzione con un pool Front End a cui è associato un archivio di controllo (3199266)

**Problema:**

Se un amministratore tenta di usare il comando **Rimuovi distribuzione** in Generatore di topologie per rimuovere una distribuzione che include un pool Front End a cui è associato un archivio di controllo, viene visualizzato un errore di convalida in Generatore di topologie e l'azione non viene eseguita.

**Soluzione:**

Per risolvere questo problema, effettuare una delle operazioni seguenti:

  - Rimuovere l'archivio di controllo prima di tentare di rimuovere la distribuzione.

  - Aggiungere un archivio di controllo per il pool Front End e quindi rimuoverlo.

## Le informazioni sulla distribuzione di server Chat persistente sono incoerenti tra lo Strumento di pianificazione e Generatore di topologie (3012228)

**Problema:**

Quando Lync Server 2013, Strumento di pianificazione genera il diagramma della topologia di siti per una distribuzione di server Chat persistente con il ripristino di emergenza abilitato, tale diagramma include più siti (fisici) con server Chat persistente assegnati in modo omogeneo a ogni sito. In Generatore di topologie, tutti i server Chat persistente sono rappresentati come appartenenti a un singolo sito (logico) e sono elencati nello stesso nodo del pool di server Chat persistente.

**Soluzione:**

Attualmente non esiste una soluzione a questo problema. L'utente deve analizzare l'output dello Strumento di pianificazione per la distribuzione di server Chat persistente e modificare il piano in modo da soddisfare esigenze specifiche.

## Localizzazione

## Monitoraggio

## In determinate circostanze, nella Distribuzione guidata dei rapporti di monitoraggio vengono visualizzati caratteri errati se si usa una versione per l'Asia orientale di Lync Server (3113565)

**Problema:**

Quando si usa una versione per l'Asia orientale di Lync Server 2013, ad esempio quelle in cinese (semplificato o tradizionale), giapponese o coreano, in un sistema operativo le cui impostazioni locali non sono impostate su una lingua dell'Asia orientale, nella Distribuzione guidata dei rapporti di monitoraggio vengono visualizzati punti interrogativi o altri caratteri invece dei messaggi localizzati.

**Soluzione:**

Per risolvere il problema, usare le medesime impostazioni locali per il sistema operativo e Lync Server 2013 in modo da visualizzare tutti i messaggi correttamente.

## Pannello di controllo di Lync Server

## In alcuni casi, il primo elemento nella barra di spostamento superiore di una pagina del Pannello di controllo di Lync Server sparisce quando si fa clic sull'ultimo elemento della barra stessa (3158118)

**Problema:**

Esistono tre casi noti in cui se si fa clic sull'ultimo elemento nella barra di spostamento superiore di una pagina del Pannello di controllo di Lync Server il primo elemento della barra sparisce:

  - Nella versione in lingua francese nella pagina "Féderation et accès externe", l'elemento "Stratégie d'accès externe" sparisce se si fa clic su "Partenaires fédérés XMPP".

  - Nella versione in lingua tedesca, nella pagina "Clients", l'elemento "Clientversionskonfiguration" sparisce se si fa clic su "Pushbenachrichtigungskonfiguration".

  - Nella versione in lingua russa, nella pagina "Конфигурация сети" l'elemento "Глобально" sparisce se si fa clic su "Маршрут региона".

**Soluzione:**

Per risolvere questo problema, aggiornare la pagina del Pannello di controllo di Lync Server nel browser. La pagina verrà caricata nel browser con tutti gli elementi nella barra di spostamento superiore visualizzati.

## Rubrica

## L'indicizzazione nella Rubrica non funziona come previsto in alcune lingue (3336047)


> [!NOTE]
> Le informazioni in questa sezione sono relative agli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.



Se le proprietà di un utente contengono un campo indicizzato e tale campo contiene solo caratteri che non è possibile indicizzare, l'utente non verrà visualizzato nelle ricerche eseguite nella Rubrica.

Non è possibile indicizzare i caratteri e le impostazioni locali seguenti:

  - Caratteri cirillici, greci e armeni in maiuscolo

  - Caratteri accentati in maiuscolo

  - Tailandese

  - Lao

  - Myanmar

  - Devanagari

  - Etiopico

  - Tibetano

  - Bengali

  - Gujarati

  - Telugu

  - Caratteri in tutte le altre lingue indiane indoeuropee

## Lync Web App, Web Scheduler e componenti Web

## Il fallback della lingua per alcune lingue di Lync Web Scheduler, Dial-In, Join Launcher, Persistent Chat Room Management e OCTab poterebbe non funzionare come previsto (3079700)

**Problema:**

Quando si seleziona un'impostazione locale neutra in un Web browser (in Internet Explorer, ad esempio, il nome della lingua senza ulteriori specifiche, come "Norvegese \[no\]") invece di un'impostazione locale che specifica lingua, alfabeto e paese (ad esempio "Norwegian, Bokmål (Norvegia) \[nb-NO\]"), si potrebbero verificare comportamenti di visualizzazione imprevisti per determinate lingue in Lync Web Scheduler, Dial-In, Join Launcher, Persistent Chat Room Management e OCTab. Ad esempio, gli utenti potrebbero vedere la pagina in inglese se è selezionata una delle lingue seguenti:

  - Norvegese

  - Portoghese

  - Serbo

**Soluzione:**

Se si vuole selezionare una lingua con impostazioni locali neutre, accertarsi sempre di aggiungere anche la lingua con impostazioni specifiche (alfabeto e/o codice paese) come lingua aggiuntiva nell'elenco di preferenze del browser.

## Esiste un supporto limitato per le impostazioni locali in azeri e uzbeco quando si utilizzano Lync Web Scheduler, Dial-In, Join Launcher, Persistent Chat Room Management e OCTab in alcuni Web browser (3336748)


> [!NOTE]
> Le informazioni in questa sezione sono relative agli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.



**Problema:**

Quando si utilizza Internet Explorer 8 o Internet Explorer 9 e si imposta la lingua del browser su Azeri (alfabeto latino) o Uzbeco (alfabeto latino), le pagine di Dial-In e Join Launcher verranno visualizzate in inglese o nella lingua preferita impostata nel browser.

Se si utilizzano i browser Firefox o Chrome e si imposta la lingua su Azeri (alfabeto latino) o Uzbeco (alfabeto latino,) Lync Web App, Lync Web Scheduler e RGS OCTab verranno visualizzati in inglese o nella lingua preferita impostata per il browser.

Le impostazioni locali in Uzbeco (alfabeto latino) non sono supportate nel browser Safari.

**Soluzione:**

Non è disponibile una soluzione per questi problemi.

## Manca la freccia a discesa per l'elenco "Partecipa a riunione" nella versione romena di Lync Web App (3154899)

**Problema:**

Quando un utente che usa la versione romena di Lync Web App esegue le operazioni seguenti, la freccia a discesa per l'elenco a discesa **Partecipa a riunione** non viene visualizzata:

1.  Selezionare **Memorizza account su questo computer** nella scheda **Generale** .

2.  Selezionare la scheda **Telefono** .

3.  Fare clic sull'elenco a discesa **Partecipa a riunione** .
    
    Gli utenti non vedranno una freccia indicante che sono disponibili altre opzione oltre a quella predefinita **Lync Web App**, ovvero **Non accedere all'audio** (in romeno, "Nu se asociaža la componenta audio") e **Nuovo numero** " (in romeno, "Numar nou").

**Soluzione:**

Anche se la freccia dell'elenco a discesa non è visualizzata, gli utenti possono comunque selezionare le altre impostazioni dell'elenco facendo clic sul valore predefinito.

## Quando si usa la versione turca di Lync Web Scheduler, non è possibile salvare una riunione se si usa l'opzione "Persone scelte dall'utente" in "Relatori" (3169483)

**Problema:**

Quando si crea o si modifica una riunione nella versione turca di Lync Web Scheduler, l'opzione "Persone scelte dall'utente" in "Relatori" non è supportata. Se si seleziona questa opzione, non sarà possibile salvare la riunione. Viene invece visualizzato un messaggio d'errore indicante che una o più persone non possono essere relatori.

**Soluzione:**

Per risolvere questo problema, gli utenti possono utilizzare l'opzione predefinita "Persone appartenenti alla società" o qualsiasi altra opzione, ad esempio "Solo organizzatore" oppure "Tutti incluse le persone non appartenenti alla società". L'organizzatore può abbassare o alzare di livello le persone nei ruoli corretti in un secondo momento, dopo che hanno effettuato l'accesso alla riunione.

In alternativa, gli utenti in grado di parlare un'altra lingua possono cambiare la scelta della lingua nel browser selezionando una delle 43 supportate e tentare quindi di usare l'opzione “Persone scelte dall'utente”.

## Copyright

Questo documento supporta una versione preliminare di un prodotto software che potrebbe subire modifiche sostanziali prima della versione finale per utilizzo commerciale e contiene informazioni riservate e proprietarie di Microsoft Corporation. Il presente documento viene divulgato ai sensi di un accordo di riservatezza tra il destinatario e Microsoft. Questo documento è esclusivamente per scopi informativi. Microsoft esclude ogni garanzia espressa o implicita in questo documento. Le informazioni contenute nel presente documento, inclusi riferimenti a URL e ad altri siti Web Internet, sono soggette a modifiche senza preavviso. L'intero rischio conseguente all'uso di questo documento o i risultati da esso derivanti rimangono a carico dell'utente. Se non specificato diversamente, ogni riferimento a società, organizzazioni, prodotti, nomi di dominio, indirizzi di posta elettronica, logo, persone, luoghi ed eventi utilizzati negli esempi contenuti è puramente casuale e ha il solo scopo di illustrare l'uso del prodotto Microsoft. Il rispetto di tutte le applicabili leggi in materia di copyright è esclusivamente a carico dell'utente. Fermi restando tutti i diritti coperti da copyright, nessuna parte di questo documento potrà comunque essere riprodotta o inserita in un sistema di riproduzione o trasmessa in qualsiasi forma e con qualsiasi mezzo (in formato elettronico, meccanico, su fotocopia, come registrazione o altro) per qualsiasi scopo, senza il permesso scritto di Microsoft Corporation..

Microsoft può essere titolare di brevetti, domande di brevetto, marchi, copyright o altri diritti di proprietà intellettuale relativi all'oggetto di questo documento. Salvo quanto espressamente previsto in un contratto scritto di licenza Microsoft, la consegna di questo documento non implica la concessione di alcuna licenza su tali brevetti, marchi, copyright o altra proprietà intellettuale.

© 2012 Microsoft Corporation. Tutti i diritti riservati.

Microsoft, Windows, Windows Live, Active Directory, Internet Explorer, MSN, Outlook e SQL sono marchi o marchi registrati di Microsoft Corporation negli Stati Uniti e/o negli altri paesi.

Tutti gli altri marchi sono proprietà dei rispettivi proprietari.

