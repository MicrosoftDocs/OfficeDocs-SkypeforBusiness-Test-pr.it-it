---
title: 'Lync Server 2013: Creare o modificare un flusso di lavoro di un gruppo di risposta'
TOCTitle: Creare o modificare un flusso di lavoro di un gruppo di risposta
ms:assetid: dcb9effb-5d12-4dee-80fc-ab9654222d5a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205321(v=OCS.15)
ms:contentKeyID: 49302188
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un flusso di lavoro di un gruppo di risposta in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-09-11_

Eseguire una delle procedure seguenti per creare o modificare il flusso di lavoro di un gruppo di risposta.


> [!NOTE]
> È possibile utilizzare Lync Server Management Shell oppure lo Strumento di configurazione di Response Group per creare e modificare flussi di lavoro di gruppi di risposta. Per accedere allo Strumento di configurazione di Response Group, utilizzare il Pannello di controllo di Lync Server oppure aprire la pagina Web direttamente da un Web browser e digitare l'URL seguente: <STRONG>https://</STRONG> <EM>&lt;FqdnPoolWeb&gt;</EM> <STRONG>/RgsConfig</STRONG> .



## Per utilizzare Strumento di configurazione di Response Group per creare o modificare il flusso di lavoro di un gruppo di risposta

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Response Group** e quindi su **Flusso di lavoro** .

4.  Nella pagina **Flusso di lavoro** fare clic su **Crea o modifica un flusso di lavoro** .

5.  Nel campo di ricerca **Seleziona un servizio** digitare tutto o parte del nome del servizio **ApplicationServer** che ospita il flusso di lavoro che si desidera creare o modificare. Nell'elenco di servizi risultante fare clic sul servizio desiderato e quindi su **OK** .
    

    > [!NOTE]
    > Verrà aperto lo Strumento di configurazione di Response Group. È inoltre possibile aprire lo Strumento di configurazione di Response Group direttamente da un Web browser digitando l'URL seguente: <STRONG>https://</STRONG> <EM>&lt;FqdnPoolWeb&gt;</EM> <STRONG>/RgsConfig</STRONG> .



6.  Eseguire una delle operazioni seguenti:
    
      - In **Crea un nuovo flusso di lavoro** fare clic su **Crea** accanto a Gruppo di risposta.
    
      - In **Gestisci un flusso di lavoro esistente** individuare il flusso di lavoro che si desidera modificare e quindi fare clic su **Modifica** in **Azione** .

7.  Se gli utenti possono iniziare a chiamare il flusso di lavoro immediatamente, selezionare **Attiva il flusso di lavoro** .
    

    > [!NOTE]
    > Se si desidera creare un flusso di lavoro gestito, selezionare <STRONG>Attiva il flusso di lavoro</STRONG> . Dopo aver salvato il flusso di lavoro gestito attivo, è possibile modificarlo e disattivarlo.



8.  Per consentire agli utenti federati di chiamare il gruppo, selezionare la casella di controllo **Abilita per federazione** . È inoltre necessario disporre di un criterio di accesso esterno per l' applicazione Response Group configurata per la federazione.
    

    > [!NOTE]
    > I criteri di accesso esterno globali vengono utilizzati per l' applicazione Response Group. È possibile configurare i criteri globali per la federazione di Response Group utilizzando il Pannello di controllo di Lync Server oppure il cmdlet <STRONG>Set-CsExternalAccessPolicy</STRONG> per impostare il parametro EnableOutsideAccess su True. Considerare che le impostazioni di criteri globali vengono applicate a tutti gli utenti, a meno che non dispongano di un criterio sito o utente assegnato. Prima di modificare questa impostazione per i Response Group, verificare quindi che le impostazioni della federazione soddisfino i requisiti dell'organizzazione. Per informazioni dettagliate sull'applicazione dei criteri agli utenti, vedere <A href="lync-server-2013-manage-external-access-policy-for-your-organization.md">Gestire i criteri di accesso esterno per l'organizzazione in Lync Server 2013</A>. Per informazioni dettagliate sull'impostazione della federazione, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExternalAccessPolicy">Set-CsExternalAccessPolicy</A>.

    

    > [!NOTE]
    > Gli utenti ospitati in Lync Online non possono effettuare chiamate a Response Group ospitati in una distribuzione locale. Ciò vale sia nelle distribuzioni ibride sia per distribuzioni locali federate con una distribuzione di Lync Online.



