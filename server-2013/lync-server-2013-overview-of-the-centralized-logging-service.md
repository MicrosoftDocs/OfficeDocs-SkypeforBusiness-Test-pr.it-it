---
title: Panoramica del servizio di registrazione centralizzato
TOCTitle: Panoramica del servizio di registrazione centralizzato
ms:assetid: 975718a0-f3e3-404d-9453-6224e73bfdd0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688145(v=OCS.15)
ms:contentKeyID: 49887669
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Il servizio di registrazione centralizzato è progettato per consentire la raccolta controllata di dati con ambiti più o meno ampi. È possibile raccogliere dati da tutti i server della distribuzione contemporaneamente, definire specifici elementi di cui tenere traccia, impostare flag di traccia e restituire risultati della ricerca da un singolo computer o un'aggregazione di tutti i dati di tutti i server. Il servizio di registrazione centralizzato viene eseguito su tutti i server della distribuzione. L'architettura del servizio di registrazione centralizzato è costituita dagli agenti e servizi seguenti:

  - *Agente del servizio di registrazione centralizzato*   ClsAgent.exe è il file eseguibile del servizio che comunica con il controller e riceve i comandi che vi vengono eseguiti dall'amministratore. L'agente viene eseguito come servizio in ogni computer Lync Server. Quando l'agente riceve un comando, lo esegue, invia messaggi ai componenti definiti per la traccia e scrive i log di traccia su disco. Legge inoltre i log di traccia per il computer e reinvia i dati di traccia al controller quando richiesto. ClsAgent è in attesa dei comandi sulle porte seguenti: **TCP 50001**, **TCP 50002** e **TCP 50003**.

  - *Controller servizio di registrazione centralizzato*   ClsControllerLib.dll è il motore di esecuzione comandi per la Lync Server Management Shell e per ClsController.exe. CLSControllerLib.dll invia comandi di avvio, arresto, scaricamento e ricerca a ClsAgent. Quando vengono inviati comandi di ricerca, i log risultati vengono restituiti a ClsControllerLib.dll e aggregati. Il controller è responsabile dell'invio di comandi all'agente, della ricezione dello stato di tali comandi e della gestione dei dati dei file di log della ricerca quando vengono restituiti da tutti gli agenti nei computer dell'ambito di ricerca e dell'aggregazione dei dati di log in un set di output ordinato e significativo. Le informazioni negli argomenti seguenti sono incentrate sull'uso della Lync Server Management Shell. ClsController.exe è limitato a un sottoinsieme delle caratteristiche e delle funzioni disponibili nella Lync Server Management Shell. Informazioni su ClsController.exe sono disponibile alla riga di comando digitando `ClsController` nella directory predefinita C:\\Programmi\\File comuni\\Microsoft Lync Server 2013\\ClsAgent

**Comunicazioni di ClsController a ClsAgent**

![Relazione tra CLSController e CLSAgent.](images/JJ688145.68c90811-5cf9-4a84-95b7-ea9ffc61eac4(OCS.15).jpg "Relazione tra CLSController e CLSAgent.")

I comandi vengono eseguiti mediante l'interfaccia della riga di comando di Windows Server oppure usando la Lync Server Management Shell. I comandi vengono eseguiti nel computer a cui è connesso l'utente e inviati al ClsAgent locale o agli altri computer e pool della distribuzione.

ClsAgent mantiene un file di indice di tutti i file CACHE che si trova nel computer locale. ClsAgent li alloca in modo che vengano distribuiti uniformemente tra i volumi definiti mediante l'opzione CacheFileLocalFolders, senza mai occupare più dell'80% di ogni volume (ovvero il percorso della cache locale e la percentuale sono configurabili mediante il cmdlet **Set-CsClsConfiguration**). ClsAgent è anche responsabile dei file di traccia degli eventi (etl) in scadenza memorizzati nella cache del computer locale. Dopo due settimane (il periodo di tempo è configurabile mediante il cmdlet **Set-CsClsConfiguration**) questi file vengono copiati in una condivisione ed eliminati dal computer locale. Per dettagli, vedere [Set-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsConfiguration). Quando si riceve una richiesta di ricerca, i criteri di quest'ultima vengono usati per selezionare il set di file etl memorizzati nella cache per eseguire la ricerca in base ai valori nell'indice mantenuto dall'agente.


> [!NOTE]
> I file che vengono spostati nella condivisione di file dal computer locale possono essere ricercati da ClsAgent. Dopo che ClsAgent sposta i file nella condivisione, la scadenza e la rimozione dei file non vengono gestite da ClsAgent. È necessario definire un'attività amministrativa per monitorare le dimensioni dei file nella condivisione ed eliminarli o archiviarli.



