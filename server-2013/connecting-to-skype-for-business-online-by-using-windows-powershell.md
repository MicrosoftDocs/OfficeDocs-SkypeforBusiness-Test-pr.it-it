---
title: Connessione a Lync Online tramite Windows PowerShell
TOCTitle: Connessione a Lync Online tramite Windows PowerShell
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56269914
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connessione a Lync Online tramite Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Una volta installati i prerequisiti software, è possibile iniziare a usare Windows PowerShell per la gestione di Skype for Business online. A tale scopo, iniziare aprendo un'istanza standard di Windows PowerShell. Non è necessario aprire un'istanza speciale di Windows PowerShell (ad esempio Lync Server Management Shell), né aprire alcuna app del Pannello di controllo o qualunque altro tipo di applicazione speciale. Ciò è dovuto al fatto che la gestione di Skype for Business online viene eseguita usando una sessione remota di Windows PowerShell. Questo significa che:

1.  Per connettersi a Skype for Business online si usa una sessione standard di Windows PowerShell. Durante la connessione in remoto, si usa il computer locale con la copia locale di Windows PowerShell, ma è si gestiscono oggetti che si trovano in un sistema remoto (ovvero Skype for Business online).

2.  Tutti i cmdlet, gli script e gli altri elementi necessari per gestire Skype for Business online vengono scaricati nel computer. Questi elementi vengono conservati in memoria e sono disponibili solo nelle sessioni remote stabilite con Skype for Business online. È importante ricordare questa informazione. Quando si esegue una connessione remota a Skype for Business online, i cmdlet di Skype for Business online, ad esempio [Get-CsTenant](get-cstenant.md), vengono copiati nella memoria del computer. Nella sessione remota sarà quindi possibile eseguire questi cmdlet, i quali però saranno disponibili solo in quella sessione remota. Si può ad esempio avviare una seconda sessione di Windows PowerShell, ma senza connettersi a Skype for Business online in questa sessione. Se si tenta di eseguire il cmdlet **Get-CsTenant** dall'interno di quella sessione, viene visualizzato il messaggio di errore seguente:
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    Tenere inoltre presente che la ricerca del cmdlet **Get-CsTenant** (o di qualsiasi altro cmdlet di Skype for Business online) non restituirà alcun risultato. Questo perché nulla viene effettivamente salvato nel disco rigido quando si crea una sessione remota.

3.  Quando si chiude la sessione remota, gli elementi scaricati vengono eliminati dalla memoria del computer. Ad esempio, è possibile avviare una sessione remota di Windows PowerShell con il cmdlet **Get-CsTenant**, quindi chiudere la sessione. Se si riavvia Windows PowerShell, il cmdlet **Get-CsTenant** non sarà più disponibile. Per accedere al cmdlet **Get-CsTenant**, sarà necessario riconnettersi a Skype for Business online.


> [!NOTE]
> Se si utilizza una distribuzione ibrida, è necessario seguire le procedure illustrare nell'articolo <A href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">Uso di Windows PowerShell in una distribuzione ibrida</A>.



Per creare una connessione remota a Skype for Business online, iniziare avviando una nuova sessione di Windows PowerShell nel computer locale. Se si esegue Windows 7, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2, procedere come segue:

  - Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Accessori**, fare clic su **Windows PowerShell** e quindi su **Windows PowerShell**.

Se si esegue Windows 8 o 8.1, procedere come segue:

  - Accedere alla barra degli accessi, fare clic su **Cerca**, quindi su **Windows PowerShell**. È possibile accedere rapidamente alla barra degli accessi in qualsiasi computer con Windows 8 o 8.1 (dotato o meno di touchscreen) tenendo premuti contemporaneamente il tasto WINDOWS e il tasto C.

Quando viene visualizzata la console di Windows PowerShell è necessario creare un oggetto credenziali di Windows PowerShell. L'oggetto credenziali si usa per comunicare in modo sicuro il nome utente e la password a Skype for Business online. Per creare un oggetto credenziali, digitare il comando seguente al prompt di Windows PowerShell e premere INVIO:

    $credential = Get-Credential


> [!NOTE]
> In questo esempio il nome utente e la password vengono archiviati nella variabile $credential. A questa variabile è possibile assegnare un nome qualsiasi, purché sia conforme alle regole relative ai nomi di variabili per Windows PowerShell. L'uso di una variabile è comunque necessario per archiviare il nome utente e la password, altrimenti l'oggetto credenziali creato scomparirà subito dopo essere stato creato.



Dopo aver premuto INVIO, viene visualizzata la finestra di dialogo **Richiesta credenziali di Windows PowerShell**:

![Credenziali di accesso di Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Credenziali di accesso di Windows PowerShell")

Nella casella **Nome utente** digitare il nome utente di Skype for Business online. Nella casella **Password** digitare la password di Skype for Business online (la password è mascherata e non viene visualizzata sullo schermo). Se ad esempio il nome utente è kenmyer@litwareinc.com e la password è p@ssw0rd\!, la finestra di dialogo avrà l'aspetto seguente:

![Accesso con le credenziali di Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Accesso con le credenziali di Windows PowerShell")

Per creare l'oggetto credenziali, fare clic su **OK**. Per verificare che l'oggetto sia stato creato, digitare il nome della variabile al prompt di Windows PowerShell quindi premere INVIO:

    $credential

Windows PowerShell risponde visualizzando un messaggio simile al seguente:

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString


> [!NOTE]
> Tenere presente che il cmdlet <STRONG>Get-Credential</STRONG> accetta qualsiasi set di credenziali immesso e non tenta di verificare la validità del nome utente e della password fornite. La convalida avviene solo quando si prova ad accedere a Skype for Business online.



Una volta creato l'oggetto credenziali, si può creare una nuova sessione remota di Windows PowerShell che stabilisce una connessione a Skype for Business online. A tale scopo, digitare il comando seguente al prompt di Windows PowerShell e premere INVIO:

    $session = New-CsOnlineSession -Credential $credential


> [!NOTE]
> $session è una variabile usata per memorizzare informazioni. Nel caso specifico, si tratta delle informazioni relative alla connessione a Skype for Business online. Si potrà quindi assegnare a questa variabile un nome qualsiasi, purché sia conforme alle linee guida relative ai nomi di variabili per Windows PowerShell (il nome non deve ad esempio contenere spazi vuoti o segni di punteggiatura).



Accertarsi di digitare il comando esattamente come visualizzato (con l'unica possibile eccezione relativa al nome della variabile). Tenere presente che il nome del dominio di Skype for Business online non ha importanza. Indipendentemente dal nome del dominio, il cmdlet **New-CsOnlineSession** effettua la connessione e l'accesso a Office 365 usando le credenziali specificate. Dopo aver completato la connessione e l'autenticazione, si viene automaticamente reindirizzati all'URI appropriato in base alle credenziali fornite.

Se la connessione riesce, nella console di Windows PowerShell vengono visualizzati dei messaggi simili ai seguenti:

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

Ora si è quasi pronti per iniziare a usare Windows PowerShell per la gestione di Skype for Business online. Il cmdlet **New-CsOnlineSession** si connette a Skype for Business online e crea una nuova sessione per l'utente, ma per essere davvero pronti è necessario importare questa sessione nella console di Windows PowerShell eseguendo il comando seguente:

    Import-PSSession $session

Quando si preme INVIO, viene visualizzato un indicatore di stato simile a quello visualizzato nella console di Windows PowerShell:

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

A questo punto Windows PowerShell scarica cmdlet e altri elementi necessari per la gestione di Skype for Business online. Al termine del download, nella console di Windows PowerShell verranno visualizzate informazioni simili a quelle riportate di seguito:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

Si è ora pronti per iniziare a usare Windows PowerShell per la gestione di Skype for Business online. Per verificare che il download sia riuscito e per visualizzare i cmdlet di Skype for Business online disponibili, è prima necessario determinare il nome del modulo Windows PowerShell temporaneo che contiene tutti i cmdlet di Skype for Business online. A tale scopo, eseguire il comando seguente dal prompt di Windows PowerShell:

    Get-Module

Verranno visualizzate informazioni simili a quelle riportate di seguito:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Il modulo con ModuleType uguale a Script è quello che contiene i cmdlet di Skype for Business online. Per ottenere un elenco di questi cmdlet, eseguire il cmdlet **Get-Command** specificando il nome del modulo Script come nome del modulo:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell visualizzerà quindi un elenco di tutti i cmdlet di Skype for Business online.

Dopo aver completato le attività di gestione, eseguire sempre il comando seguente prima di chiudere la console di Windows PowerShell:

    Remove-PSSession $session

Il cmdlet **Remove-PSSession** disconnette l'utente da Skype for Business online e chiude la sessione remota. Se si cerca di reimportare la sessione eseguendo il cmdlet **Import-PSSession**, viene infatti visualizzato il messaggio di errore seguente:

    Import-PSSession : State of runspace is not valid for this operation.

Questo messaggio significa semplicemente che per riconnettersi a Skype for Business online si dovrà creare una nuova sessione.

Se si dimentica di rimuovere la sessione prima di chiudere la console di Windows PowerShell, o se la console viene chiusa in modo imprevisto, non accadrà nulla di grave. Dopo 15 minuti di inattività, la sessione si disconnetterà automaticamente. Per impostazione predefinita, a ciascun amministratore di Skype for Business online sono tuttavia consentite solo tre sessioni simultanee a Skype for Business online. Se si chiude la console di Windows PowerShell senza rimuovere la sessione, la sessione chiusa verrà comunque contata come una connessione anche se in quel momento non è in uso e continuerà ad essere considerata come tale fino a quando non se ne verificherà il timeout. Se ad esempio si apre e si chiude la console di Windows PowerShell per tre volte, senza rimuovere ogni volta la sessione di Skype for Business online, quando si apre nuovamente Windows PowerShell e si tenta di effettuare una quarta connessione, il comando si bloccherà e non verrà stabilita alcuna connessione.


> [!NOTE]
> Se Windows PowerShell si blocca durante il tentativo di stabilire una connessione, premere CTRL+C per terminare il comando bloccato.



Mentre i singoli amministratori possono creare fino a tre connessioni simultanee a un tenant di Skype for Business online, alle organizzazioni è consentito creare fino a nove connessioni simultanee. Ciò significa che tre singoli amministratori possono creare fino a tre connessioni simultanee ciascuno, oppure nove amministrazioni possono creare una connessione ciascuno a Skype for Business online e così via. Nessun singolo amministratore, tuttavia, potrà avere più di tre sessioni attive.

## Vedere anche

#### Concetti

[Configurazione del computer per la gestione di Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