9.  Per nascondere l'identità degli agenti durante le chiamate, selezionare la casella di controllo **Abilita anonimato agente** .
    

    > [!NOTE]
    > Le chiamate anonime non possono iniziare con un messaggio istantaneo o un video, sebbene l'agente o il chiamante possa aggiungere messaggi istantanei e video dopo l'attivazione della chiamata. Un agente anonimo può inoltre mettere le chiamate in attesa, eseguire trasferimenti di chiamata, nascosti o con consultazione del destinatario, nonché parcheggiare e recuperare le chiamate. Per le chiamate anonime non sono supportate conferenze, condivisione di applicazioni, condivisione del desktop, trasferimenti di file, collaborazione con lavagna e sui dati e registrazione delle chiamate. Gli agenti che utilizzano il plug-in di Lync VDI possono ricevere chiamate in arrivo anonime, ma non possono effettuare chiamate in uscita anonime.



10. In **Immettere l'indirizzo del gruppo che riceverà le chiamate** digitare l'indirizzo URI (Uniform Resource Identifier) SIP primario del gruppo che dovrà rispondere alle chiamate al flusso di lavoro.
    

    > [!NOTE]
    > L'URI primario di un flusso di lavoro viene utilizzato come identificazione e riferimento per un flusso di lavoro. L'URI SIP immesso viene creato come oggetto contatto in Servizi di dominio Active Directory. Per creare l'URI, l'oggetto deve essere univoco in Active Directory.



11. In **Nome visualizzato** digitare il nome che si desidera visualizzare per il flusso di lavoro, ad esempio Response Group Vendite.
    

    > [!NOTE]
    > Non includere i caratteri "&lt;" o "&gt;" nel nome visualizzato. Non utilizzare i nomi visualizzati seguenti, perché sono riservati: <STRONG>RGS Presence Watcher</STRONG> o <STRONG>Servizio Annuncio</STRONG> .



12. In **Numero di telefono** digitare l'URI di linea per il Response Group, ad esempio +14255550165.

13. In **Numero visualizzato** digitare il numero nel modo in cui si desidera venga visualizzato per il Response Group, ad esempio +1 (425) 555-0165.

14. (Facoltativo) In **Descrizione** digitare una descrizione per il flusso di lavoro nel modo in cui si desidera venga visualizzata nella scheda contatto del client Lync.

15. In **Tipo di flusso di lavoro** selezionare **Gestito** se il flusso di lavoro verrà gestito da un responsabile di Response Group. Per assegnare responsabili di Response Group al flusso di lavoro, eseguire le operazioni seguenti:
    
    1.  Digitare l'URI SIP di un responsabile per questo flusso di lavoro e fare clic su **Aggiungi** .
    
    2.  Digitare l'URI SIP di ulteriori responsabili da aggiungere al flusso di lavoro e fare clic su **Aggiungi** .
    
    > [!IMPORTANT]  
    > A ogni utente designato come responsabile di un Response Group deve essere assegnato il ruolo CsResponseGroupManager. Se non viene assegnato loro questo ruolo, non potranno gestire i Response Group.

16. In **Passaggio 2 Selezionare una lingua** fare clic sulla lingua che si desidera utilizzare per il riconoscimento vocale e la sintesi vocale.