I file di log risultanti possono essere letti e analizzati mediante diversi strumenti, tra cui **Snooper.exe** e qualsiasi strumento in grado di leggere file di testo, come **Notepad.exe**. Snooper.exe fa parte degli strumenti di debug di Lync Server 2013 ed è disponibile come download dal Web.

Analogamente a OCSLogger, il servizio di registrazione centralizzato può tenere traccia di diversi componente e offre opzioni per selezionare i flag come TF\_COMPONENT e TF\_DIAG. servizio di registrazione centralizzato include inoltre le opzioni a livello di registrazione di OCSLogger.

Il vantaggio maggiore correlato all'uso della Windows PowerShell rispetto al ClsController della riga di comando consiste nel fatto che è possibile configurare e definire nuovi scenari usando provider selezionati incentrati su spazio dei problemi, flag personalizzati e livelli di registrazione. Gli scenari disponibili in ClsController sono limitati a quelli definiti per l'eseguibile.

Nelle versioni precedenti, OCSLogger.exe consente agli amministratori e al personale di supporto di raccogliere file di traccia dai computer nella distribuzione. OCSLogger, nonostante tutti i punti di forza, ha una lacuna. È possibile collegare i log a un solo computer alla volta. È possibile accedere a più computer usando copie separate di OCSLogger, tuttavia ciò produce più log e nessun modo semplice per aggregare i risultati.

Quando un utente richiede una ricerca di log, ClsController determina i computer a cui inviare la richiesta (in base agli scenari selezionati). Determina anche se la ricerca deve essere inviata alla condivisione di file in cui sono stati salvati i file con estensione etl. Quando i risultati di riceva vengono restituiti a ClsController, il controller li unisce in un singolo set di risultati in ordine cronologico presentato all'utente. Gli utenti possono salvare i risultati di ricerca nel proprio computer locale per ulteriori analisi.

Quando si avvia una sessione di registrazione, si specificano scenari relativi al problema da risolvere. È possibile eseguire due scenari alla volta. Uno di questi scenari deve essere quello AlwaysOn, ovvero deve essere sempre in esecuzione nella distribuzione per raccogliere informazioni su tutti i computer, i pool e i componenti.

> [!IMPORTANT]  
> Per impostazione predefinita, lo scenario AlwaysOn non è in esecuzione nella distribuzione. È necessario avviarlo in modo esplicito. Una volta avviato, il servizio continua a essere eseguito fino all'arresto esplicito e lo stato di esecuzione permane nonostante i riavvii del computer. Per informazioni dettagliate sull'avvio e l'arresto degli scenari, vedere <a href="lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md">Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato</a> e <a href="lync-server-2013-using-stop-for-the-centralized-logging-service.md">Utilizzo del comando Stop per il servizio di registrazione centralizzato</a>.

Quando si verifica un problema, avviare un secondo scenario correlato al problema segnalato. Riprodurre il problema e arrestare la registrazione per il secondo scenario. Iniziare le ricerche dei log relativi al problema segnalato. La raccolta aggregata dei log produce un file di log contenente i messaggi di traccia di tutti i computer nel sito oppure dell'ambito globale della distribuzione. Se la ricerca restituisce più dati di quanti sia possibile analizzarne (condizione nota in genere come rapporto segnale/rumore, in cui il rumore è troppo elevato), è possibile eseguire un'altra ricerca con parametri più limitati. A questo punto, è possibile iniziare a osservare i modelli risultati in modo da formarsi un quadro più chiaro del problema. Infine, dopo aver eseguito un paio di ricerche perfezionate, è possibile individuare i dati rilevanti per il problema e dedurne la causa principale.

> [!TIP]  
> Quando si presenta uno scenario di problema in Lync Server, iniziare chiedendosi quali informazioni sono disponibili sul problema. Se si delineano i confini del problema, è possibile eliminare una gran parte delle entità operative di Lync Server.<br />Considerare ad esempio uno scenario in cui si sa che gli utenti non ricevono risultati aggiornati quando cercano un contatto. Non sarà in questo caso necessario cercare le cause del problema nei componenti multimediali, in VoIP aziendale, nei servizi per conferenza e in numerosi altri componenti. Ciò che potrebbe non essere noto è la posizione effettiva da cui trae origine il problema: lato client o lato server? I contatti sono raccolti da Active Directory mediante User Replicator e recapitare al client mediante il server della Rubrica (ABServer). ABServer ottiene gli aggiornamenti dal database RTC (dopo i dati sono stati scritti da User Replicator) e li raccoglie in file della rubrica per impostazione predefinita alle 1.30. I clienti Lync Server recuperano la nuova rubrica in base a una pianificazione casuale. Poiché si conosce la modalità di funzionamento del processo, è possibile ridurre la ricerca della causa potenziale individuandola in un problema correlato alla raccolta dei dati di Active Directory da parte di User Replicator, al mancato recupero o creazione dei file di rubrica da parte di ABServer oppure al mancato download del file della rubrica da parte dei client.
