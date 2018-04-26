---
title: 'Lync Server 2013: Novità per i client'
TOCTitle: Novità per i client
ms:assetid: 5c144677-4d58-4fc3-8445-74b76c9fcf07
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204933(v=OCS.15)
ms:contentKeyID: 49300685
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Novità per i client in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-19_

In Microsoft Lync 2013 è stata riprogettata l'interfaccia utente e sono state introdotte nuove importanti funzionalità. Per gli amministratori, il client è ora incluso nel programma di installazione di Office e ciò consente un approccio facilitato alla distribuzione di Office e alla personalizzazione dei client nell'organizzazione.


> [!NOTE]
> Per una presentazione illustrata degli aggiornamenti dell'interfaccia utente di Lync 2013, vedere "Novità di Lync 2013" all'indirizzo <A href="http://go.microsoft.com/fwlink/?linkid=273885">http://go.microsoft.com/fwlink/?LinkId=273885</A>.



## Integrazione con l'installazione di Office

Il client Lync 2013 e il componente aggiuntivo per riunioni online per Lync 2013, che supporta la gestione delle riunioni dal client per la collaborazione e la messaggistica Outlook, sono ora entrambi inclusi nel programma di installazione di Office 2013.

Nelle versioni precedenti di Lync e Office Communicator è consentito l'utilizzo di Windows Installer per personalizzare e controllare l'installazione di Office. Dato che Lync 2013 è integrato nell'installazione di Office, è possibile utilizzare i metodi seguenti per personalizzare l'installazione di Lync 2013:

  - Utilizzare lo Strumento di personalizzazione di Office

  - Utilizzare il file Config.xml per eseguire le attività di installazione

  - Utilizzare le opzioni della riga di comando del programma di installazione


> [!NOTE]
> Il programma di installazione di Lync 2013 non include la disinstallazione delle versioni precedenti di Lync o Office Communicator. Il client Lync 2013 viene installato affiancato ad altri client Lync o Office Communicator.



Per informazioni dettagliate, vedere [Distribuzione di client Lync](lync-server-2013-deploying-lync-clients.md).

## Distribuzione di Criteri di gruppo

Dato che Lync 2013 è ora incluso nell'installazione di Office, è cambiato il metodo per distribuire le impostazioni di Criteri di gruppo di Lync. Nelle versioni precedenti di Lync e Office Communicator, è possibile utilizzare Communicator.adm per definire le impostazioni di Criteri di gruppo, mentre in Lync 2013 è ora possibile utilizzare i modelli amministrativi ADMX e ADML di Lync forniti insieme ai modelli amministrativi di Criteri di gruppo di Office.

Per informazioni dettagliate, vedere [Impostazione dei criteri di gruppo per Lync 2013](lync-server-2013-group-policy-settings-for-lync-2013.md).

## Aggiornamenti del componente aggiuntivo di Outlook per la pianificazione delle riunioni

Il componente aggiuntivo per riunioni online per Lync 2013 include funzionalità per la personalizzazione degli inviti alle riunioni e nuove opzioni per le riunioni.

  - Gli amministratori possono personalizzare gli inviti alle riunioni dell'organizzazione aggiungendo un logo personalizzato, un URL di supporto, un URL per la dichiarazione di non responsabilità legale o un testo personalizzato per il piè di pagina. Per informazioni dettagliate, vedere [Personalizzazione del componente aggiuntivo per riunioni online](lync-server-2013-customizing-the-online-meeting-add-in.md).

  - I nuovi controlli per la disattivazione dell'audio dei partecipanti consentono agli organizzatori delle riunioni di disattivare l'audio e il video dei partecipanti per impostazione predefinita.

## Plug-in VDI (Virtual Desktop Infrastructure)