17. Se si desidera configurare un messaggio di benvenuto, in **Passaggio 3 Configurare un messaggio di benvenuto** selezionare la casella di controllo **Riprodurre un messaggio di benvenuto** , quindi effettuare una delle operazioni seguenti:
    
      - Per immettere il messaggio di benvenuto come testo della sintesi vocale per i chiamanti, fare clic su **Usa sintesi vocale** , quindi digitare il messaggio nella casella di testo.
        

        > [!NOTE]
        > Non includere tag HTML nel testo immesso. Se si includono tag HTML verrà visualizzato un messaggio di errore.

    
      - Per utilizzare la registrazione di un file WAVE (WAV) o Windows Media Audio (WMA) per il messaggio di benvenuto, fare clic su **Selezionare una registrazione** . Se si desidera caricare un nuovo file audio, fare clic sul collegamento **una registrazione** . Nella nuova finestra del browser fare clic su **Sfoglia** , selezionare il file audio che si desidera utilizzare, quindi fare clic su **Apri** . Fare clic su **Carica** per caricare il file audio.
        

        > [!NOTE]
        > Tutti i file audio forniti dall'utente devono soddisfare requisiti specifici. Per informazioni dettagliate sui formati di file supportati, vedere <A href="lync-server-2013-technical-requirements-for-response-group.md">Requisiti tecnici per i Response Group in Lync Server 2013</A>.



18. In **Passaggio 4 Specificare l'orario di ufficio** fare clic sul fuso orario del flusso di lavoro in **Fuso orario** .
    

    > [!NOTE]
    > È necessario specificare il fuso orario in cui risiedono i chiamanti e gli agenti del flusso di lavoro. Il fuso orario viene utilizzato per calcolare le ore di apertura e di chiusura. Se, ad esempio, il flusso di lavoro è configurato per l'utilizzo del fuso orario orientale ed è pianificato per l'apertura alle 7.00 e la chiusura alle 23.00, si presuppone che le ore di apertura e di chiusura siano rispettivamente le 7.00 e le 23.00 del fuso orario orientale. È necessario immettere le ore nel formato a 24 ore.



19. Selezionare il tipo di pianificazione dell'orario di ufficio che si desidera utilizzare eseguendo una delle operazioni seguenti:
    
      - Per utilizzare una pianificazione dell'orario di ufficio predefinita, fare clic su **Usa pianificazione preimpostata** , quindi selezionare la pianificazione che si desidera utilizzare nell'elenco a discesa.
        

        > [!NOTE]
        > Per potere selezionare questa opzione, è necessario che in precedenza sia stata definita almeno una pianificazione preimpostata. Per definire le pianificazioni preimpostate, utilizzare il cmdlet <STRONG>New-CSRgsHoursOfBusiness</STRONG>. Per informazioni dettagliate, vedere <A href="lync-server-2013-optional-define-response-group-business-hours.md">Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013</A>.

        

        > [!NOTE]
        > Quando si seleziona una pianificazione preimpostata, nei campi <STRONG>Giorno</STRONG> , <STRONG>Apri</STRONG> e <STRONG>Chiudi</STRONG> vengono inseriti automaticamente i giorni e le ore in cui il Response Group è disponibile.

    
      - Per utilizzare una pianificazione personalizzata da applicare solo a questo flusso di lavoro, fare clic su **Usa pianificazione personalizzata** .

20. Se si crea una pianificazione personalizzata per questo flusso di lavoro, fare clic sulle caselle di controllo per i giorni della settimana in cui il Response Group è disponibile.

21. Se si crea una pianificazione personalizzata, digitare le ore in **Apri** e **Chiudi** per ogni giorno della settimana in cui il Response Group è disponibile.
    

    > [!NOTE]
    > Le ore in <STRONG>Apri</STRONG> e <STRONG>Chiudi</STRONG> devono essere nel formato a 24 ore. Se l'ufficio, ad esempio, è operativo dalle 9.00 alle 17.00 con una pausa per il pranzo a mezzogiorno, è possibile specificare l'orario di ufficio impostando <STRONG>Apri</STRONG> su 9.00, <STRONG>Chiudi</STRONG> su 12.00, quindi di nuovo <STRONG>Apri</STRONG> su 13.00 e <STRONG>Chiudi</STRONG> su 17.00.



