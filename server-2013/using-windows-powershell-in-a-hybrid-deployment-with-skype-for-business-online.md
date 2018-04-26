---
title: Uso di Windows PowerShell in una distribuzione ibrida
TOCTitle: Uso di Windows PowerShell in una distribuzione ibrida
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56269969
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso di Windows PowerShell in una distribuzione ibrida

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Una distribuzione ibrida è una distribuzione in cui alcuni utenti dell'organizzazione sono ospitati nella versione locale di Lync Server 2013 e altri in Skype for Business online. È possibile usare un'unica sessione di Windows PowerShell per gestire contemporaneamente sia la versione locale di Lync Server che il tenant di Skype for Business online. A questo scopo è necessario essere in grado di:

1.  Effettuare una connessione simultanea a Lync Server e Skype for Business online.

2.  Fare riferimento alle impostazioni di Skype for Business online da questa connessione simultanea.

Stabilire una connessione simultanea a Lync Server e Skype for Business online è sorprendentemente facile. Basta connettersi a Lync Server nel modo consueto, avviando Lync Server Management Shell o creando una connessione remota a un pool Front End. Dopo avere stabilito la connessione alla versione locale di Lync Server, è possibile connettersi a Skype for Business online usando la stessa procedura che si userebbe per connettersi solo a Skype for Business online. Prima di effettuare questa connessione occorre creare un oggetto credenziali di Windows PowerShell usando le informazioni di accesso di Office 365. A questo scopo, digitare quanto segue al prompt dei comandi di Windows PowerShell e premere INVIO:

    $credential = Get-Credential

Dopo aver premuto INVIO, viene visualizzata la finestra di dialogo **Richiesta credenziali di Windows PowerShell**:

![Credenziali di accesso di Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Credenziali di accesso di Windows PowerShell")

Nella casella **Nome utente** digitare il nome utente di Skype for Business online. Nella casella **Password** digitare la password di Skype for Business online (la password è mascherata e non viene visualizzata sullo schermo). Se ad esempio il nome utente è kenmyer@litwareinc.com e la password è p@ssw0rd\!, la finestra di dialogo avrà l'aspetto seguente:

![Accesso con le credenziali di Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Accesso con le credenziali di Windows PowerShell")

Per creare l'oggetto credenziali, fare clic su **OK**. Una volta creato l'oggetto, è possibile connettersi a Skype for Business online eseguendo il comando seguente:

    $session = New-CsOnlineSession -Credential $credential

Assicurarsi di digitare il comando esattamente come visualizzato. Tenere presente che il nome del dominio di Skype for Business online non ha importanza. Il cmdlet **New-CsOnlineSession** effettua la connessione e l'accesso a Office 365 usando le credenziali specificate. Dopo aver completato la connessione e l'autenticazione, si viene automaticamente reindirizzati all'URI appropriato.

Se la connessione riesce, nella console di Windows PowerShell viene visualizzato un messaggio simile al seguente:

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

Dopo avere stabilito una connessione a Skype for Business online, importare la sessione eseguendo un comando simile al seguente:

    Import-PSSession $session -AllowClobber


> [!NOTE]
> Il parametro AllowClobber verifica che tutti i cmdlet di Skype for Business online vengano importati, inclusi i cmdlet che hanno lo stesso nome dei cmdlet regolari di Lync Server. Questi cmdlet sono molto numerosi, poiché la maggior parte dei cmdlet di Skype for Business online, inclusi <A href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</A>, <A href="new-csexumcontact.md">New-CsExUmContact</A>, <A href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</A> e così via, ha un equivalente locale. I cmdlet accoppiati (ad esempio Lync Server<STRONG>Get-CsMeetingConfiguration</STRONG> e Skype for Business online<STRONG>Get-CsMeetingConfiguration</STRONG>) sono identici, pertanto possono essere usati indifferentemente. L'uso del parametro AllowClobber ha il solo scopo di impedire la visualizzazione dei messaggi di avviso sullo schermo.



A questo punto è possibile iniziare a gestire sia la versione locale di Lync Server che Skype for Business online. In questa fase è importante capire come si distinguono i criteri e le impostazioni di Lync Server da quelli di Skype for Business online. Supponiamo ad esempio di voler modificare le impostazioni di configurazione globali delle riunioni. A questo scopo si esegue il comando seguente:

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

Questo comando modifica le impostazioni globali. Ma quali? Quelle della versione locale di Lync Server? Quelle di Skype for Business online? Entrambe? Nessuna?

In questo caso particolare vengono modificate le impostazioni della versione locale. Lo si capisce dal fatto che il parametro Tenant non è stato incluso nel comando. Se si è connessi contemporaneamente alla versione locale di Lync Server e a Skype for Business online, i cmdlet che funzionano nelle due piattaforme vengono eseguiti in Lync Server a meno che non si specifichi diversamente. E l'unico modo per specificare diversamente consiste nell'includere il parametro Tenant quando si esegue il comando. Ad esempio, il comando seguente aggiorna le impostazioni globali del tenant di Skype for Business online con ID bf19b7db-6960-41e5-a139-2aa373474354:

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

Il parametro Tenant è la chiave. Questo comando restituisce il criterio di accesso esterno globale per la versione locale di Lync Server:

    Get-CsExternalAccessPolicy -Identity "global"

Questo comando invece restituisce il criterio di accesso esterno globale per il tenant di Skype for Business online:

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Tenere presente che esistono ben più di 700 cmdlet locali. Tuttavia, questi cmdlet non hanno, per la maggior parte, un parametro Tenant, che significa che non possono essere usati con Skype for Business online. Esistono anche alcuni cmdlet che hanno un parametro Tenant, ma non sono ancora disponibili per l'uso con Skype for Business online. Per recuperare l'insieme esatto di cmdlet che possono essere usati con Skype for Business online, eseguire il comando seguente dal prompt di Windows PowerShell:

    Get-Module

Sullo schermo verranno visualizzate informazioni simili alle seguenti:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Il modulo con ModuleType uguale a Script è quello che contiene i cmdlet di Skype for Business online. Per ottenere un elenco di questi cmdlet, eseguire il cmdlet **Get-Command** specificando il nome del modulo Script come nome del modulo:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell visualizzerà quindi un elenco di tutti i cmdlet di Skype for Business online.

**Risoluzione dei problemi di connessione in una distribuzione ibrida**

In alcuni casi, gli amministratori potrebbero rilevare dei problemi di accesso a Office 365 durante l'utilizzo di un account locale (ad esempio, administrator@litwareinc.net), invece di un account di Office 365 (ad esempio, administrator@litwareinc.onmicrosoft.com). Se la sincronizzazione delle directory funziona correttamente, è possibile eseguire l'accesso con entrambi gli account: questo infatti è uno dei vantaggi della distribuzione ibrida. Tuttavia, si sono verificati casi in cui un amministratore non è riuscito a eseguire l'accesso utilizzando il proprio account locale. In genere, ciò è dovuto al fatto che l'individuazione automatica tenta di eseguire l'accesso nell'installazione locale di Lync Server invece che in Office 365.

Fortunatamente, questo problema può essere risolto rapidamente. Quando si utilizza il cmdlet **New-CsOnlineSession** per eseguire l'accesso a Office 365, includere il parametro OverrideAdminDomain seguito dal nome di dominio di Office 365. Ad esempio, per eseguire l'accesso a Office 365 utilizzando l'account administrator@litwareinc.net, includere il parametro OverrideAdminDomain seguito dal nome di dominio litwareinc.onmicrosoft.com:

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

Tale comando indirizzerà esplicitamente il tentativo di accesso ai server di Office 365 e al dominio litwareinc.onmicrosoft.com.