Il client Lync 2013 supporta ora audio e video in un ambiente VDI (Virtual Desktop Infrastructure). Un utente può connettere un dispositivo audio o video (ad esempio un auricolare o una videocamera) al computer locale (ad esempio un thin client o un computer ricondizionato). L'utente può connettersi alla macchina virtuale, accedere al client Lync 2013 che esegue la macchina virtuale e partecipare a comunicazioni audio e video in tempo reale come se il client fosse in esecuzione in locale. In un ambiente desktop virtuale sono supportate le funzionalità seguenti:

  - Integrazione dei dispositivi per audio e video, incluso quanto segue:
    
      - Controlli di chiamata dal dispositivo
    
      - Integrazione della presenza nel dispositivo
    
      - Supporto di più HID (Human Interface Device)

  - Supporto di servizi di geolocalizzazione ed emergenza.

  - Supporto di tutte le modalità di Lync, inclusi messaggistica istantanea, audio, video, condivisione di applicazioni, condivisione del desktop, condivisione di PowerPoint, lavagna e trasferimento di file.

  - Supporto di audio e video nelle chiamate e nelle conferenze telefoniche a due.

Per informazioni sulla distribuzione del plug-in VDI, vedere [Distribuzione del plug-in VDI di Lync in Lync Server 2013](lync-server-2013-deploying-the-lync-vdi-plug-in.md).

## Miglioramenti relativi alle funzionalità video

Molte nuove funzionalità migliorano in modo sostanziale l'esperienza video per i partecipanti alle conferenze.

  - Le funzionalità video sono ottimizzate con rilevamento dei volti e framing intelligente, in modo che il video del partecipante si sposti automaticamente in modo che il volto rimanga centrato nel fotogramma.

  - È ora supportato il video ad alta definizione per le chiamate a due e le conferenze con più partecipanti. Gli utenti potranno usufruire di risoluzioni fino a 1080p HD.

  - I partecipanti possono scegliere tra diversi layout per le riunioni. Con la visualizzazione Raccolta vengono visualizzati i video o le immagini di tutti i partecipanti. Nella visualizzazione relatore viene mostrato il contenuto della riunione e solo il video o l'immagine del relatore corrente. La visualizzazione presentazione mostra solo il contenuto della riunione e la visualizzazione compatta include solo i controlli per la riunione.

  - Con la nuova funzionalità Raccolta, i partecipanti possono visualizzare più feed video contemporaneamente. Se alla conferenza partecipano più di cinque persone, nella prima riga saranno visualizzati solo i feed video dei partecipanti più attivi, mentre per gli altri partecipanti verranno visualizzate le immagini.

  - I partecipanti possono scegliere di bloccare il video per selezionare uno o più feed video tra quelli disponibili, in modo che siano sempre visibili.

  - I relatori possono utilizzare la funzionalità di video in evidenza per selezionare il feed video di una persona in modo che tutti gli altri partecipanti alla riunione vedano solo il video di tale partecipante.

## Integrazione delle chat room

In Lync 2013 sono ora integrate le funzionalità precedentemente fornite da Lync 2010, Group Chat. Non è più necessario un client Group Chat separato.

  - Da Lync 2013 gli utenti possono cercare chat room, aggiungere chat room ai contatti, monitorare l'attività delle chat room e leggere e pubblicare messaggi.

  - Gli utenti possono creare feed di argomenti in modo da ricevere notifica nel caso qualcuno nelle chat room seguite aggiunga un post con parole chiave specifiche.

  - Con la nuova pagina di opzioni **Chat persistente** gli utenti possono impostare avvisi e suoni di notifica applicabili al post di messaggi nelle loro chat room.

## Aggiornamenti di Lync Web App

Lync Web App è il client per conferenze basate sul Web per le riunioni Lync Server 2013. In questa versione, l'aggiunta di audio e video del computer a Lync Web App offre un'esperienza completa di partecipazione alle riunioni per chiunque non disponga di un client Lync installato in locale. I partecipanti alla riunione hanno accesso a tutte le funzionalità di collaborazione e condivisione, oltre ai controlli della riunione per il relatore.

Quando un utente tenta di partecipare a una riunione, ma non dispone di un client installato in locale, si apre Lync Web App. Se si desidera rendere disponibili ulteriori opzioni per la partecipazione alla riunione, è possibile configurare la pagina di partecipazione alla riunione. Vedere [Configurazione della pagina di partecipazione alle riunioni in Lync Server 2013](lync-server-2013-configuring-the-meeting-join-page.md) nella documentazione relativa alla distribuzione.

Considerati i miglioramenti di Lync Web App, non è disponibile una versione aggiornata di Attendee per Lync Server 2013. Lync Web App è il client prescelto per i partecipanti esterni all'organizzazione. Non è richiesta l'installazione di un client locale, anche se per le funzionalità audio, video e di condivisione è necessario installare un plug-in al primo utilizzo.