22. Se si desidera riprodurre un messaggio quando l'ufficio non è aperto, selezionare la casella di controllo **Riproduci un messaggio quando il Response Group non è durante l'orario di ufficio** , quindi specificare il messaggio da riprodurre effettuando una delle operazioni seguenti:
    
      - Per immettere il messaggio come testo della sintesi vocale per il chiamante, fare clic su **Usa sintesi vocale** , quindi digitare il messaggio nella casella di testo.
        

        > [!NOTE]
        > Non includere tag HTML nel testo immesso. Se si includono tag HTML verrà visualizzato un messaggio di errore.

    
      - Per utilizzare la registrazione di un file audio per il messaggio, fare clic su **Selezionare una registrazione** . Se si desidera caricare un nuovo file audio, fare clic sul collegamento **una registrazione** . Nella nuova finestra del browser, fare clic su **Sfoglia** , selezionare il file che si desidera utilizzare, quindi fare clic su **Apri** . Fare clic su **Carica** per caricare il file audio.
        

        > [!NOTE]
        > Tutti i file audio forniti dall'utente devono soddisfare requisiti specifici. Per informazioni dettagliate sui formati di file audio supportati, vedere <A href="lync-server-2013-technical-requirements-for-response-group.md">Requisiti tecnici per i Response Group in Lync Server 2013</A>.



23. Specificare come gestire le chiamate dopo la riproduzione del messaggio (se è stato configurato un messaggio):
    
      - Per interrompere la chiamata, fare clic su **Interrompi chiamata** .
    
      - Per inoltrare la chiamata alla segreteria telefonica, fare clic su **Inoltra a segreteria telefonica** e quindi digitare l'indirizzo della segreteria telefonica. Il formato per l'indirizzo della segreteria telefonica è *\<nomeutente\>* @ *\<nomeDominio\>* , ad esempio francesco@contoso.com.
    
      - Per inoltrare la chiamata a un altro utente, fare clic su **Inoltra a URI SIP** e quindi digitare l'indirizzo dell'utente. Il formato per l'indirizzo dell'utente è *\<nomeutente\>* @ *\<nomeDominio\>* .
    
      - Per inoltrare la chiamata a un altro numero di telefono, fare clic su **Inoltra a numero di telefono** e quindi digitare il numero di telefono. Il formato per il numero di telefono è *\<numero\>* @ *\<nomeDominio\>* , ad esempio +14255550121@contoso.com. Il nome di dominio viene utilizzato per instradare il chiamante alla destinazione corretta.

24. In **Passaggio 5 Specificare le festività** fare clic sulle caselle di controllo per uno o più insiemi di festività che definiscono i giorni in cui il Response Group è chiuso.
    

    > [!NOTE]
    > È necessario definire le festività e i relativi insiemi prima di configurare il flusso di lavoro. Utilizzare i cmdlet <STRONG>New-CsRgsHoliday</STRONG> e <STRONG>New-CsRgsHolidaySet</STRONG> per definire le festività e i relativi insiemi. Per informazioni dettagliate, vedere <A href="lync-server-2013-optional-define-response-group-holiday-sets.md">Definire gli insiemi di festività dei Response Group (facoltativo)</A>.



25. Se si desidera riprodurre un messaggio delle festività, selezionare la casella di controllo **Riproduci un messaggio durante le festività** , quindi specificare il messaggio da riprodurre effettuando una delle operazioni seguenti:
    
      - Per immettere il messaggio come testo della sintesi vocale per il chiamante, fare clic su **Usa sintesi vocale** , quindi digitare il messaggio nella casella di testo.
        

        > [!NOTE]
        > Non includere tag HTML nel testo immesso. Se si includono tag HTML verrà visualizzato un messaggio di errore.

    
      - Per utilizzare la registrazione di un file audio per il messaggio, fare clic su **Selezionare una registrazione** . Se si desidera caricare un nuovo file audio, fare clic sul collegamento **una registrazione** . Nella nuova finestra del browser, fare clic su **Sfoglia** , selezionare il file che si desidera utilizzare, quindi fare clic su **Apri** . Fare clic su **Carica** per caricare il file audio.
        

        > [!NOTE]
        > Tutti i file audio forniti dall'utente devono soddisfare requisiti specifici. Per informazioni dettagliate sui formati di file audio supportati, vedere <A href="lync-server-2013-technical-requirements-for-response-group.md">Requisiti tecnici per i Response Group in Lync Server 2013</A>.



