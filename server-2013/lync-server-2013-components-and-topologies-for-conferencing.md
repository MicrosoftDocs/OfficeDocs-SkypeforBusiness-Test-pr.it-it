---
title: 'Lync Server 2013: Componenti e topologie per le conferenze'
TOCTitle: Componenti e topologie per le conferenze
ms:assetid: eb83052a-3360-4ba1-a6a0-6ee419942809
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399061(v=OCS.15)
ms:contentKeyID: 49302353
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per le conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-04_

Quando si seleziona il servizio di conferenza in Generatore di topologie, questo viene distribuito come parte del Front End Server o del server Standard Edition. La conferenza telefonica con accesso esterno e la condivisione PowerPoint richiedono configurazioni e componenti aggiuntivi. Nelle sezioni seguenti vengono descritti i componenti e le topologie supportati per Web Conferencing, A/V Conferencing e conferenza telefonica con accesso esterno.

## Componenti supportati

Gli unici componenti necessari per Web Conferencing e A/V Conferencing sono i Front End Server o i server Standard Edition dell'organizzazione. Per un elenco dei requisiti hardware e software per i Front End Server e i server Standard Edition, vedere [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) e [Supporto dell'infrastruttura e del software server in Lync Server 2013](lync-server-2013-server-software-and-infrastructure-support.md).

Lync Server 2013 utilizza Office Web Apps e Server Office Web Apps per gestire la condivisione e il rendering delle presentazioni PowerPoint. Per informazioni dettagliate sull'installazione e la configurazione di Server Office Web Apps, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

In aggiunta ai requisiti per Web Conferencing e A/V Conferencing, la conferenza telefonica con accesso esterno richiede anche l'utilizzo dei componenti seguenti di Lync Server 2013:

  - **Servizio dell'applicazione**    Servizio applicazione offre una piattaforma per la distribuzione, l'hosting e la gestione delle applicazioni per comunicazioni unificate (UC). La conferenza telefonica con accesso esterno utilizza due applicazioni UC che richiedono il Servizio applicazione: Operatore Conferenza e Annuncio conferenza. Il Servizio applicazione viene installato e attivato per impostazione predefinita in ogni Front End Server in un pool Front End e in ogni server Standard Edition quando si distribuisce un carico di lavoro di conferenza e si seleziona l'opzione di conferenza telefonica con accesso esterno.

  - **applicazione Operatore Conferenza**    applicazione Operatore Conferenza è un'applicazione per comunicazioni unificate in grado di accettare chiamate PSTN (Public Switched Telephone Network), riprodurre istruzioni e inserire le chiamate in una conferenza audio/video. applicazione Operatore Conferenza viene installato e attivato per impostazione predefinita quando si distribuisce un carico di lavoro di conferenza e si seleziona l'opzione di conferenza telefonica con accesso esterno.

  - **applicazione Annuncio conferenza**applicazione Annuncio conferenza è un'applicazione per comunicazioni unificate in grado di riprodurre toni e istruzioni per i partecipanti PSTN in relazione a determinate azioni, ad esempio quando i partecipanti prendono parte a una conferenza o escono da essa, l'audio dei partecipanti viene attivato o disattivato, un utente accede alla sala di attesa della conferenza oppure la conferenza viene bloccata o sbloccata. applicazione Annuncio conferenza supporta anche i comandi DTMF (Dual-Tone MultiFrequency) dal tastierino del telefono. applicazione Annuncio conferenza viene automaticamente installato e attivato per impostazione predefinita quando si distribuisce un carico di lavoro di conferenza e si seleziona l'opzione di conferenza telefonica con accesso esterno.

  - **pagina Impostazioni conferenza telefonica con accesso esterno**   Nella pagina Impostazioni conferenza telefonica con accesso esterno vengono visualizzati i numeri con accesso esterno alla conferenza con le lingue disponibili, le informazioni sulle conferenze assegnate (ovvero per le riunioni che non richiedono una pianificazione) e i controlli DTMF di conferenza e viene supportata la gestione del PIN e delle informazioni sulle conferenze assegnate. La pagina Impostazioni conferenza telefonica con accesso esterno viene installata automaticamente come parte dei servizi Web.

  - **Lync Server 2013, Mediation Server e gateway PSTN**   Le conferenze telefoniche con accesso esterno richiedono un Mediation Server per la conversione dei segnali e, in alcune configurazioni, dei contenuti multimediali, tra Lync Server 2013 e il gateway PSTN, nonché un gateway PSTN per la conversione dei segnali e dei contenuti multimediali tra Mediation Server e il gateway PSTN. Per le conferenze telefoniche con accesso esterno, è necessario distribuire almeno un Mediation Server e almeno uno dei seguenti:
    
      - Gateway PSTN
    
      - IP-PBX
    
      - SBC (Session Border Controller), per un provider di servizi di telefonia Internet a cui viene eseguita la connessione tramite la configurazione di un trunk SIP
    

    > [!NOTE]
    > Se si distribuisce anche VoIP aziendale, Mediation Server e i gateway PSTN fanno parte della distribuzione di VoIP aziendale. Se non si distribuisce VoIP aziendale, è necessario distribuire almeno un Mediation Server e almeno un gateway PSTN, un sistema IP-PBX o un servizio SBC per le conferenze telefoniche con accesso esterno.



  - **Archivio file**   L'archivio file viene utilizzato per i file audio dei nomi registrati. Si tratta di un componente standard di ogni distribuzione di Enterprise Edition o Standard Edition.

  - **Archivio utente**   L'archivio utente viene utilizzato per archiviare i PIN degli utenti di Lync Server 2013. I PIN vengono sottoposti a hashing. Si tratta di un componente standard di ogni distribuzione di Enterprise Edition o Standard Edition.

  - **Pannello di controllo di Lync Server**   Alcune impostazioni di accesso esterno possono essere configurate utilizzando il Pannello di controllo di Lync Server.

  - **Lync Server Management Shell**   Tutte le impostazioni di accesso esterno possono essere configurate utilizzando i cmdlet di Lync Server Management Shell. Sono disponibili cmdlet di Lync Server Management Shell per la distribuzione, la configurazione, l'esecuzione, il monitoraggio e la risoluzione dei problemi dell' applicazione Operatore Conferenza e dell' applicazione Annuncio conferenza. Per informazioni dettagliate su cmdlet specifici, vedere la documentazione di Lync Server Management Shell.