## Aggiornamenti di Lync 2013 per client per dispositivi mobili

Oltre alle funzionalità avanzate per presenza, contatti e messaggistica istantanea, i client per dispositivi mobili di Lync 2013 supportano ora chiamate vocali e video tramite Internet e connessioni dati cellulari. Con un singolo tocco del collegamento alla riunione in un elemento del calendario, gli utenti mobili possono partecipare a riunioni di Lync con voce e video. Per ulteriori informazioni sui client per dispositivi mobili di Lync 2013, vedere [Pianificazione dei client mobili](lync-server-2013-planning-for-mobile-clients.md).

## Aggiornamenti dell'interfaccia utente di Lync 2013

## Aggiornamenti dell'accessibilità

Lync 2013 include varie nuove caratteristiche di accessibilità.

  - Lync 2013 supporta alti livelli di risoluzione DPI, che consentono agli utenti di ridimensionare testo e grafica a 125% e 150% punti per pollice.

  - Lync include il supporto per il contrasto elevato in modo che l'interfaccia utente rimanga del tutto funzionale anche quando viene utilizzata con i temi a contrasto elevato di Windows.

  - Lync include più di 100 scelte rapide da tastiera in modo che gli utenti possano accedere a funzioni importanti anche senza un mouse. È ad esempio possibile premere ALT+C per accettare una chiamata o ALT+I per ignorarla, senza doversi spostare con TAB o impostare lo stato attivo. Premendo ALT+Q si interrompe una chiamata, con CTRL+N si avvia OneNote e ALT+T consente di aprire il menu Strumenti.

  - Il supporto esteso di screen reader in Lync 2013 assicura che le notifiche, le richieste in arrivo e i messaggi istantanei vengano tutti letti ad alta voce quando è abilitato un software screen reader.

## Stato presenza durante la condivisione

Quando in Lync viene rilevato che un utente sta utilizzando le funzioni di condivisione, Lync assegna automaticamente all'utente lo stato presenza Presentazione. Questo stato blocca tutte le comunicazioni in arrivo, a meno che al mittente non sia assegnata la relazione di privacy Gruppo di lavoro. Se l'utente utilizza la funzionalità di condivisione interamente in un monitor secondario, Lync non assegna lo stato presenza Presentazione.

## Aggiornamenti della finestra di conversazione

La finestra di conversazione riprogettata consente di accedere più rapidamente a funzionalità importanti.

  - Con la nuova funzionalità per le conversazioni su schede, gli utenti possono ora mantenere tutti i messaggi istantanei e le chat room in una singola finestra di conversazione. Le schede lungo il lato sinistro di questa finestra consentono agli utenti di spostarsi facilmente tra tutte le conversazioni attive.

  - Gli utenti possono disancorare una singola conversazione visualizzandola in una finestra separata e poi ridimensionare la finestra. È inoltre possibile riancorare la finestra alla finestra di conversazione principale.

  - In Lync 2013 le conversazioni di un utente vengono riaperte quando l'utente di disconnette e poi riesegue l'accesso a Lync.

  - Gli utenti possono aggiungere rapidamente gli strumenti per messaggi istantanei, video, condivisione dei programmi, condivisione del desktop o conferenze Web (lavagna, note delle riunioni, blocchi appunti condivisi e allegati) a qualsiasi conversazione.

  - In una riunione con video o contenuto condiviso, gli utenti possono disancorare il video o il contenuto condiviso della riunione e quindi ridimensionare la finestra.

## Aggiornamenti della finestra principale di Lync

Il nuovo aspetto ottimizzato conserva caratteristiche familiari come il campo note **Cosa succede oggi** , il selettore di stato e il selettore **Imposta la posizione** .

  - Quando sono abilitate le chat room, nella pagina principale di Lync viene visualizzata una nuova icona **Chat room** . Con l'icona **Chat room** gli utenti possono accedere rapidamente a chat room e filtri.

  - È possibile fare clic sulle icone delle visualizzazioni per passare rapidamente alla visualizzazione **Contatti** , **Chat room** , **Conversazioni** o **Telefono** .

  - Se è stata eseguita la migrazione degli utenti a Exchange 2013, è consentito il caricamento di un'immagine ad alta risoluzione.