26. Specificare come gestire le chiamate dopo la riproduzione del messaggio (se è stato configurato un messaggio):
    
      - Per interrompere la chiamata, fare clic su **Interrompi chiamata** .
    
      - Per inoltrare la chiamata alla segreteria telefonica, fare clic su **Inoltra a segreteria telefonica** e quindi digitare l'indirizzo della segreteria telefonica. Il formato per l'indirizzo della segreteria telefonica è *\<nomeutente\>* @ *\<nomeDominio\>* , ad esempio francesco@contoso.com.
    
      - Per inoltrare la chiamata a un altro utente, fare clic su **Inoltra a URI SIP** e quindi digitare l'indirizzo dell'utente. Il formato per l'indirizzo dell'utente è *\<nomeutente\>* @ *\<nomeDominio\>* .
    
      - Per inoltrare la chiamata a un altro numero di telefono, fare clic su **Inoltra a numero di telefono** e quindi digitare il numero di telefono. Il formato per il numero di telefono è *\<numero\>* @ *\<nomeDominio\>* , ad esempio +14255550121@contoso.com. Il nome di dominio viene utilizzato per instradare il chiamante alla destinazione corretta.

27. In **Passaggio 6 Configurare una coda** selezionare la coda in cui si desidera mettere in attesa i chiamanti fino a quando non diventa disponibile un agente in **Selezionare la coda che riceverà le chiamate** .

28. In **Passaggio 7 Configurare la musica di attesa** scegliere la musica che si desidera riprodurre per i chiamanti in attesa della risposta di un agente effettuando una delle operazioni seguenti:
    
      - Per utilizzare la registrazione della musica di attesa predefinita, fare clic su **Usa predefinita** .
    
      - Per utilizzare la registrazione di un file audio per la musica di attesa, fare clic su **Selezionare un file musicale** . Se si desidera caricare un nuovo file audio, fare clic sul collegamento **un file musicale** . Nella nuova finestra del browser, fare clic su **Sfoglia** , selezionare il file che si desidera utilizzare e quindi fare clic su **Apri** . Fare clic su **Carica** per caricare il file audio.
        

        > [!NOTE]
        > Tutti i file audio forniti dall'utente devono soddisfare requisiti specifici. Per informazioni dettagliate sui formati di file audio supportati, vedere <A href="lync-server-2013-technical-requirements-for-response-group.md">Requisiti tecnici per i Response Group in Lync Server 2013</A>.



29. Fare clic su **Distribuisci** .

## Per utilizzare Windows PowerShell per creare o modificare il flusso di lavoro di un gruppo di risposta

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Creare il messaggio di benvenuto e salvarlo in una variabile. Nella riga di comando digitare il comando seguente:
    
        $promptWM = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    Ad esempio:
    
        $promptWM = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to Contoso. Please wait for an available agent."
    

    > [!NOTE]
    > Per utilizzare un file audio per il messaggio, eseguire il cmdlet <STRONG>Import-CsRgsAudioFile</STRONG>. Per informazioni dettagliate, vedere <A href="https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile">Import-CsRgsAudioFile</A>.



4.  Ottenere l'identità della coda o informazioni sull'indirizzamento delle chiamate. Nella riga di comando digitare il comando seguente:
    
        $qid = (Get-CsRgsQueue -Name "Help Desk").Identity
    
    Per informazioni dettagliate sulla creazione della coda, vedere [New-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsQueue).