## Topologie supportate

In Lync Server 2013 il server che esegue i servizi di conferenza viene sempre collocato con i Front End Server o con i server Standard Edition. Durante la distribuzione iniziale, il Generatore di topologie offre la possibilità di includere i servizi di conferenza nella topologia. È anche possibile utilizzare il Generatore di topologie per aggiungere i servizi di conferenza a una distribuzione esistente. Per informazioni dettagliate, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md).

## Topologie di conferenza telefonica con accesso esterno

È possibile distribuire le conferenze telefoniche con accesso esterno nelle topologie e configurazioni seguenti:

  - Lync Server 2013Standard Edition

  - Lync Server 2013Enterprise Edition

  - Con o senza VoIP aziendale

È possibile distribuire il Servizio applicazione, l' applicazione Operatore Conferenza e l' applicazione Annuncio conferenza in un sito centrale, ma non in un sito di succursale.


> [!NOTE]
> Se si distribuiscono le conferenze con accesso esterno, è necessario distribuirle in ogni pool in cui si distribuisce il servizio di conferenza di Lync Server 2013. Non è necessario assegnare numeri di accesso in ogni pool, ma è necessario distribuire la caratteristica di conferenza con accesso esterno in ogni pool. Questo requisito supporta la caratteristica del nome registrato quando un utente chiama un numero di accesso da un pool per partecipare a una conferenza di Lync Server 2013 in un altro pool.



## Topologie supportate per Lync Server 2013 e Office Web Apps

In Lync Server 2013 è possibile configurare Server Office Web Apps nei modi seguenti. A seconda delle esigenze, è possibile:

  - **Installare sia Lync Server 2013 che Server Office Web Apps in locale, dietro il firewall dell'organizzazione e nella stessa area di rete.** Con questa topologia, l'accesso esterno a Server Office Web Apps verrà offerto tramite il server proxy inverso. Sia Lync Server 2013 che Server Office Web Apps (o una server farm di Server Office Web Apps) vengono installati in locale, dietro il firewall dell'organizzazione. Server Office Web Apps andrebbe idealmente installato nella stessa area di rete di Lync Server.
    
    I client Lync esterni possono connettersi a Lync Server 2013 e a Server Office Web Apps utilizzando un server proxy inverso, ovvero un server che riceve le richieste provenienti da Internet e le inoltra alla rete interna. Non è necessario che i client interni utilizzino il server proxy inverso perché possono connettersi a Server Office Web Apps direttamente. Questa topologia è ideale in presenza di una server farm di Server Office Web Apps dedicata che viene utilizzata solo da Lync Server 2013.

  - **Utilizzo di un Server Office Web Apps distribuito esternamente**
    
    In questa topologia Lync Server 2013 viene distribuito in locale e utilizza un Server Office Web Apps distribuito all'esterno dell'area di rete di Lync Server. Questo può accadere quando Server Office Web Apps viene condiviso tra più applicazioni aziendali ed è distribuito in una rete che richiede Lync Server per utilizzare l'interfaccia esterna di Server Office Web Apps e viceversa.
    
    Non è necessario installare un server proxy inverso. Tutte le richieste inviate da Server Office Web Apps a Lync Server 2013 vengono piuttosto instradate attraverso il server perimetrale. I client Lync sia interni che esterni si connettono a Server Office Web Apps utilizzando l'URL esterno.
    
    Se Server Office Web Apps viene distribuito all'esterno del firewall interno, selezionare l'opzione **Il server Office Web Apps è distribuito in una rete esterna (perimetro/Internet)** in Generatore di topologie. Per ulteriori dettagli, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

Indipendentemente dalla topologia selezionata, è fondamentale aprire le porte del firewall corrette. È necessario verificare che i nomi DNS, gli indirizzi IP e le porte non siano bloccati dai firewall in Server Office Web Apps, nel servizio di bilanciamento del carico o in Lync Server.


> [!NOTE]
> Un altro modo per fornire accesso esterno a Server Office Web Apps consiste nel distribuire il server nella rete perimetrale. Se si opta per questa soluzione, tenere a mente che l'installazione di Server Office Web Apps richiede che il computer server sia un membro del dominio di Active Directory. A meno che i criteri di rete non consentano che i computer inclusi all'interno della rete perimetrale siano membri di Active Directory, è consigliabile non installare Server Office Web Apps nella rete perimetrale. È preferibile invece installare Server Office Web Apps nella rete interna e fornire agli utenti esterni l'accesso tramite il server proxy inverso.