## Aggiornamenti della visualizzazione Contatti e dei biglietti da visita

Lync 2013 offre agli utenti diversi modi per visualizzare contatti e gruppi nella visualizzazione **Contatti** .

  - Con il nuovo archivio contatti unificato, dopo la migrazione dei contatti di Lync a Exchange 2013, sarà possibile visualizzare e gestire i contatti personali da Lync 2013, Outlook o Outlook Web App e i Preferiti rimangono sincronizzati. Se si aggiunge un contatto ai Preferiti in Outlook, ad esempio, il contatto viene visualizzato anche nel gruppo Preferiti in Lync 2013.

  - Se si aggiungono e configurano il proxy XMPP e il gateway XMPP, gli utenti possono aggiungere contatti dai partner XMPP per la messaggistica istantanea e la presenza.

  - La nuova funzionalità **Aggiungi contatto esterno all'organizzazione** consente di aggiungere facilmente persone esterne all'organizzazione.

  - Un nuovo gruppo **Preferiti** consente agli utenti di creare un elenco di persone contattate più di frequente per accedervi più rapidamente.

  - È possibile utilizzare la nuova pagina di opzioni **Elenco contatti** per scegliere la modalità di ordinamento e visualizzazione dei contatti. È possibile selezionare una visualizzazione espansa su due righe che include le immagini dei contatti oppure una visualizzazione ridotta su una riga. Gli utenti possono inoltre disporre i contatti in ordine alfabetico o di disponibilità.

## Aggiornamenti per le conferenze

In Lync 2013 sono disponibili vari miglioramenti delle funzionalità per le conferenze.

  - A seconda del tipo di riunione, è ora possibile disattivare l'audio per il pubblico e consentire o impedire la condivisione del video in fase di pianificazione della riunione. Queste opzioni sono disponibili nella pagina **Opzioni riunione** ed è consigliabile utilizzarle per riunioni con più di 20 partecipanti.

  - I controlli audio di facile utilizzo nella sala riunioni consentono di controllare le opzioni per l'audio, ad esempio disattivare l'audio, riattivare l'audio, cambiare dispositivo e così via.

  - Per la condivisione dei programmi è ora possibile selezionare più programmi da condividere se si desidera utilizzare più di un programma.

  - È ora possibile caricare presentazioni che contengono clip video. È sufficiente caricare il file di PowerPoint e posizionare il mouse sulla diapositiva per visualizzare i controlli video, come i controlli di riproduzione e pausa, nonché i controlli audio.

  - Durante una riunione è possibile unire un'altra conversazione aperta scegliendo **Unisci la chiamata a** nel menu **Altre opzioni** ( **…** ).

  - Per visualizzare i nomi dei partecipanti, è possibile passare il mouse sul pulsante **Mostra partecipanti** oppure fare clic su **Mostra elenco partecipanti** per ancorare il pannello nella riunione.

  - A seconda del tipo di riunione, è possibile scegliere tra varie visualizzazioni diverse per contenuto e partecipanti.

  - Le registrazioni delle riunioni vengono salvate automaticamente in un formato riproducibile in Windows Media Player (MP4). È possibile condividere facilmente il file con chiunque oppure utilizzare la funzionalità **Pubblica** in Gestione registrazioni per pubblicare la registrazione in una posizione condivisa.

  - OneNote rende possibili nuovi scenari di collaborazione in una riunione. Durante una riunione è possibile aggiungere note con OneNote da utilizzare personalmente durante la riunione oppure utilizzare blocchi appunti condivisi per modificarli insieme agli altri partecipanti in tempo reale. Tutti i membri del team possono accedere alle note condivise per fornire il loro contributo, scambiarsi idee o utilizzare le pagine del blocco appunti come lavagna virtuale. Le persone e il contenuto condivisi nella riunione vengono aggiunti automaticamente alle note.

  - È possibile passare da un tipo di contenuto all'altro tramite **Condividi contenuto e conduci attività di riunione** nella parte inferiore della sala riunioni. È inoltre possibile utilizzare il menu **Gestisci contenuto presentabile** per scegliere il contenuto da condividere.

## Vedere anche

#### Ulteriori risorse

[Pianificazione dei client](lync-server-2013-planning-for-clients.md)