5.  Definire l'azione predefinita da eseguire quando viene aperto un flusso di lavoro durante l'orario di ufficio e salvarla in una variabile. Nella riga di comando digitare il comando seguente:
    
        $actionWM = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken> -QueueID $qid
    

    > [!NOTE]
    > Per i flussi di lavoro di gruppi di risposta, l'azione predefinita consiste nell'indirizzare la chiamata a una coda. Questo parametro è obbligatorio per i flussi di lavoro attivi. Non è obbligatorio invece per i flussi di lavoro inattivi.

    
    Ad esempio:
    
        $actionWM = New-CsRgsCallAction -Prompt $promptWM -Action TransferToQueue -QueueID $qid.Identity

6.  Se si desidera definire l'orario di ufficio e le festività, è necessario eseguire questa operazione prima della creazione o della modifica del flusso di lavoro. Per informazioni dettagliate, vedere [Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013](lync-server-2013-optional-define-response-group-business-hours.md) e [Definire gli insiemi di festività dei Response Group (facoltativo)](lync-server-2013-optional-define-response-group-holiday-sets.md).

7.  Se si desidera fare in modo che vengano inviati avvisi per le chiamate ricevute al di fuori dell'orario di ufficio o durante le festività, utilizzare il cmdlet **New-CsRgsPrompt** per definire l'avviso e il cmdlet **New-CsRgsCallAction** per definire l'azione da eseguire dopo l'avviso. Per informazioni dettagliate, vedere [New-CsRgsPrompt](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsPrompt) e [New-CsRgsCallAction](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction).

8.  Recuperare il nome del servizio per Lync Server, Response Group Service e assegnarlo a una variabile. Nella riga di comando digitare il comando seguente:
    
        $serviceId="service:"+(Get-CSService | ?{$_.Applications -like "*RGS*"}).ServiceId;

9.  Creare o modificare il flusso di lavoro. Per creare un flusso di lavoro, utilizzare **New-CsRgsWorkflow**. Per modificare un flusso di lavoro, utilizzare **Set-CsRgsWorkflow**. Nella riga di comando digitare il comando seguente:
    
        $workflowHG = New-CsRgsWorkflow -Parent <service ID for the Response Group service> -Name "<hunt group name>" [-Description "<hunt group description>"] -PrimaryUri "<SIP address for the workflow>" [-LineUri "<Phone number for the workflow>"] [-DisplayNumber "<Phone number displayed in Lync>"] [-Active <$true | $false>] [-Anonymous <$true | $false>] [-DefaultAction <variable from preceding step>] [-EnabledForFederation <$true | $false>] [-Managed <$true | $false>] [-MangersByUri <SIP addresses for Response Group Managers who can manage the workflow>]
    
    Ad esempio:
    
        $workflowHG = New-CsRgsWorkflow -Parent $serviceID -Name "Human Resources" -Description "Human Resources workflow" -PrimaryUri "sip:humanresources@contoso.com" -LineUri "TEL:+14255551219" -DisplayNumber "555-1219" -Active $true -Anonymous $true -DefaultAction $actionWM -EnabledForFederation $false -Managed $true -ManagersByUri "sip:bob@contoso.com", "mindy@contoso.com"
    
    > [!IMPORTANT]  
    > A tutti gli utenti designati come responsabili dei flussi di lavoro deve essere assegnato il ruolo CsResponseGroupManager.    

    > [!NOTE]
    > Per informazioni dettagliate su ulteriori parametri facoltativi, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsWorkflow">New-CsRgsWorkflow</A> o <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRgsWorkflow">Set-CsRgsWorkflow</A>



## Vedere anche

#### Attività

[Definire gli insiemi di festività dei Response Group (facoltativo)](lync-server-2013-optional-define-response-group-holiday-sets.md)  

#### Concetti

[Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013](lync-server-2013-optional-define-response-group-business-hours.md)  

#### Ulteriori risorse

[New-CsRgsWorkflow](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsWorkflow)  
[Set-CsRgsWorkflow](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRgsWorkflow)  
[New-CsRgsPrompt](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsPrompt)  
[New-CsRgsCallAction](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction)

